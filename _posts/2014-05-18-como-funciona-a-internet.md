---
layout: post
title: "Como Funciona a Internet?"
description: "Uma explicação acessível de como dados circulam pela internet, de pacotes a servidores."
date: 2014-05-18
---

A internet é uma das criações mais complexas e fascinantes da humanidade. Bilhões de dispositivos conectados trocando informações em milissegundos — tudo isso funcionando através de padrões, protocolos e uma infraestrutura global impressionante. Vamos desvendar como tudo isso funciona.

## O Básico: O que é a Internet?

A internet é uma **rede de redes** — uma interconexão de milhões de redes menores, cada uma contendo dispositivos que se comunicam usando protocolos padronizados. Não existe uma entidade que "controla" a internet; ela funciona através de acordos e padrões voluntáriados.

## A Infraestrutura Física

### Backbones

O núcleo da internet são os **backbones** — fibras ópticas de alta velocidade que conectam continentes. Esses cabos submarinos são responsáveis por quase todo o tráfego internacional:

- Mais de 400 cabos submarinos atravessam os oceanos
- Alguns cables têm comprimento de milhares de quilômetros
- Capacidade de vários terabits por segundo

### IXPs (Internet Exchange Points)

Pontos de troca de tráfego onde provedores se conectam para trocar dados localmente, evitando rotas internacionais desnecessárias.

### Provedores de Internet (ISPs)

Empresas como Vivo, Claro, NET e outras são ISPs que conectam usuários finais à infraestrutura global. Elas operam em diferentes níveis:

- **Tier 1**: Provedores globais que possuem backbones internacionais
- **Tier 2**: Provedores regionais
- **Tier 3**: Provedores locais

## O Modelo TCP/IP

A comunicação na internet usa o conjunto de protocolos **TCP/IP**, organizado em camadas:

### 1. Camada de Aplicação
HTTP, HTTPS, FTP, SMTP, DNS — protocolos que usuários diretamente utilizam.

### 2. Camada de Transporte
**TCP**: Garante que dados cheguem ordenados e sem erros.
**UDP**: Mais rápido, mas sem garantias (usado em streaming, gaming).

### 3. Camada de Internet (Rede)
**IP (Internet Protocol)**: Endereçamento e roteamento de pacotes.

### 4. Camada de Enlace
Ethernet, Wi-Fi — como dados são transmitidos fisicamente em uma rede local.

## Endereços IP: Os Números da Internet

Cada dispositivo na internet tem um endereço IP único:

### IPv4
```
192.168.1.1
```
4 bytes, cerca de 4 billion addresses — esgotados!

### IPv6
```
2001:0db8:85a3:0000:0000:8a2e:0370:7334
```
16 bytes, virtually ilimitado.

## DNS: A Agenda Telefônica da Internet

Você não digita endereços IP para acessar sites — usa nomes de domínio. O **DNS** (Domain Name System) traduz esses nomes em endereços IP.

```
www.google.com → 142.250.185.46
youtube.com → 142.250.186.78
```

O sistema é hierárquico:
1. Servidores raiz
2. Servidores TLD (.com, .org, .br)
3. Servidores autoritativos de domínio

## Como Funciona uma Requisição Web

Quando você digita um endereço no navegador:

### Passo 1: DNS Lookup
O navegador pergunta a um servidor DNS pelo IP do domínio.

### Passo 2: Estabelecimento de Conexão TCP
Navegador e servidor "se cumprimentam" para estabelecer comunicação confiável.

### Passo 3: Requisição HTTP
Navegador envia um pedido como:
```
GET /pagina HTTP/1.1
Host: www.exemplo.com
```

### Passo 4: Resposta
Servidor responde com código de status (200 OK, 404 Not Found) e conteúdo.

### Passo 5: Renderização
Navegador interpreta HTML, CSS, JavaScript e exibe a página.

## Pacotes: A Unidade de Dados

Informações não são enviadas como um bloco único — são divididas em **pacotes**:

- Cada pacote tem cabeçalho (endereços, informações de controle)
- Pacotes podem seguir rotas diferentes
- Receptor reassembla os pacotes na ordem correta

## HTTP vs HTTPS

- **HTTP**: Dados transmitidos em texto claro — qualquer um no meio pode ler
- **HTTPS**: Dados criptografados usando TLS/SSL — seguro para transações sensíveis

Hoje, a maioria dos sites usa HTTPS por padrão, indicado pelo cadeado no navegador.

## CDN: Accelerando a Entrega de Conteúdo

**Content Delivery Networks** são redes de servidores distribuídos geograficamente que armazenam cópias de conteúdo:

- Quando você acessa um site, o servidor mais próximo entrega o conteúdo
- Reduz latência e carga no servidor de origem
- Exemplos: Cloudflare, Akamai, Amazon CloudFront

## O Futuro: IPV6, HTTP/3 e Mais

A internet continua evoluindo:

- **IPv6**: Adoção crescente para resolver o esgotamento de endereços
- **HTTP/3**: Baseado em QUIC, mais rápido e confiável
- **WebAssembly**: Código de alto desempenho no navegador

---

**Série: Infraestrutura Web**
1. [Como Funciona a Internet?]({{ site.baseurl }}/como-funciona-a-internet) ← *você está aqui*
2. [Redes de Computadores: Uma Introdução]({{ site.baseurl }}/redes-de-computadores-uma-introducao)
3. [Bancos de Dados: Conceitos Fundamentais]({{ site.baseurl }}/bancos-de-dados-conceitos-fundamentais)
4. [Segurança da Informação: Princípios Básicos]({{ site.baseurl }}/seguranca-da-informacao-principios-basicos)

## Leia Mais

- Kurose, J. F. & Ross, K. W. *Redes de Computadores e a Internet*. 7ª Ed. Pearson, 2017.
- Tanenbaum, A. S. & Wetherall, D. *Redes de Computadores*. 5ª Ed. Prentice Hall, 2011.
- RFC 791 - Internet Protocol. IETF.
- DNS RFCs: RFC 1034, RFC 1035.
