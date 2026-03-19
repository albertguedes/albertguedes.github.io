---
layout: post
title: "História da IA: Dos Inícios aos Dias Atuais"
description: "Uma jornada pela evolução da inteligência artificial, dos primeiros sonhos aos transformers."
date: 2022-08-25
---

A história da **inteligência artificial** é fascinante — cheia de revoluções, invernos de Funding, e breakthroughs que transformaram nosso mundo. Vamos explorar como chegamos até aqui.

## Os Primórdios (1940-1956)

### As Fundações

**1943**: McCulloch e Pitts publicam "A Logical Calculus of Ideas Immanent in Nervous Activity". Proposta o primeiro modelo matemático de neurônio artificial.

**1949**: Donald Hebb propões a "Hebbian learning" rule — neurônios que fire together, wire together.

**1950**: Alan Turing pubblica "Computing Machinery and Intelligence". Propõe o famoso **Teste de Turing** — se uma máquina pode conversar de forma indistinguível de um humano, ela é "inteligente".

### A Conferências de Dartmouth (1956)

Evento considerado o **nascimento oficial** da IA:

- John McCarthy (cunhou o termo "Artificial Intelligence")
- Marvin Minsky
- Claude Shannon
- Nathaniel Rochester

Participants acreditavam que:
> "Every aspect of learning or any other feature of intelligence can be so precisely described that a machine can be made to simulate it."

Optimismo que would lead to both great advances and great disappointments.

## Os Primeiros Sucessos (1956-1974)

### Programas que Impressionavam

**ELIZA (1966)**: Primeiro chatbot, criado por Joseph Weizenbaum no MIT. Simula um terapeuta rogeriano. Ainda impressiona pela "conversa".

** SHRDLU (1970)**: Programa de Terry Winograd que entendia comandos em linguagem natural sobre blocos em uma mesa virtual.

**Deep Blue antecessor**: Programas de xadrez que melhoravam progressivamente.

### Bots que Jogavam

- **Samuel's Checkers Player (1959)**: Primeiro programa de aprendizado autodidata
- **Mac Hack (1967)**: Primeiro programa a alcançar ranking de mestre em xadrez

### O Otimismo

Pesquisadores acreditavam que:
- Tradução automática em 5-10 anos
- Máquinas seriam campeãs de xadrez em 10 anos
- IA geral em 20 anos

## O Primeiro Inverno da IA (1974-1980)

### A Realidade Bate

Promessas não cumpridas:
- Tradução automática era muy笨拙a
- Redes neurais tinham limitações fundamentais (Minsky & Papert, 1969)
- Computadores eram lentos demais

### Cortes de Financiamento

- REDut de funding governamental, especialmente nos EUA
- Many researchers left the field
- Ceticismo geral sobre IA

## Renascimento (1980-1987)

### Sistemas Especialistas

IA encontra实用 application em **expert systems**:

```
SE temperatura > 30°C E umidade > 80%
ENTÃO diagnóstico = "condições ideais para mosquito"
```

Empresas investem heavily em sistemas baseados em regras para:
- Diagnóstico médico
- Configuração de computadores
- Prospecção mineral

### O Ciclo de IA

Japão announces o Projeto **Quinta Geração** (1982):
- Computadores para processamento de conhecimento
- Prolog como linguagem native
- 10-year, $400M projeto

Ocidente responde with increased funding.

## O Segundo Inverno (1987-1993)

### Sistemas Especialistas Falhavam

Problemas:
- Difficult to maintain and update
- Expensive to develop
- Não generalizavam well beyond narrow domains

### Mais Cortess

- O mercado de sistemas especialistas colapsa
- Funding para IA seca novamente
- Many AI companies go under

### A Rebirth

Pesquisadores começam a focar em:
- Probabilistic reasoning
- Neural networks (de volta!)
- Robotics

## Era Moderna: Aprendizado de Máquina (1990s-2010s)

### Statistical Learning

IA abandona regras explícitas e embrace statistical learning:

- Hidden Markov Models para speech recognition
- Support Vector Machines
- Probabilistic models

###连胜 de marcos

**1997**: **Deep Blue** beats Kasparov at chess. Primeiro programa a vencer campeão mundial.

**2002**: **Google** launches, massive data drives ML advances.

**2006**: **Netflix Prize** shows power of collaborative filtering.

**2011**: **Watson** wins Jeopardy! against champions.

## Revolução do Deep Learning (2012-presente)

### ImageNet Moment

**2012**: AlexNet wins ImageNet competition with deep CNN. Error rate drops from 26% to 15%.

O artigo mais influente em IA da história? Many think so.

### Por que Agora?

Três factores convergiram:

1. **Dados**: ImageNet, internet, sensors
2. **Computação**: GPUs, TPUs
3. **Algoritmos**: Better architectures, dropout, ReLU

### Marcos Recentes

| Ano | Marco |
|-----|-------|
| 2014 | GANs (Goodfellow) - geração de imagens |
| 2014 | Generative adversarial networks |
| 2015 | ResNet - redes muito profundas |
| 2016 | AlphaGo beats Lee Sedol (Go) |
| 2017 | Attention Is All You Need (Transformers) |
| 2018 | BERT (NLP) |
| 2019 | GPT-3 (175B parameters) |
| 2020 | AlphaFold (proteína folding) |
| 2022 | ChatGPT |
| 2023 | GPT-4, LLaMA, open models |
| 2024+ | Multimodal, reasoning, agents |

## Onde Estamos Agora

### Estado da Arte

- **LLMs**: Capazes de texto, código, raciocínio
- **Visão**: Detecção, geração, editing
- **Multimodalidade**: Integração texto-imagem-áudio
- **Agents**: Capazes de usar tools e executar tarefas

### Preocupações

- **Alignment**: Garantir que IA fazer o que queremos
- **Concentração**: who controls these powerful models?
- **Ambiente**: Treinar modelos grandes consome enorme energia
- **Emprego**: Automação de tasks knowledge work

## Lições da História

1. **Oscilação entre otimismo e ceticismo**: Expectativas realista são importantes
2. **Dados > Regras**: Statistical learning superou symbolic AI
3. **Escala funciona**: Mais dados + mais computação = better results
4. **Hugh, notIncremental**: Breakthroughs change the field dramatically
5. **O futuro é incerto**: Predictions consistently wrong

---

**Série: IA Fundamentos**
1. [O que é Inteligência Artificial?]({{ site.baseurl }}/o-que-e-inteligencia-artificial)
2. [História da IA: Dos Inícios aos Dias Atuais]({{ site.baseurl }}/historia-da-ia-dos-inicios-aos-dias-atuais) ← *você está aqui*
3. [Algoritmos de Busca: DFS, BFS e A*]({{ site.baseurl }}/algoritmos-de-busca-dfs-bfs-e-a)

## Leia Mais

- Russell, S. & Norvig, P. *Inteligência Artificial*. 3ª Ed. Elsevier, 2013.
- McCorduck, P. *Machines Who Think*. A K Peters, 2004.
- Crevier, D. *AI: The Tumultuous History*. Basic Books, 1993.
- LeCun, Y., Bengio, Y. & Hinton, G. "Deep Learning". *Nature*, 2015.
