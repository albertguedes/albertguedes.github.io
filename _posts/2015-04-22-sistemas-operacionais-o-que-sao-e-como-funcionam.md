---
layout: post
title: "Sistemas Operacionais: O que São e Como Funcionam"
description: "Entenda o papel fundamental do sistema operacional na intermediação entre hardware e software."
date: 2015-04-22
---

Quando você liga seu computador e aguarda a tela inicial aparecer, algo extraordinário acontece nos bastidores: o **sistema operacional** (SO) assume o controle, gerenciando hardware e fornecendo serviços para que aplicativos possam executar. Sem sistemas operacionais, cada programa precisaria conhecer os detalhes de cada componente de hardware.

## O que é um Sistema Operacional?

Um **sistema operacional** é um programa que atua como intermediário entre o usuário e o hardware do computador. Suas funções principais são:

1. **Gerenciar recursos de hardware** (CPU, memória, disco, periféricos)
2. **Fornecer uma interface para execução de programas**
3. **Proteger o sistema de falhas e acessos não autorizados**

Exemplos populares: Windows, macOS, Linux, Android, iOS.

## Arquitetura de um Sistema Operacional

### Kernel

O **núcleo** é a parte central do SO, sempre residente na memória. Ele gerencia:
- Comunicação com hardware
- Escalonamento de processos
- Alocação de memória
- Sistema de arquivos

### Espaço do Usuário

Área onde rodam os programas do usuário — navegadores, editores de texto, jogos. Aplicativos nunca acessam hardware diretamente; eles pedem ao kernel.

### System Calls (Chamadas de Sistema)

A interface entre o espaço do usuário e o kernel. Programas usam system calls para:
- Ler/escrever arquivos
- Criar processos
- Alocar memória
- Comunicar-se pela rede

## Processos e Thread

### O que é um Processo?

Um **processo** é um programa em execução. Cada processo tem:
- Seu próprio espaço de memória
- Contador de instruções
- Registradores da CPU
- Arquivos abertos

### Thread

Um **thread** é uma linha de execução dentro de um processo. Múltiplos threads compartilham a memória do processo, mas cada um tem seu próprio contador de instruções.

### Escalonamento (Scheduling)

O kernel decide qual processo/thread executa em cada momento. Algoritmos comuns:

- **FIFO**: Primeiro a chegar, primeiro a executar
- **Round-Robin**: Cada processo ganha tempo igual em rodízio
- **Priority-based**: Processos prioritários executam primeiro

## Gerenciamento de Memória

### Memória Virtual

Cada processo acredita ter toda a memória para si. O SO mapeia endereços virtuais para físicos, permitindo:

- **Isolamento**: Processos não podem acessar memória de outros
- **Overcommitment**: SO pode oferecer mais memória do que fisicamente existe
- **Swap**: mover partes inativas para o disco

### Paginação

Memória dividida em páginas (típico 4KB). MMU (Memory Management Unit) traduz endereços virtuais para físicos.

### RAM vs Swap

Quando a RAM se esgota, o SO move páginas menos ativas para o disco (swap), liberando RAM para processos ativos.

## Sistema de Arquivos

O SO organiza dados em arquivos e diretórios através de um **sistema de arquivos**:

| Sistema | Uso Comum |
|---------|-----------|
| NTFS | Windows |
| APFS, HFS+ | macOS |
| ext4, XFS, Btrfs | Linux |
| FAT32, exFAT | Dispositivos USB |

### Estrutura de Diretórios

```
/ (root)
├── home/
│   └── usuario/
│       ├── documentos/
│       └── downloads/
├── etc/ (configurações)
├── var/ (dados variáveis)
└── tmp/ (arquivos temporários)
```

## Gerenciamento de Dispositivos

### Drivers

Cada dispositivo (impressora, webcam, placa de rede) precisa de um **driver** — um programa que sabe como comunicar com esse hardware específico.

### Plug and Play

SOs modernos detectam e configuram novos dispositivos automaticamente.

## Proteção e Segurança

### Modos de Execução

- **Kernel mode**: Acesso total ao hardware
- **User mode**: Acesso restrito, apps não podem acessar hardware diretamente

Tentativas de acesso ilegal resultam em **segmentation fault**.

### Permissões

SOs multiusuário implementam sistemas de permissões:

```
drwxr-xr-x  arquivo.txt
│││││
││││└─ Outros: leitura
│││└── Outros: escrita
││└── Grupo: execução
│└── Dono: leitura
└── Dono: execução
```

## Exemplos de Sistemas Operacionais Modernos

### Desktop/Server
- **Linux**: Código aberto, domina servidores, base do Android
- **Windows**: Maior fatia de desktops
- **macOS**: Interface elegante, baseado em Unix

### Mobile
- **Android**: Baseado em Linux, código aberto
- **iOS**: Fechado, otimizado para hardware Apple

### Embedded/IoT
- **FreeRTOS**: Para dispositivos com recursos limitados
- **Zephyr**: IoT e sistemas embarcados

---

**Série: Como Computadores Funcionam**
1. [Introdução à Computação: História e Evolução]({{ site.baseurl }}/introducao-a-computacao-historia-e-evolucao)
2. [Sistemas Binários e Representação de Dados]({{ site.baseurl }}/sistemas-binarios-e-representacao-de-dados)
3. [Sistemas Operacionais: O que São e Como Funcionam]({{ site.baseurl }}/sistemas-operacionais-o-que-sao-e-como-funcionam) ← *você está aqui*

## Leia Mais

- Silberschatz, A., Galvin, P. B. & Gagne, G. *Sistemas Operacionais com Java*. 9ª Ed. Elsevier, 2018.
- Tanenbaum, A. S. *Sistemas Operacionais Modernos*. 4ª Ed. Pearson, 2016.
- Stallings, W. *Operating Systems: Internals and Design Principles*. 9ª Ed. Pearson, 2017.
- Love, R. *Linux Kernel Development*. 3ª Ed. Addison-Wesley, 2010.
