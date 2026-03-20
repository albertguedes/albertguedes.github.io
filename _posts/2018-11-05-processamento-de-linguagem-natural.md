---
layout: post
title: "Processamento de Linguagem Natural"
description: "Entenda como máquinas entendem e geram linguagem humana."
date: 2018-11-05
---

Quando você pergunta ao seu celular "Como está o tempo amanhã?", ou usa o Google Translator para entender um texto em outro idioma, está interagindo com sistemas de **Processamento de Linguagem Natural (PLN)** — um dos campos mais fascinantes e desafiadores da inteligência artificial.

## O que é PLN?

**Processamento de Linguagem Natural** é a área da IA focada em fazer computadores entenderem, interpretarem e gerarem linguagem humana. A desafios é enorme: linguagem é ambígua, dependente de contexto, e evolui constantemente.

### NLP vs NLU vs NLG

- **NLP**: O campo geral (Processamento)
- **NLU**: Entendimento — extrair significado
- **NLG**: Geração — criar texto

## Por que é Difícil?

### Ambiguidade

**Lexical**: Uma palavra com múltiplos significados
```
"Banco" pode ser instituição financeira ou assento
```

**Sintática**: Múltiplas formas de analisar a estrutura
```
"Vi o homem com binóculos" — Quem tem os binóculos?
```

**Semântica**: Significado que depende do contexto
```
"Fome" literal vs "estou com fome de música"
```

### Variação

- Diferentes idiomas têm diferentes estruturas
- Sotaques e dialetos
- Linguagem informal, gírias, emojis
- Erros de digitação e gramática

## Abordagens Históricas

### PLN Clássico (1950s-1990s)

Baseado em **regras explícitas** e análise linguística formal.

**Gramáticas formais**: Regras de estrutura frasal
**Dicionários**: Mapeamentos de significado
**Regras de tradução**: Padrões do tipo IFTTT

Problema: Não escala, não lida bem com ambiguidade.

### PLN Estatístico (1990s-2010s)

Modelos aprendem padrões estatisticamente de grandes corpora.

**n-grams**: Sequências de N palavras como features
**HMMs**: Para tagging part-of-speech
**IBM models**: Para tradução automática

Melhor que regras, mas ainda limitado em capturar significado profundo.

### PLN Neural / Deep Learning (2013-presente)

Redes neurais aprendem representações ricas de texto.

**Word embeddings**: Palavras como vectors num espaço semântico
**RNNs/LSTMs**: Para sequências
**Transformers**: Arquitetura atual de ponta

## Técnicas Fundamentais

### Tokenização

Dividir texto em unidades menores (tokens):

```
"Olá, como vai você?" 
→ ["Olá", ",", "como", "vai", "você", "?"]
```

Para palavras compostas ou sub-palavras (Byte Pair Encoding).

### Embeddings de Palavras

Palavras representadas como vectors em espaço vetorial:

```
king - man + woman ≈ queen
Paris - France + Italy ≈ Rome
```

Propriedade: Palavras com significados similares estão próximas no espaço.

**Modelos populares**: Word2Vec, GloVe, FastText

### Atención

Mecanismo onde cada posição pode "atender" a todas as outras:

```
Cada palavra pode olhar para todas as outras
e aprender qual contexto é mais relevante
```

Base dos Transformers e revolucionou NLP.

## Tarefas Principais

### Classificação de Texto

Atribuir categorias a documentos:

- Spam detection (spam/não-spam)
- Análise de sentimentos (positivo/negativo/neutro)
- Detecção de idioma

### Extração de Entidades (NER)

Identificar e classificar entidades no texto:

```
[Albert] [pessoa] fundou [empresa] em [São Paulo] [local]
```

### Análise de Dependência

Identificar relações gramaticais entre palavras:

```
        fundou (verbo)
           │
     ┌─────┴─────┐
   Albert    empresa
   (sujeito)   (objeto direto)
```

### Tradução Automática

Converter texto de um idioma para outro:

```
The cat sat on the mat
    ↓
O gato sentou no tapete
```

## Aplicações do Mundo Real

### Assistentes Virtuais

Siri, Alexa, Google Assistant — entendem comandos de voz e respondem apropriadamente.

### Tradução Automática

Google Translate, DeepL — tradução entre dezenas de idiomas.

### Chatbots

Atendimento automático, serviço ao cliente, bots de terapia.

### Sumarização

Extrair ou gerar resumos de documentos longos.

### Análise de Sentimentos

Monitorar opinião pública sobre marcas, produtos, políticas.

## Modelos Atuais

### BERT (2018)

"Bidirectional Encoder Representations from Transformers"

- Treina predizendo palavras mascaradas em ambas direções
- Gera contextual embeddings
- Revolucionou tarefas de entendimento

### GPT (2018-presente)

"Generative Pre-trained Transformer"

- Autoregressive: prediz próxima palavra
- Treino em bilhões de textos
- Capacidade emergente de raciocínio

### T5, BART, and others

 diferentes objetivos de pré-treino, diferentes pontos fortes.

## Limitações Atuais

### Falta de Raciocínio Profundo

Modelos são bons em reconhecimento de padrões, mas raciocínio multicross permanece desafiador.

### Necessidade de Bases Conhecidas

Não entende o mundo como humanos — falta senso comum.

### Alucinações

LLMs podem gerar informações factualmente incorretas com confiança.

### Vieses

Modelos absorvem e amplificam vieses presentes nos dados de treinamento.

## O Futuro do NLP

### Tendências

- **Multimodalidade**: Integrando texto, imagem, áudio
- **Eficiência**: Modelos menores e mais rápidos
- **Interpretabilidade**: Entender como modelos chegam a respostas
- **Fine-tuning especializado**: Adaptação a domínios específicos

### Desafios

- Cross-lingual understanding
- Low-resource languages
- Faithfulness to sources
- Measuring comprehension

---

**Série: Redes Neurais**
1. [Redes Neurais Artificiais: Conceitos]({{ site.baseurl }}/redes-neurais-artificiais-conceitos)
2. [Deep Learning: Uma Introdução]({{ site.baseurl }}/deep-learning-uma-introducao)
3. [Processamento de Linguagem Natural]({{ site.baseurl }}/processamento-de-linguagem-natural) ← *você está aqui*
4. [Visão Computacional: Como Máquinas Veem]({{ site.baseurl }}/visao-computacional-como-maquinas-veem)

## Leia Mais

- Jurafsky, D. & Martin, J. H. *Speech and Language Processing*. 3rd Ed. draft, 2023.
- Goldberg, Y. "A Primer on Neural Network Models for Natural Language Processing". *JAIR*, 2016.
- Vaswani, A. et al. "Attention Is All You Need". *NeurIPS*, 2017.
- Devlin, J. et al. "BERT". *NAACL*, 2019.
