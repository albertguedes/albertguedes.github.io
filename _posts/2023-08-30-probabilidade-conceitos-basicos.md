---
layout: post
title: "Probabilidade: Conceitos Básicos"
description: "Uma introdução aos fundamentos da probabilidade, essencial para estatística e machine learning."
date: 2023-08-30
---

**Probabilidade** é a linguagem da incerteza. Está presente em tudo — do tempo que vai fazer amanhã ao risco de um investimento. Para machine learning, estatística e ciência de dados, é fundamental.

## O que é Probabilidade?

Probabilidade mede **quão provável** é um evento ocorrer.

Valores entre 0 e 1:
- **P = 0**: Evento impossível
- **P = 1**: Evento certo
- **0 < P < 1**: Incerteza

### Frequência vs Subjetiva

**Frequência**: Baseada em repetições históricas
> "Se jogar essa moeda 1000 vezes, ~500 serão cara"

**Subjetiva**: Grau de crença pessoal
> "Acho que há 70% de chance do Brasil ganhar"

## Conceitos Fundamentais

### Experimento Aleatório

Processo com resultado incerto:

- Jogar moeda
- Rolar dado
- Escolher pessoa aleatória

### Espaço Amostral (Ω)

Conjunto de todos os resultados possíveis:

```
Moeda: Ω = {cara, coroa}
Dado: Ω = {1, 2, 3, 4, 5, 6}
```

### Evento

Subconjunto do espaço amostral:

```
E = {2, 4, 6} (números pares ao jogar dado)
```

## Regras Básicas

### 1. Probabilidade de um Evento

```
P(E) = número de outcomes favoráveis / número de outcomes possíveis
```

**Exemplo**: Qual a probabilidade de sair número 3?

```
P(3) = 1/6 ≈ 0.167
```

### 2. Probabilidade Complementar

```
P(não E) = 1 - P(E)
```

**Exemplo**: P(não 3) = 1 - 1/6 = 5/6

### 3. Adição (União)

**Eventos Mutuamente Exclusivos** (não podem ocorrer juntos):

```
P(A ou B) = P(A) + P(B)
```

**Exemplo**: P(1 ou 2) = P(1) + P(2) = 1/6 + 1/6 = 2/6

**Eventos Não-Exclusivos**:

```
P(A ou B) = P(A) + P(B) - P(A e B)
```

### 4. Multiplicação (Interseção)

**Eventos Independentes** (um não afeta o outro):

```
P(A e B) = P(A) × P(B)
```

**Exemplo**: Duas moedas, probabilidade de duas caras?

```
P(cara e cara) = 0.5 × 0.5 = 0.25
```

**Eventos Dependentes** (condicional):

```
P(A e B) = P(A) × P(B|A)
```

## Probabilidade Condicional

**P(B|A)**: Probabilidade de B dado que A ocorreu:

```
P(B|A) = P(A e B) / P(A)
```

**Exemplo**: Urna com 3 bolas vermelhas e 2 azuis. Sem reposição.

```
P(1ª azul) = 2/5
P(2ª azul | 1ª azul) = 1/4
```

## Teorema de Bayes

Um dos teoremas mais importantes:

```
P(A|B) = P(B|A) × P(A) / P(B)
```

### Intuição

Updates our belief based on new evidence.

### Exemplo Clássico

**Problema do teste de doença:**

- Doença afeta 1% da população
- Teste: 99% de sensibilidade (acerta quando doente)
- Teste: 95% de especificidade (acerta quando saudável)

Qual a P(doente | teste positivo)?
```
P(+) = P(+|D)P(D) + P(+|N)D)P(N)
     = 0.99 × 0.01 + 0.05 × 0.99
     ≈ 0.0594

P(D|+) = (0.99 × 0.01) / 0.0594 ≈ 0.167
```

Surpreendente! Mesmo com teste "bom", se você testa positivo, só ~17% de chance de ter a doença. É por isso que taxas base importam.

## Variáveis Aleatórias

### O que é?

Uma variável que assigna um número a cada outcome:

```
X = resultado de dado
X pode ser {1, 2, 3, 4, 5, 6}
```

### Discreta vs Contínua

**Discreta**: Valores contáveis (números inteiros)
**Contínua**: Valores em um intervalo (qualquer valor real)

### Distribuição de Probabilidade

Descreve como probabilidade se distribui sobre valores.

## Distribuições Importantes

### Discretas

**Uniforme**: Todos os resultados igualmente provável (dado honesto)

**Binomial**: Número de sucessos em N trials independentes:
```
P(X=k) = C(N,k) × p^k × (1-p)^(N-k)
```

**Poisson**: Eventos raros em um período/área:
```
P(X=k) = λ^k × e^(-λ) / k!
```

### Contínuas

**Normal (Gaussiana)**:
```
f(x) = (1/σ√(2π)) × e^(-(x-μ)²/2σ²)
```

Bell curve. CENTRAL LIMIT THEOREM: Somas de variáveis tendem à normal.

**Exponencial**: Tempo até próximo evento:
```
f(x) = λ × e^(-λx)
```

## Valor Esperado e Variância

### Valor Esperado (Média)

```
E[X] = Σ x × P(X=x)  (discreta)
E[X] = ∫ x × f(x) dx  (contínua)
```

É a média teórica de longo prazo.

### Variância

Mede dispersão em torno da média:

```
Var(X) = E[(X - μ)²]
```

### Propriedades

```
E[aX + b] = aE[X] + b
Var(aX + b) = a²Var(X)
```

## Aplicações em Machine Learning

### Classificação

- **Naive Bayes**: Usa probabilidade condicional para classificar
- **Logistic Regression**: Modela P(y|x) diretamente

### Avaliação

- **Cross-validation**: Estimar erro de generalização
- **Confidence intervals**: Quantificar incerteza
- **Probabilistic forecasting**: Predições como distributions

---

**Série: Matemática**
1. [Probabilidade: Conceitos Básicos]({{ site.baseurl }}/probabilidade-conceitos-basicos) ← *você está aqui*
2. [Estatística Descritiva: O Básico]({{ site.baseurl }}/estatistica-descritiva-o-basico)

## Leia Mais

- Ross, S. M. *Introduction to Probability and Statistics*. 4th Ed. Elsevier, 2012.
- Grinstead, C. M. & Snell, J. L. *Introduction to Probability*. 2nd Ed. AMS, 2006.
- DeGroot, M. H. & Schervish, M. J. *Probability and Statistics*. 4th Ed. Pearson, 2011.
- MIT OpenCourseWare. *Probability and Statistics*.
