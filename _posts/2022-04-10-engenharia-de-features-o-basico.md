---
layout: post
title: "Engenharia de Features: O Básico"
description: "Aprenda a arte de transformar dados crus em features que melhoram modelos de ML."
date: 2022-04-10
---

Na prática, o sucesso de um modelo de machine learning depende enormemente de quão bem os **dados de entrada** são preparados. **Engenharia de features** é o processo de transformar dados crus em representações que ajudam modelos a aprender patterns mais effectively.

## Por que Feature Engineering é Importante?

### Ditado Popular

> "Garbage in, garbage out"

Se features são poor, mesmo the most sophisticated algorithms will struggle.

### O que uma Boa Feature Deve Ser

- **Informativa**: Correlacionada com target
- **Independente**: Não redundante com outras features
- **Numérica ou Convertível**: Modelos precisam numbers

### Impacto

Feature engineering bem feita pode:
- Improve model accuracy dramatically
- Reduce overfitting
- Make models more interpretable
- Reduce training time

## Técnicas Básicas

### 1. Normalização/Escalonamento

Features em diferentes escalas podem perjudicar modelos sensíveis:

**Min-Max Scaling:**
```
x_scaled = (x - x_min) / (x_max - x_min)
```

Resulta em valores entre 0 e 1.

**Standardization (Z-score):**
```
z = (x - μ) / σ
```

Resulta em média 0 e desvio padrão 1.

**Quando usar cada:**
- Algoritmos sensíveis a escala: SVM, KNN, Neural Networks
- Árvores de decisão: não necessário

### 2. Transformação de Variáveis

Adicionar nonlinearities sem mudar o modelo:

```python
# Polinomial
x² = x ** 2
x³ = x ** 3

# Logarítmica (para dados skewados)
log_x = np.log(x + 1)

# Raiz quadrada
sqrt_x = np.sqrt(x)
```

### 3. Encoding de Variáveis Categóricas

Modelos precisam números:

**Label Encoding:**
```
Fruta: Maçã → 0, Banana → 1, Laranja → 2
```

Só faz sentido se há ordenação natural.

**One-Hot Encoding:**
```
Maçã: [1, 0, 0]
Banana: [0, 1, 0]
Laranja: [0, 0, 1]
```

Cria uma coluna por categoria. Usar quando não há orden.

**Target Encoding:**
```
Média do target por categoria
```
Use carefully to avoid leakage.

## Feature Selection

Nem todas as features são úteis. Selection helps:

### 3.1 Filter Methods

Baseados em estatísticas:

- **Correlação**: Remove features altamente correlacionadas entre si
- **Chi-square**: Para variáveis categóricas
- **Information gain**: Baseado em entropia

### 3.2 Wrapper Methods

Avaliam subsets de features com o modelo:

- **Forward selection**: Adiciona features uma a uma
- **Backward elimination**: Remove features uma a uma
- **Recursive Feature Elimination (RFE)**: Iterativamente remove as menos importantes

### 3.3 Embedded Methods

Feature selection occurs during training:

- **L1 regularization (Lasso)**: Zera coeficientes
- **Feature importance em Random Forest**

## Feature Creation

Criar novas features combinando ou transformando existentes:

### Exemplo: Dados de Imóveis

```python
# Features originais
df['area'] = ...
df['quartos'] = ...
df['banheiros'] = ...

# Features criadas
df['area_por_quarto'] = df['area'] / df['quartos']
df['banheiros_por_quarto'] = df['banheiros'] / df['quartos']
df['log_area'] = np.log(df['area'])
df['area_2'] = df['area'] ** 2
```

### Exemplo: Dados de Tempo

```python
df['day_of_week'] = df['date'].dt.dayofweek
df['month'] = df['date'].dt.month
df['is_weekend'] = df['day_of_week'].isin([5, 6]).astype(int)
df['quarter'] = df['date'].dt.quarter
```

## Feature Engineering para Texto

### Bag of Words

```python
from sklearn.feature_extraction.text import CountVectorizer

vectorizer = CountVectorizer()
X = vectorizer.fit_transform(corpus)
```

### TF-IDF

```
TF-IDF = Frequência do termo × Inverse Document Frequency
```

Dá peso a termos importantes, não apenas frequentes.

```python
from sklearn.feature_extraction.text import TfidfVectorizer

vectorizer = TfidfVectorizer()
X = vectorizer.fit_transform(corpus)
```

## Feature Engineering para Séries Temporais

### Lag Features

```python
df['vendas_lag_1'] = df['vendas'].shift(1)
df['vendas_lag_7'] = df['vendas'].shift(7)  # 1 semana atrás
df['vendas_lag_30'] = df['vendas'].shift(30)  # 1 mês atrás
```

### Rolling Statistics

```python
df['media_movel_7'] = df['vendas'].rolling(7).mean()
df['desvio_movel_7'] = df['vendas'].rolling(7).std()
```

### Date Features

```python
df['day_of_month'] = date.dt.day
df['week_of_year'] = date.dt.isocalendar().week
df['is_month_start'] = date.dt.is_month_start
```

## Lidando com Missing Values

Dados faltantes podem destruir seu modelo:

### Detectar

```python
df.isnull().sum()
df.isnull().mean()  # percentual
```

### Estratégias

1. **Remover linhas**: Só se poucos missing
2. **Remover colunas**: Se muitos missing
3. **Preencher (Imputation)**:
   - Média/mediana (numéricas)
   - Moda (categóricas)
   - Forward/backward fill (temporais)
   - KNN imputation
   - Model-based imputation

## Armadilhas Comuns

### Data Leakage

Quando informação do future "vaza" para training:

```python
# ❌ ERRADO - causa leakage
df['target_lag_1'] = df['target'].shift(-1)  # Look-ahead!

# ✅ CORRETO
df['target_lag_1'] = df['target'].shift(1)  # Only past info
```

### Overfitting a Features

Mais features ≠ melhor. Features irrelevantes or noisy can harm.

### Ignorar Distribuição

Transformações podem mudar completamente o comportamento.

---

**Série: ML Prático**
1. [Engenharia de Features: O Básico]({{ site.baseurl }}/engenharia-de-features-o-basico) ← *você está aqui*
2. [Árvores de Decisão e Random Forests]({{ site.baseurl }}/arvores-de-decisao-e-random-forests)
3. [Redes Neurais Artificiais: Conceitos]({{ site.baseurl }}/redes-neurais-artificiais-conceitos)

## Leia Mais

- Zheng, A. & Casari, A. *Feature Engineering for Machine Learning*. O'Reilly, 2018.
- Molnar, C. *Interpretable Machine Learning*. 2023.
- James, G. et al. *An Introduction to Statistical Learning*. 2ª Ed. Springer, 2021.
