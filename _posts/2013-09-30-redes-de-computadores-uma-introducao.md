---
layout: post
title: "Redes de Computadores: Uma Introdução"
description: "Entenda como dispositivos se comunicam em rede, dos conceitos básicos à internet."
date: 2013-09-30
---

Vivemos em um mundo conectado. Quando você envia uma mensagem, assiste a um vídeo ou acessa um site, está participando de uma complexa rede de comunicação entre computadores espalhados pelo globle. As **redes de computadores** são o sistema nervoso da era digital.

## O que é uma Rede de Computadores?

Uma **rede de computadores** é um conjunto de dispositivos interconectados capazes de trocar dados entre si. Esses dispositivos podem incluir:

- Computadores pessoais
- Smartphones e tablets
- Servidores
- Roteadores e switches
- Dispositivos IoT (Internet das Coisas)

## Classificação das Redes

### Por Escala (HAN, LAN, MAN, WAN)

| Tipo | Abrangência | Exemplos |
|------|-------------|----------|
| **PAN** |few metros | Bluetooth entre celular e fone |
| **LAN** | Edifício/Campus | Rede de escritório ou escola |
| **MAN** | Cidade | Rede universitaria entre campus |
| **WAN** | País/Mundo | A internet |

### Por Topologia

A **topologia** descreve como os dispositivos são interconectados geometricamente:

- **Barramento**: Todos os dispositivos conectados a um único cabo
- **Estrela**: Todos conectados a um hub ou switch central
- **Anel**: Dispositivos conectados em círculo
- **Malha**: Múltiplas conexões entre dispositivos

## O Modelo OSI

Para padronizar a comunicação em rede, desenvolveu-se o **modelo OSI** (Open Systems Interconnection), com 7 camadas:

1. **Física**: Transmissão de bits brutos (cabos, sinais elétricos)
2. **Enlace de Dados**: Quadros, endereço MAC, controle de erros
3. **Rede**: Roteamento, endereço IP
4. **Transporte**: TCP/UDP, portas, controle de fluxo
5. **Sessão**: Gerenciamento de conexões
6. **Apresentação**: Criptografia, compressão, formatação
7. **Aplicação**: HTTP, FTP, SMTP, DNS

## Protocolos Fundamentais

### TCP/IP

A arquitetura da internet usa o conjunto de protocolos **TCP/IP**:

- **IP (Internet Protocol)**: Endereçamento e roteamento de pacotes
- **TCP (Transmission Control Protocol)**: Garantia de entrega ordenada e sem erros
- **UDP (User Datagram Protocol)**: Comunicação sem conexão, mais rápida

### Endereçamento IP

Cada dispositivo na internet tem um endereço IP único:

- **IPv4**: 4 bytes (ex: 192.168.1.1) — addresses agotados
- **IPv6**: 16 bytes (ex: 2001:0db8::1) — praticamente ilimitado

### DNS (Domain Name System)

O DNS traduz nomes de domínio para endereços IP:

```
www.google.com → 142.250.185.46
```

### HTTP/HTTPS

- **HTTP**: Protocolo de transferência de páginas web (não seguro)
- **HTTPS**: Versão criptografada (secure), essencial para comércio eletrônico

## Como a Internet Funciona

Quando você digita um endereço no navegador:

1. **DNS Lookup**: O navegador pergunta ao servidor DNS pelo IP do domínio
2. **Conexão TCP**: Navegador estabelece conexão com o servidor
3. **Requisição HTTP**: Navegador envia pedido da página
4. **Resposta**: Servidor envia HTML, CSS, JavaScript
5. **Renderização**: Navegador processa e exibe a página

Esse processo leva milissegundos, mas envolve dozens de servidores, roteadores e links ao redor do mundo.

## Meios de Transmissão

### Cabos

- **Cabo de par trançado**: Comum em redes locais (Cat5e, Cat6)
- **Cabo coaxial**: TV a cabo, algumas redes antigas
- **Fibra óptica**: Alta velocidade, longa distância

### Sem Fio

- **Wi-Fi**: Redes locais sem fio (IEEE 802.11)
- **Bluetooth**: Curta distância, baixo consumo
- **Celular**: 4G, 5G para mobilidade
- **Satélite**: Áreas remotas

## Segurança em Redes

### Ameaças Comuns

- **Malware**: Vírus, worms, trojans
- **Phishing**: Fraudes para roubar informações
- **Ataques DDoS**: Sobrecarregar servidores
- **Man-in-the-Middle**: Interceptação de comunicações

### Medidas de Proteção

- **Firewall**: Filtra tráfego não autorizado
- **Criptografia**: Protege dados em trânsito
- **VPN**: Cria túneis seguros pela internet
- **Autenticação**: Senhas, 2FA, biometria

---

**Série: Infraestrutura Web**
1. [Como Funciona a Internet?]({{ site.baseurl }}/como-funciona-a-internet)
2. [Redes de Computadores: Uma Introdução]({{ site.baseurl }}/redes-de-computadores-uma-introducao) ← *você está aqui*
3. [Bancos de Dados: Conceitos Fundamentais]({{ site.baseurl }}/bancos-de-dados-conceitos-fundamentais)
4. [Segurança da Informação: Princípios Básicos]({{ site.baseurl }}/seguranca-da-informacao-principios-basicos)

## Leia Mais

- Kurose, J. F. & Ross, K. W. *Redes de Computadores e a Internet*. 7ª Ed. Pearson, 2017.
- Tanenbaum, A. S. & Wetherall, D. *Redes de Computadores*. 5ª Ed. Prentice Hall, 2011.
- Stallings, W. *Data and Computer Communications*. 10ª Ed. Pearson, 2013.
