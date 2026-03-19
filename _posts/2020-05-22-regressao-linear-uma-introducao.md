---
layout: post
title: "Regressão Linear: Uma Introdução"
description: "Aprenda o algoritmo mais fundamental e interpretável do machine learning."
date: 2020-05-22
---

**Regressão linear** é o algoritmo de machine learning mais antigo, mais simples e mais interpretável. Apesar de sua simplicidade, é amplamente usado em problemas reais e serve como foundation para compreender modelos mais complexos.

## O que é Regressão Linear?

Regressão linear encontra a **relação linear** entre variáveis de entrada (features) e uma variável de saída contínua.

**Exemplos:**
- Predizer preço de casas (entrada: tamanho, localização, quartos)
- Estimar vendas futuras (entrada: gasto em propaganda, época do ano)
- Prever consumo de energia (entrada: temperatura, dia da semana)

## O Modelo Simples

### Com Uma Variável (Simples)

```
y = mx + b
```

Onde:
- **y**: variável dependente (o que queremos prever)
- **x**: variável independente (feature)
- **m**: coeficiente angular (slope)
- **b**: intercept (onde a linha cruza o eixo y)

### Com Múltiplas Variáveis (Múltipla)

```
y = β₀ + β₁x₁ + β₂x₂ + ... + βₙxₙ + ε
```

Onde:
- **β₀**: intercept (coeficiente do bias)
- **β₁, β₂, ..., βₙ**: coeficientes de cada feature
- **ε**: erro aleatório (ruído não explicável)

## Encontrando os Melhores Coeficientes

### Método dos Mínimos Quadrados

Aims to minimize the **squared residuals** (diferença entre valor real e previsto):

```
Minimizar: Σ(yᵢ - ŷᵢ)²

Onde ŷᵢ = β₀ + β₁x₁ᵢ + ...
```

Por que quadrado? Porque:
- Penaliza erros grandes mais que pequenos
- Erros positivos e negativos não se cancelam
- Matematicamente conveniente (diferenciável)

### Solução Analítica (Closed-Form)

Para regressão linear, existe solução direta:

```
β = (XᵀX)⁻¹Xᵀy
```

Onde:
- **X**: matrix de features (com coluna de 1s para bias)
- **y**: vetor de valores target
- **β**: vetor de coeficientes

Funciona bem para datasets pequenos/ médios. Para grandes, preferível iterative methods.

## Métricas de Avaliação

### R² (Coeficiente de Determinação)

Mede a proporção da variância em y explicada pelo modelo:

```
R² = 1 - (SS_res / SS_tot)

SS_res = Σ(yᵢ - ŷᵢ)²  (soma dos quadrados dos resíduos)
SS_tot = Σ(yᵢ - ȳ)²     (variância total)
```

- **R² = 1**: Perfeito (modelo explica tudo)
- **R² = 0**: Modelo não é melhor que simplesmente predictar a média
- **R² < 0**: Pior que baseline (problema!)

### RMSE (Root Mean Squared Error)

```
RMSE = √(Σ(yᵢ - ŷᵢ)² / n)
```

Mesma unidade da variável y. Intuitivo de entender.

### MAE (Mean Absolute Error)

```
MAE = Σ|yᵢ - ŷᵢ| / n
```

Menos sensível a outliers que RMSE.

## Pressupostos do Modelo

Regressão linear assume:

### 1. Linearidade
Relação entre X e y é linear. Se não for, pode transformar features (x², log(x), etc.)

### 2. Independência dos Erros
Erros não estão correlacionados entre si.

### 3. Homocedasticidade
Variância dos erros é constante. Se não, usamos regressão robusta.

### 4. Normalidade dos Erros
Erros seguem distribuição normal (importante para inferência, não tanto para predição).

### 5. Sem multicolinearidade
Features não são perfeitamente correlacionados entre si.

## Regularização

Para evitar overfitting quando há muitas features:

### Ridge (L2)

```
Minimizar: Σ(yᵢ - ŷᵢ)² + λΣβⱼ²
```

Penaliza large coefficients,倾向于 distributed weight among all features.

### Lasso (L1)

```
Minimizar: Σ(yᵢ - ŷᵢ)² + λΣ|βⱼ|
```

Penaliza the sum of absolute coefficients,倾向于 zeroing out some features (feature selection).

### Elastic Net

Combinação de Ridge e Lasso.

## Quando Usar Regressão Linear?

### Prós

- Simples e interpretável
- Rápido de treinar
- Boa baseline
- Funciona bem quando relação é realmente linear

### Contras

- Não captura relações não-lineares
- Sensível a outliers
- Pode underfit em problemas complexos

### Quando Funciona Bem

- Baseline simples
- Problemas onde interpretability é crucial
- Dados com relação linear conhecida
- Quando você precisa explain to stakeholders

## Implementação Básica

```python
import numpy as np
from sklearn.linear_model import LinearRegression

# Dados
X = np.array([[1], [2], [3], [4], [5]])
y = np.array([2.1, 4.2, 6.1, 7.9, 10.2])

# Criar e treinar modelo
modelo = LinearRegression()
modelo.fit(X, y)

# Predizer
X_novo = np.array([[6]])
y_predito = modelo.predict(X_novo)

# Coeficientes
print(f"Intercepto: {modelo.intercept_}")  # ~0.04
print(f"Coeficiente: {modelo.coef_[0]}")    # ~2.04
```

## Extensões

### Regressão Polinomial

```
y = β₀ + β₁x + β₂x² + β₃x³ + ...
```

Captura relações não-lineares mantendo o framework linear.

### Regressão Logística

Para classificação (y binário):

```
P(y=1) = sigmoid(β₀ + β₁x₁ + ...)
```

Outputs probabilities between 0 and 1.

---

**Série: ML Básico**
1. [O que é Machine Learning?]({{ site.baseurl }}/o-que-e-machine-learning)
2. [Aprendizado Supervisionado vs Não-Supervisionado]({{ site.baseurl }}/aprendizado-supervisionado-vs-nao-supervisionado)
3. [Regressão Linear: Uma Introdução]({{ site.baseurl }}/regressao-linear-uma-introducao) ← *você está aqui*
4. [Classificação: Como Máquinas Categorizam]({{ site.baseurl }}/classificacao-como-maquinas-categorizam)

## Leia Mais

- James, G. et al. *An Introduction to Statistical Learning*. 2ª Ed. Springer, 2021.
- Hastie, T., Tibshirani, R. & Friedman, J. *The Elements of Statistical Learning*. 2ª Ed. Springer, 2009.
- Montgomery, D. C., Peck, E. A. & Vining, G. G. *Introduction to Linear Regression Analysis*. 5ª Ed. Wiley, 2012.
