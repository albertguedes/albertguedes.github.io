---
layout: post
title: "Aprendizado Supervisionado vs Não-Supervisionado"
description: "Entenda as duas grandes categorias de machine learning e quando usar cada uma."
date: 2017-10-03
---

No universo do machine learning, os algoritmos geralmente se dividem em duas grandes categorias: **aprendizado supervisionado** e **aprendizado não-supervisionado**. Compreender a diferença entre eles é fundamental para saber qual técnica aplicar em cada problema.

## A Diferença Fundamental

### Aprendizado Supervisionado

O algoritmo aprende a partir de **dados rotulados** — cada exemplo de treinamento tem entrada e a saída desejada (label).

```text
Entrada → Saída desejada
Email → "spam" ou "não-spam"
Imagem → "gato" ou "cachorro"
```

O algoritmo "aprende" mapeando entradas para saídas corretas.

### Aprendizado Não-Supervisionado

O algoritmo encontra **padrões em dados não rotulados** — não há "resposta correta", apenas estrutura nos dados.

```text
Entrada → Padrões/Grupos encontrados
Clientes → Grupos por comportamento similar
Transações → Anomalias detectadas
```

## Aprendizado Supervisionado

### Classificação

A variável de saída é **categórica** (labels discretos):

- Spam ou não-spam
- Gato, cachorro ou pássaro
- Tumor maligno ou benigno

#### Algoritmos Comuns

**Regressão Logística**
$$P(Y=1|X) = \text{sigmoid}(w_0 + w_1x_1 + \cdots + w_nx_n)$$
Usada para classificação binária.

**Random Forests**
Ensemble de árvores de decisão que votam na classificação final. Robusta e difícil de overfit.

**SVM (Support Vector Machines)**
Encontra o hiperplano que melhor separa as classes. Eficaz em altas dimensões.

**Redes Neurais**
Podem aprender boundaries de decisão complexos e não-lineares.

### Regressão

A variável de saída é **contínua**:

- Predizer preço de casas
- Estimar temperatura
- Prever vendas

#### Algoritmos Comuns

**Regressão Linear**
$$Y = \beta_0 + \beta_1X_1 + \beta_2X_2 + \cdots + \varepsilon$$
Simples, interpretável, baseline útil.

**Regressão Polinomial**
Captura relações não-lineares adicionando termos de potências maiores.

**Gradient Boosting (XGBoost, LightGBM)**
Combina múltiplos modelos fracos sequencialmente, cada um corrigindo o anterior.

### Validação

Dividir dados:
- **Treino**: Para aprender o modelo
- **Validação**: Para ajustar hiperparâmetros
- **Teste**: Para avaliar performance final (só usar uma vez!)

Métricas comuns:
- Accuracy, Precision, Recall, F1-Score (classificação)
- MSE, RMSE, MAE, R² (regressão)

## Aprendizado Não-Supervisionado

### Clustering (Agrupamento)

Encontrar **grupos naturais** nos dados:

```text
Clientes
   ├── Grupo 1: Jovens, alto gasto
   ├── Grupo 2: Idosos, baixo gasto
   └── Grupo 3: Famílias, médio gasto
```

#### K-Means

1. Escolhe K centroides iniciais
2. Atribui cada ponto ao centroid mais próximo
3. Recalcula centroides
4. Repete até convergence

Simples, eficiente, mas requer escolher K e assume clusters esféricos.

#### DBSCAN

Baseado em densidade — encontra clusters de forma arbitrária e detecta outliers automaticamente.

```text
Ponto é core se tem N vizinhos dentro do raio ε
Ponto é border se é alcançável a partir de um core
Ponto é ruído se não é nenhum dos dois
```

### Redução de Dimensionalidade

Reduzir o número de features preservando a estrutura:

```text
Imagem 1000x1000 = 1.000.000 features
                    ↓
              100 componentes principais
```

#### PCA (Principal Component Analysis)

Encontra as direções de máxima variância nos dados:
1. Calcula matriz de covariância
2. Encontra autovetores (componentes principais)
3. Projeta dados nos primeiros K componentes

Mantém máxima informação com mínima perda.

#### t-SNE

Excelente para visualização:
- Preserva a estrutura local
- Bom para ver clusters em 2-3 dimensões

### Detecção de Anomalias

Identificar pontos que não se encaixam nos padrões normais:

- Transações fraudulentas
- Equipamentos com falha iminente
- Ataques cibernéticos

#### Métodos

- Isolation Forest
- Local Outlier Factor
- Autoencoders (redes neurais)

### Regras de Associação

Encontrar relações entre variáveis:

```text
Se cliente compra pão, também compra manteiga (80% das vezes)
```

Aplicações: sistemas de recomendação, market basket analysis.

## Qual Usar?

### Use Supervisionado Quando:

- Você tem dados rotulados
- Quer predizer uma variável específica
- Precisa de explicações claras
- Tem dados suficientes com labels

### Use Não-Supervisionado Quando:

- Não há labels disponíveis
- Quer explorar a estrutura dos dados
- Precisa reduzir dimensionality
- Deseja detectar anomalias

## Abordagem Híbrida

Na prática, muitas vezes combinam:

### Semi-supervised Learning
Usa poucos dados rotulados + muitos não-rotulados para melhorar o modelo.

### Self-supervised Learning
Cria labels automaticamente de dados (ex: prever próxima palavra em texto).

### Clustering + Supervisão
Às vezes, fazer clustering primeiro ajuda a entender os dados antes de classificar.

## Exemplos no Mundo Real

| Problema | Tipo | Algoritmo |
|----------|------|-----------|
| Detectar spam | Supervisionado | Random Forest |
| Segmentar clientes | Não-supervisionado | K-Means |
| Prever vendas | Supervisionado | XGBoost |
| Reduzir dimensionality de imagem | Não-supervisionado | PCA, Autoencoder |
| Detectar fraude | Híbrido | Clustering + Classificação |

---

**Série: ML Básico**
1. [O que é Machine Learning?]({{ site.baseurl }}/o-que-e-machine-learning)
2. [Aprendizado Supervisionado vs Não-Supervisionado]({{ site.baseurl }}/aprendizado-supervisionado-vs-nao-supervisionado) ← *você está aqui*
3. [Regressão Linear: Uma Introdução]({{ site.baseurl }}/regressao-linear-uma-introducao)
4. [Classificação: Como Máquinas Categorizam]({{ site.baseurl }}/classificacao-como-maquinas-categorizam)

## Leia Mais

- Mitchell, T. *Machine Learning*. McGraw-Hill, 1997.
- Bishop, C. M. *Pattern Recognition and Machine Learning*. Springer, 2006.
- Hastie, T., Tibshirani, R. & Friedman, J. *The Elements of Statistical Learning*. 2ª Ed. Springer, 2009.
- James, G. et al. *An Introduction to Statistical Learning*. 2ª Ed. Springer, 2021.
