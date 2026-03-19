---
layout: post
title: "Classificação: Como Máquinas Categorizam"
description: "Entenda os algoritmos de classificação em machine learning, de regressão logística a random forests."
date: 2021-05-15
---

**Classificação** é uma das tarefas mais importantes em machine learning — determinar a qual categoria um objeto pertence. Quando seu email é marcado como spam, quando um médico diagnostica uma doença, quando um banco decide aprovar um crédito — todos são problemas de classificação.

## O que é Classificação?

Em classificação, a variável de saída é **categórica** — discrete classes rather than continuous values.

**Exemplos:**
- Email → spam ou não-spam (binária)
- Imagem → gato, cachorro, ou pássaro (multiclasse)
- Transação → fraudulenta ou legítima (binária)
- Documento → positivo, negativo, ou neutro (multiclasse com 3+ classes)

## Regressão Logística

Despite do nome, é um algoritmo de **classificação**, não regressão.

### Como Funciona?

Usa a função **sigmoid** para converter scores lineares em probabilidades:

```
P(y=1|x) = 1 / (1 + e^(-z))
        onde z = β₀ + β₁x₁ + ... + βₙxₙ
```

A sigmoid transforma qualquer valor real em 0-1.

### Interpretação

```
Se P(y=1|x) > 0.5 → prevemos classe 1
Se P(y=1|x) < 0.5 → prevemos classe 0
```

O threshold de 0.5 pode ser ajustado based em custos de erro.

## Árvores de Decisão

Estrutura hierárquica de decisões simples:

```
                    Pergunta 1
                    /        \
              Sim              Não
              ↓                ↓
         Pergunta 2       Pergunta 3
          /    \            /    \
       Sim    Não        Sim    Não
        ↓      ↓          ↓      ↓
      Folha  Folha      Folha  Folha
```

Cada nó interno é uma pergunta sobre uma feature, cada folha é uma classe.

### Entropia e Ganho de Informação

Árvores escolhem splits que **maximizam o ganho de informação**:

```
Entropia(S) = -Σ pᵢ × log₂(pᵢ)
```

Menor entropia = mais "puro" (homogêneo) = melhor split.

### Vantagens e Desvantagens

**Prós:**
- Fácil de interpretar
- Não requer normalização de features
- Captura não-linearidades
- Lida bem com missing values

**Contras:**
- Propenso a overfitting
- Frágeis a pequenas mudanças nos dados
- Podem criar boundaries complexos de forma ineficiente

## Random Forests

**Ensemble** de múltiplas árvores de decisão:

1. Treina múltiplas árvores em bootstrap samples (amostragem com reposição)
2. Cada árvore vê apenas um subconjunto de features
3. Prediction final é voting among all trees

### Por que Funciona?

- **Reduce variance**: Erros de árvores individuais tendem a cancelar
- **Decorrelation**: Trees treinadas em diferentes subsets de features são menos correlacionadas
- **Robustez**: Menos sensível a outliers

### Hiperparâmetros Importantes

- **n_estimators**: Número de árvores (mais = melhor, com diminishing returns)
- **max_depth**: Profundidade máxima de cada árvore
- **min_samples_split**: Mínimo de amostras para fazer split
- **max_features**: Número de features por árvore

## Support Vector Machines (SVM)

### A Ideia Central

SVM encontra o **hiperplano ótimo** que separa as classes com a **margem máxima**:

```
        Classe 1        Hiperplano        Classe 2
    ● ● ● ●            |            ○ ○ ○ ○
      ● ● ● ●          |            ○ ○ ○
    ● ● ● ●            |            ○ ○ ○
```

Support vectors são os pontos mais próximos do hiperplano — eles "sustentam" a margem.

### Kernels

Para dados não-linearmente separáveis, SVM usa **kernels** para project data into higher-dimensional space onde separação é possível:

- **Linear**: Para dados já separáveis
- **RBF (Gaussiano)**: Comumente usado, very flexible
- **Polinomial**: Pode capture polynomial relationships

### Vantagens e Desvantagens

**Prós:**
- Effective em altas dimensões
- Funciona bem com boundarys de decisão claros
- Memory efficient (apenas support vectors são stored)

**Contras:**
- Pode ser lento para datasets grandes
- Sensível à escolha do kernel e hyperparameters
- Não escala bem com many samples

## Métricas de Avaliação

### Matriz de Confusão

```
                 Predito
              Positivo  Negativo
Real  Positivo    TP       FN
      Negativo    FP       TN
```

### Acurácia

```
Acurácia = (TP + TN) / Total
```

Simples, mas pode ser misleading com classes desbalanceadas.

### Precision e Recall

```
Precision = TP / (TP + FP)  (dos que chamei de positivo, quantos realmente eram)
Recall = TP / (TP + FN)     (de todos os positivos reais, quantos encontrei)
```

### F1-Score

```
F1 = 2 × (Precision × Recall) / (Precision + Recall)
```

Média harmônica — penaliza quando uma é muito baixa.

### ROC AUC

Curva ROC plota True Positive Rate vs False Positive Rate. AUC = área sob a curva. Valores mais próximos de 1 = melhor.

## Lidando com Classes Desbalanceadas

Quando uma classe é muito mais frequente:

### Técnicas

**1. SMOTE**: Synthetic Minority Over-sampling
**2. Undersampling da classe majoritária**
**3. Class weights**: Ponderar errors differently
**4. Ensemble de undersampled sets**: BalancedBagging

### Escolher Métrica Certa

- Acurácia pode ser alta mesmo com modelo useless
- Se FP é muito custoso: maximize Precision
- Se FN é muito custoso: maximize Recall
- F1 balance between both

## Aplicações no Mundo Real

### Filtragem de Spam

```
Features: palavras, remetente, headers, links
Classe: spam ou não-spam
```

### Diagnóstico Médico

```
Features: sintomas, exames, histórico
Classe: doença presente ou ausente
```

### Scoring de Crédito

```
Features: renda, histórico, dívidas, emprego
Classe: aprovado ou rejeitado
```

---

**Série: ML Básico**
1. [O que é Machine Learning?]({{ site.baseurl }}/o-que-e-machine-learning)
2. [Aprendizado Supervisionado vs Não-Supervisionado]({{ site.baseurl }}/aprendizado-supervisionado-vs-nao-supervisionado)
3. [Regressão Linear: Uma Introdução]({{ site.baseurl }}/regressao-linear-uma-introducao)
4. [Classificação: Como Máquinas Categorizam]({{ site.baseurl }}/classificacao-como-maquinas-categorizam) ← *você está aqui*

## Leia Mais

- Mitchell, T. *Machine Learning*. McGraw-Hill, 1997.
- Bishop, C. M. *Pattern Recognition and Machine Learning*. Springer, 2006.
- Hastie, T., Tibshirani, R. & Friedman, J. *The Elements of Statistical Learning*. 2ª Ed. Springer, 2009.
- James, G. et al. *An Introduction to Statistical Learning*. 2ª Ed. Springer, 2021.
