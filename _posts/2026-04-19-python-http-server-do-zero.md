---
layout: post
title: "Construindo um HTTP Server do Zero com Python Puro"
description: "Análise técnica de um servidor HTTP minimalista implementado em Python padrão, sem frameworks externos, demonstrando os fundamentos do protocolo HTTP."
date: 2026-04-19
tags: ["projects", "github", "python", "http", "networking", "web-server"]
categories: ["networking", "python", "systems"]
---

O projeto **simple-python-webserver** é um exercício fundamental em engenharia de sistemas: implementar um servidor HTTP do zero usando apenas a biblioteca padrão do Python. Este projeto demonstra compreensão profunda do protocolo HTTP e dos princípios de sockets TCP.

## Por que Construir um Server do Zero?

Entender como servidores web funcionam em baixo nível é essencial para:
- **Depuração**: Compreender erros de rede e problemas de comunicação
- **Performance**: Identificar gargalos em frameworks web
- **Segurança**: Reconhecer vulnerabilidades como SQL injection, XSS
- **Arquitetura**: Projetar sistemas distribuídos com clareza

## Arquitetura do Servidor

```
simple-python-webserver/
├── src/
│   └── http_server.py    # Implementação principal
├── tests/
│   └── test_http_server.py
└── README.md
```

## Implementação Técnica

### 1. Socket TCP Básico

O servidor utiliza a API de sockets do Python para comunicação de rede:

```python
import socket
from http.server import HTTPServer, BaseHTTPRequestHandler
from urllib.parse import urlparse

class HTTPServer:
    def __init__(self, host='0.0.0.0', port=8000):
        self.host = host
        self.port = port
        self.server_socket = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
        self.server_socket.setsockopt(socket.SOL_SOCKET, socket.SO_REUSEADDR, 1)
    
    def start(self):
        self.server_socket.bind((self.host, self.port))
        self.server_socket.listen(5)
        print(f"Server running on http://{self.host}:{self.port}")
        
        while True:
            client_socket, address = self.server_socket.accept()
            self.handle_request(client_socket, address)
    
    def handle_request(self, client_socket, address):
        request = client_socket.recv(4096).decode('utf-8')
        response = self.process_request(request)
        client_socket.sendall(response)
        client_socket.close()
```

### 2. Parsing de Requisições HTTP

O protocolo HTTP é textual. Uma requisição GET simples:

```
GET /index.html HTTP/1.1
Host: localhost:8000
User-Agent: curl/7.68.0
Accept: */*
```

```python
class HTTPRequest:
    def __init__(self, raw_request: str):
        self.method = None
        self.path = None
        self.headers = {}
        self.body = None
        self.parse(raw_request)
    
    def parse(self, raw_request: str):
        lines = raw_request.split('\r\n')
        
        # Primeira linha: METHOD PATH HTTP/VERSION
        request_line = lines[0].split(' ')
        self.method = request_line[0]
        self.path = request_line[1]
        
        # Parse headers
        for line in lines[1:]:
            if line == '':
                break
            key, value = line.split(': ', 1)
            self.headers[key.lower()] = value
        
        # Body (após linha vazia)
        body_start = raw_request.find('\r\n\r\n')
        if body_start != -1:
            self.body = raw_request[body_start + 4:]
```

### 3. Construção de Respostas HTTP

Respostas HTTP seguem o formato:

```
HTTP/1.1 200 OK
Content-Type: text/html
Content-Length: 123

<html>...</html>
```

```python
class HTTPResponse:
    STATUS_CODES = {
        200: 'OK',
        404: 'Not Found',
        500: 'Internal Server Error',
        400: 'Bad Request',
        405: 'Method Not Allowed'
    }
    
    def __init__(self):
        self.status_code = 200
        self.headers = {'Content-Type': 'text/html'}
        self.body = ''
    
    def build(self) -> bytes:
        status_line = f"HTTP/1.1 {self.status_code} {self.STATUS_CODES[self.status_code]}\r\n"
        
        headers = ''.join(f"{k}: {v}\r\n" for k, v in self.headers.items())
        headers += f"Content-Length: {len(self.body)}\r\n"
        
        response = f"{status_line}{headers}\r\n".encode('utf-8')
        response += self.body.encode('utf-8')
        
        return response
```

### 4. Servindo Arquivos Estáticos

```python
class StaticFileHandler:
    def __init__(self, root_dir='.'):
        self.root_dir = root_dir
        self.mime_types = {
            'html': 'text/html',
            'css': 'text/css',
            'js': 'application/javascript',
            'png': 'image/png',
            'jpg': 'image/jpeg',
            'json': 'application/json'
        }
    
    def serve(self, path: str) -> HTTPResponse:
        # Security: prevent directory traversal
        safe_path = self.sanitize_path(path)
        
        try:
            with open(safe_path, 'rb') as f:
                content = f.read()
            
            response = HTTPResponse()
            response.body = content
            response.headers['Content-Type'] = self.guess_mime_type(safe_path)
            return response
            
        except FileNotFoundError:
            return self.not_found()
    
    def sanitize_path(self, path: str) -> str:
        # Remove leading slash and sanitize
        safe_path = path.lstrip('/')
        safe_path = os.path.normpath(safe_path)
        
        full_path = os.path.join(self.root_dir, safe_path)
        
        # Prevent directory traversal attack
        if not full_path.startswith(os.path.abspath(self.root_dir)):
            raise ValueError("Access denied")
        
        return full_path
```

## Testes

O projeto inclui testes unitários usando `unittest`:

```python
import unittest
from http_server import HTTPRequest, HTTPResponse, StaticFileHandler

class TestHTTPRequest(unittest.TestCase):
    def test_parse_get_request(self):
        raw = "GET /index.html HTTP/1.1\r\nHost: localhost\r\n\r\n"
        request = HTTPRequest(raw)
        self.assertEqual(request.method, 'GET')
        self.assertEqual(request.path, '/index.html')
    
    def test_parse_headers(self):
        raw = "GET / HTTP/1.1\r\nAccept: */*\r\n\r\n"
        request = HTTPRequest(raw)
        self.assertEqual(request.headers['accept'], '*/*')

class TestSecurity(unittest.TestCase):
    def test_directory_traversal_blocked(self):
        handler = StaticFileHandler()
        with self.assertRaises(ValueError):
            handler.sanitize_path('../../../etc/passwd')
```

## Conceitos Fundamentais Demonstrados

| Conceito | Aplicação |
|----------|-----------|
| TCP Sockets | Comunicação cliente-servidor |
| HTTP Protocol | Estrutura de requisições/respostas |
| File I/O | Leitura de arquivos estáticos |
| MIME Types | Content negotiation |
| Security | Prevenção de path traversal |
| Concurrency | Aceitar múltiplos clientes |

## Limitações e Extensões

**O que o servidor faz:**
- GET requests
- Arquivos estáticos
- MIME type detection
- Security contra directory traversal

**O que poderia ser adicionado:**
- POST requests e handling de formulários
- CGI/WSGI support
- Keep-alive connections
- HTTPS/TLS
- Directory listing
- Compression (gzip)
- Caching headers

## Conclusão

Construir um servidor HTTP do zero é um dos melhores exercícios para entender como a web funciona. O **simple-python-webserver** demonstra que com poucas centenas de linhas de Python padrão, é possível criar um servidor funcional que compreende o protocolo HTTP.

Este conhecimento é a base para trabalhar com qualquer framework web — Flask, Django, FastAPI — pois você entenderá o que acontece por baixo dos panos.

**Repositório**: [github.com/albertguedes/simple-python-webserver](https://github.com/albertguedes/simple-python-webserver)
