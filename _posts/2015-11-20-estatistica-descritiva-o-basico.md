---
layout: post
title: "Estatística Descritiva: O Básico"
description: "Aprenda a resumir e explorar dados com medidas de tendência central e dispersão."
date: 2015-11-20
---

**Estatística descritiva** é o conjunto de técnicas usadas para resumir, organizar e descrever dados. É frequentemente o primeiro passo em qualquer análise de dados — antes de modelos complexos, você precisa entender seus dados.

## Por que Estatística Descritiva?

Antes de qualquer análise avançada:

- Entender os dados
- Identificar padrões
- Detectar anomalias
- Guiar próxima análise

## Medidas de Tendência Central

### Média (Mean)

A soma dos valores dividida pela contagem:

```
x̄ = (x₁ + x₂ + ... + xₙ) / n
```

**Prós:** Usa todos os valores, intuitiva
**Contras:** Sensível a outliers

```python
import numpy as np
dados = [10, 20, 30, 40, 50]
media = np.mean(dados)  # 30
```

### Mediana (Median)

O valor do meio quando ordenado:

- Ímpar: valor do meio
- Par: média dos dois valores do meio

**Prós:** Não afetada por outliers
**Contras:** Não considera todos os valores

```python
np.median([10, 20, 30, 40, 1000])  # 30 (não afetado pelo outlier)
```

### Moda (Mode)

O valor mais frequente:

```python
from scipy import stats
stats.mode([1, 2, 2, 3, 4])  # 2
```

Útil para dados categóricos.

## Medidas de Dispersão

Quão dispersos estão os valores?

### Amplitude (Range)

```
Amplitude = máximo - mínimo
```

Simples, mas sensível a outliers.

### Variância (Variance)

Média dos desvios ao quadrado:

```
σ² = Σ(xᵢ - x̄)² / (n - 1)  # sample variance
```

- Por que ao quadrado? Evita valores negativos
- (n-1) vs n: Correção de Bessel para amostra

```python
np.var(dados, ddof=1)  # sample variance
```

### Desvio Padrão (Standard Deviation)

Raiz quadrada da variância:

```
σ = √σ²
```

Mesma unidade dos dados — mais interpretável.

```python
np.std(dados, ddof=1)
```

## Quartis e Boxplots

### Quartis

Dividem os dados em 4 partes:

- **Q1 (25%)**: 25% dos dados abaixo
- **Q2 (50%)**: Mediana
- **Q3 (75%)**: 75% dos dados abaixo

### Boxplot

```
    Q1    Mediana    Q3
      |------|------|
      ■          ■
      |==========|
outliers        outliers
```

Visualiza:
- Centro (mediana)
- Dispersão (IQR)
- Outliers

```python
import matplotlib.pyplot as plt
plt.boxplot(dados)
```

## Covariância e Correlação

### Covariância

Mede como duas variáveis variam juntas:

```
cov(x,y) = Σ(xᵢ - x̄)(yᵢ - ȳ) / (n-1)
```

- Positiva: variáveis se movem na mesma direção
- Negativa: opostas
- Zero: independentes

### Correlação de Pearson

Versão normalizada (entre -1 e 1):

```
r = cov(x,y) / (σₓ × σᵧ)
```

Interpretação:

| r | Interpretação |
|---|---------------|
| 0.8 - 1.0 | Forte positiva |
| 0.5 - 0.8 | Moderada positiva |
| 0.2 - 0.5 | Fraca positiva |
| -0.2 - 0.2 | Muito fraca/nula |
| -0.5 - -0.2 | Fraca negativa |
| -0.8 - -0.5 | Moderada negativa |
| -1.0 - -0.8 | Forte negativa |

```python
np.corrcoef(x, y)[0,1]
```

**Cuidado:** Correlação não implica causalidade!

## Distribuições

### Normal (Gaussiana)

Curva em forma de sino:

```
        média = mediana = moda
              ████
           ██████████
         ████████████████
       ████████████████████
    ─────────────────────────
```

- Simétrica
- 68% dos dados dentro de 1σ
- 95% dentro de 2σ
- 99,7% dentro de 3σ

```python
from scipy import stats
stats.normaltest(dados)  # teste de normalidade
```

### Skewness (Assimetria)

- **Skew > 0**: Cauda à direita ( outliers à direita)
- **Skew < 0**: Cauda à esquerda
- **Skew ≈ 0**: Simétrica

```python
stats.skew(dados)
```

### Kurtosis (Curtose)

- **Kurtosis > 0**: Mais "picos" que normal
- **Curtose < 0**: Mais "achatada" que normal

## Visualização

### Histograma

Frequência de valores em bins:

```python
plt.hist(dados, bins=20)
```

### Gráfico de Dispersão (Scatter)

Duas variáveis:

```python
plt.scatter(x, y)
```

### Bar Chart

Dados categóricos:

```python
plt.bar(categorias, valores)
```

## Tabela Resumo

```python
import pandas as pd

df.describe()
#         idade      salario
# count    1000       1000
# mean    35.2      45000
# std      10.1      15000
# min      18        20000
# 25%      28        32000
# 50%      34        40000
# 75%      42        55000
# max      65       200000
```

## Armadilhas Comuns

### Outliers

Valores extremos podem distorcer média e variância:

```
Dados: [10, 20, 30, 40, 1000]
Média: 220 ← não representa valor típico
Mediana: 30 ← melhor
```

Sempre verifique outliers.

### Média vs Mediana

Quando usar cada:

- **Média**: Dados simétricos sem outliers
- **Mediana**: Dados com outliers ou assimétricos

Exemplo: Salários — alguns bilionários puxam média para cima.

---

**Série: Matemática**
1. [Probabilidade: Conceitos Básicos]({{ site.baseurl }}/probabilidade-conceitos-basicos)
2. [Estatística Descritiva: O Básico]({{ site.baseurl }}/estatistica-descritiva-o-basico) ← *você está aqui*

## Leia Mais

- Triola, M. F. *Introdução à Estatística*. 12ª Ed. LTC, 2017.
- Moore, D. S. *Estatística Básica e sua Prática*. 7ª Ed. LTC, 2017.
- Spiegel, M. R. *Estatística*. 3ª Ed. Pearson, 2015.
- Wharton School. *Statistics Fundamentals* (Coursera).
