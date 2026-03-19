---
layout: post
title: "Redes Neurais Artificiais: Conceitos"
description: "Entenda como as redes neurais funcionam, inspiradas no cérebro humano."
date: 2017-02-25
---

As **redes neurais artificiais** são modelos computacionais inspirados na estrutura e funcionamento do cérebro biológico. São a base do **deep learning** que revolucionou a inteligência artificial na última década, powering everything from voice assistants to medical diagnosis.

## O Cérebro Biológico como Inspiração

### Neurônios Reais

O cérebro humano contém aproximadamente 86 bilhões de neurônios, cada um conectado a milhares de outros através de **sinapses**. Um neurônio:

1. Recebe sinais elétricos de outros neurônios via dendritos
2. Integra esses sinais no corpo celular
3. Se o sinal combinado exceed um limiar, transmite um pulso elétrico pelo axônio
4. O sinal é passed para outros neurônios nas sinapses

### A Analogia Artificial

Redes neurais artificiais adaptam esses conceitos:

| Cérebro | Rede Neural Artificial |
|---------|----------------------|
| Neurônio | Nó ou unidade |
| Sinapse | Peso sináptico |
| Dendritos | Entradas |
| Axônio | Saída |
| Aprendizagem | Ajuste de pesos |

## Estrutura de uma Rede Neural

### Neurônio Artificial

```
        Entradas          Peso
           │             │
           ▼             ▼
      ┌─────────┐
      │  Σ (soma) │──→ Função de Ativação ─→ Saída
      └─────────┘
           ▲
           │
        Limiar (bias)
```

1. Cada entrada é multiplicada por um peso
2. O neurônio soma todas as entradas ponderadas
3. Adiciona um viés (bias)
4. Aplica uma **função de ativação**
5. Produz uma saída

### Funções de Ativação

- **Step**: 0 ou 1 (como neurônio biológico idealizado)
- **Sigmoid**: Suave, valores entre 0 e 1
- **ReLU**: max(0, x) — mais popular em deep learning
- **Tanh**: Valores entre -1 e 1

### Arquitetura em Camadas

```
Entrada (Input Layer)          Oculta (Hidden)         Saída (Output)
     │                              │                       │
  [x1] ───────┐                  ┌───▼───┐              [y1]
  [x2] ───────┼────────┐      ┌──▶│ Neur │──┐         [y2]
  [x3] ───────┼────────┼──┐  │   └───────┘  │──┐     [y3]
              │        │  │  │              │  │
              │        │  │  │   . . .      │  │
              │        │  └──▶│ Neur │◀─────┘  │
              │        │     └──┬───┘          │
              │        │        │              │
              │        │        ▼              │
              │        │    ┌───────┐          │
              │        └────▶│ Neur │◀─────────┘
              │             └──┬───┘
              │                │
              ▼                ▼
          Pesos w          Pesos w
```

- **Camada de entrada**: Recebe os dados (features)
- **Camadas ocultas**: Processam e transformam dados
- **Camada de saída**: Produz o resultado final

## Como uma Rede Aprende?

### O Algoritmo de Backpropagation

A rede aprende ajustando os pesos através de **backpropagation**:

1. **Forward pass**: Dados fluem da entrada para a saída
2. **Calcular erro**: Compare saída predicted com saída desejada
3. **Backward pass**: Erro propaga de volta, layer por layer
4. **Ajustar pesos**: Use gradient descent para minimizar erro

### Gradient Descent

Para encontrar o mínimo da função de erro, a rede:
1. Calcula a derivatives parcial do erro em relação a cada peso
2. Ajusta os pesos na direção que reduce o erro
3. Repete até convergence

### Taxa de Aprendizado

控制 quanto cada peso é ajustado:
- Taxa muito alta: rede não converge (oscila)
- Taxa muito baixa: aprendizado muito lento

## Tipos de Redes Neurais

### Perceptron (1957)

A rede neural mais simples — um único neurônio. Só pode resolver problemas linearmente separáveis.

### Multi-Layer Perceptron (MLP)

Redes com múltiplas camadas ocultas:
- Pode resolver problemas não-lineares
- Universal function approximator

### Redes Neurais Convolucionais (CNN)

Especializadas em processar imagens:
- Usam filtros que deslizam sobre a imagem
- Excelentes para visão computacional

### Redes Neurais Recorrentes (RNN)

Especializadas em dados sequenciais:
- Tienen conexões que voltam no tempo
- Úteis para texto, séries temporais

### Transformers

Arquitetura state-of-the-art para NLP:
- Base de modelos como GPT, BERT
- Self-attention mechanism

## Aplicações

### Visão Computacional
- Reconhecimento facial
- Diagnóstico por imagem
- Carros autônomos

### Processamento de Linguagem Natural
- Tradução automática
- Chatbots
- Análise de sentimentos

### Games e Robótica
- AlphaGo
- Agentes que aprendem a jogar

### Medicina
- Deteção de câncer
- Descoberta de remédios

## Limitações e Desafios

### Necessidade de Dados

Redes profundas precisam de grandes quantidades de dados rotulados.

### Overfitting

Risco de memorizar os dados de treino em vez de generalize.

### Interpretabilidade

Difícil entender por que a rede fez uma determinada prediction.

### Custos Computacionais

Treinar grandes modelos requer muito poder de processamento e energia.

---

**Série: Redes Neurais**
1. [Redes Neurais Artificiais: Conceitos]({{ site.baseurl }}/redes-neurais-artificiais-conceitos) ← *você está aqui*
2. [Deep Learning: Uma Introdução]({{ site.baseurl }}/deep-learning-uma-introducao)
3. [Processamento de Linguagem Natural]({{ site.baseurl }}/processamento-de-linguagem-natural)
4. [Visão Computacional: Como Máquinas Veem]({{ site.baseurl }}/visao-computacional-como-maquinas-veem)

## Leia Mais

- Goodfellow, I., Bengio, Y. & Courville, A. *Deep Learning*. MIT Press, 2016.
- Chollet, F. *Deep Learning with Python*. Manning, 2017.
- Nielsen, M. *Neural Networks and Deep Learning*. Determination Press, 2015.
- Russell, S. & Norvig, P. *Inteligência Artificial*. 3ª Ed. Elsevier, 2013.
