---
layout: post
title: "Sistemas Binários e Representação de Dados"
description: "Como computadores armazenam e processam informações usando apenas 0s e 1s."
date: 2013-05-15
---

Os computadores são máquinas extraordinariamente complexas por dentro, mas sua linguagem fundamental é surpreendentemente simples: **binária**. Apenas dois dígitos — 0 e 1 — são suficientes para representar qualquer informação que um computador processa, desde textos simples até vídeos em alta definição.

## O Sistema Binário

Nosso sistema decimal usa 10 dígitos (0-9) e é **posicional** — o valor de cada dígito depende de sua posição (unidades, dezenas, centenas, etc.). O sistema binário funciona igual, mas com apenas 2 dígitos.

### Decimal vs Binário

| Decimal | Binário |
|---------|---------|
| 0 | 0 |
| 1 | 1 |
| 2 | 10 |
| 3 | 11 |
| 4 | 100 |
| 5 | 101 |
| 10 | 1010 |

### Convertendo Decimal para Binário

Para converter um número decimal em binário, dividimos sucessivamente por 2 e anotamos os restos:

```
13 ÷ 2 = 6 resto 1
6 ÷ 2 = 3 resto 0
3 ÷ 2 = 1 resto 1
1 ÷ 2 = 0 resto 1
Lendo de baixo para cima: 1101
```

### Convertendo Binário para Decimal

Multiplicamos cada dígito por 2 elevado à sua posição (contada da direita, começando em 0):

```
1×2³ + 1×2² + 0×2¹ + 1×2⁰
= 8 + 4 + 0 + 1
= 13
```

## Bits e Bytes

- **Bit** (binary digit): A menor unidade de dados — pode ser 0 ou 1
- **Byte**: Grupo de 8 bits. Representa 256 valores possíveis (2⁸)

Prefixos comuns:
- KB (Quilobyte): ~1.000 bytes (na verdade 1024)
- MB (Megabyte): ~1 milhão de bytes
- GB (Gigabyte): ~1 bilhão de bytes
- TB (Terabyte): ~1 trilhão de bytes

## Representação de Texto: ASCII e Unicode

### ASCII
O **American Standard Code for Information Interchange** usa 7 bits (128 caracteres) para representar texto em inglês. Inclui:
- Letras maiúsculas e minúsculas (A-Z, a-z)
- Dígitos (0-9)
- Pontuação e símbolos
- Caracteres de controle

### Unicode
Para acomodar todos os idiomas do mundo, surgiu o **Unicode**, que pode usar até 32 bits por caractere. As implementações mais comuns:

- **UTF-8**: Caracteres de tamanho variável (1-4 bytes), compatível com ASCII
- **UTF-16**: Caracteres de 2 ou 4 bytes
- **UTF-32**: Caracteres fixos de 4 bytes

## Representação de Números

### Inteiros
Números inteiros são armazenados diretamente em binário. Sistemas modernos usam 32 ou 64 bits.

### Números Negativos
O método mais comum é o **complemento de dois**, que permite representar números negativos e fazer aritmética de forma eficiente.

### Números Reais (Ponto Flutuante)
Para números com parte decimal, usa-se o padrão **IEEE 754**:
- 1 bit para sinal
- Bits para expoente
- Bits para mantissa (parte fracionária)

Exemplo: O float 3.14 é aproximadamente 3.14 em decimal.

## Representação de Imagens

### Mapa de Bits (Bitmap)
Cada pixel é armazenado como valores de cor. Uma imagem 1920×1080 tem mais de 2 milhões de pixels.

### Formatos Comuns
- **PNG**: Sem perda, bom para gráficos
- **JPEG**: Com perda, eficiente para fotos
- **GIF**: Para animações simples

## Representação de Áudio

Áudio digital é amostrado — o som é medido milhares de vezes por segundo:
- **CD Quality**: 44.100 samples/segundo, 16 bits/sample, estéreo
- **MP3/AAC**: Compressão com perda perceptiva
- **FLAC**: Compressão sem perda

## Lógica Binária e Portas Lógicas

Portas lógicas são componentes eletrônicos que implementam operações booleanas:

- **AND**: Saída 1 apenas se todas as entradas são 1
- **OR**: Saída 1 se pelo menos uma entrada é 1
- **NOT**: Inverte o sinal (0→1, 1→0)
- **XOR**: Saída 1 se as entradas são diferentes

Combinando dessas portas, construímos circuitos que realizam cálculos complexos — somadores, multiplicadores, processadores inteiros.

---

**Série: Como Computadores Funcionam**
1. [Introdução à Computação: História e Evolução]({{ site.baseurl }}/introducao-a-computacao-historia-e-evolucao)
2. [Sistemas Binários e Representação de Dados]({{ site.baseurl }}/sistemas-binarios-e-representacao-de-dados) ← *você está aqui*
3. [Sistemas Operacionais: O que São e Como Funcionam]({{ site.baseurl }}/sistemas-operacionais-o-que-sao-e-como-funcionam)

## Leia Mais

- Tanenbaum, A. S. & Austin, T. *Organização Estruturada de Computadores*. 6ª Ed. Prentice Hall, 2012.
- Null, L. & Lobur, J. *Princípios de Hardware e Arquitetura de Computadores*. 4ª Ed. Bookman, 2015.
- Stallings, W. *Computer Organization and Architecture*. 10ª Ed. Pearson, 2015.
- IEEE 754: Standard for Floating-Point Arithmetic.
