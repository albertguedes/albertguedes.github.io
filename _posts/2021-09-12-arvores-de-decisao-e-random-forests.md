---
layout: post
title: "Árvores de Decisão e Random Forests"
description: "Conheça algoritmos interpretáveis e poderosos para classificação e regressão."
date: 2021-09-12
---

**Árvores de decisão** são um dos algoritmos de machine learning mais intuitivos e versáteis. Simples de entender, fáceis de interpretar, e formam a base para **Random Forests** — um dos métodos mais robustos para problemas supervisionados.

## O que é uma Árvore de Decisão?

Uma árvore de decisão é como um fluxograma de decisões:

```
                    Chover?
                   /        \
               Sim          Não
              /                \
        Tênis?            Sair de guarda-chuva?
        /    \              /          \
     Sim      Não        Sim            Não
      ↓        ↓          ↓              ↓
   "Use"    "Sandálias"  "Levar"       "Não levar"
```

Cada nó interno é uma pergunta sobre uma feature, cada folha é uma decisão/classe.

## Construindo Árvores

### Critério de Divisão (Split)

Árvores escolhem pergunstas that best separate the target classes.

**Para classificação**, comum usar:
- **Gini impurity**: Mede "impureza" de um nó
- **Entropy**: Mede "desordem" information-theoretic

**Gini Impurity:**
```
Gini = 1 - Σ pᵢ²
```

Menor Gini = mais puro = melhor split.

### Como Funciona

1. Para cada feature, testar todos os possíveis splits
2. Calcular impurity de cada lado da split
3. Weighted average para get split quality
4. Escolher best split

```
Feature: "idade > 30?"
Gini antes: 0.5
Gini depois: 0.2 (jovens) + 0.3 (idosos) weighted average
```

5. Recursivamente repeat for child nodes
6. Parar quando:
   - Todas samples são da mesma classe
   - Máxima profundidade atingida
   - Mínimo de samples por nó

## Regressão com Árvores

Para targets contínuos:

- Em vez de Gini/Entropy, usar **MSE** (Mean Squared Error)
- Folhas predict a média dos valores
- Funciona mesmo com não-linearidades

## Vantagens e Desvantagens

### Vantagens

- **Interpretável**: Árvores podem ser visualizadas e explicadas
- **Não precisa normalização**: Works with any feature scales
- **Lida com não-linearidades**: Naturally
- **Feature importance**: Built-in
- **Pode handle missing values**: Naturally

### Desvantagens

- **Overfitting**: Árvores profundas memorizam noise
- **Instável**: Pequenas mudanças nos dados podem alterar estrutura
- **Bias para features com muitas categorias**: Tendem a overfit nelas
- ** Não tão accurate** como outros methods

## Ensemble Learning

Multiple modelos combinam forces:

```
Múltiplas árvores "fracas"
        ↓
    Votação/Média
        ↓
Predição "forte"
```

### Bagging (Bootstrap Aggregating)

Treina múltiplas árvores em bootstrap samples:

1. Sample with replacement from training data
2. Treinar árvore em cada sample
3. Average predictions (regressão) or vote (classificação)

Reduz variance sem increase bias.

## Random Forests

Extensão de bagging com **feature randomness**:

### Como Funciona

1. Para cada árvore:
   - Bootstrap sample dos dados
   - Em cada split, only random subset of features is considered
2. Final prediction: average or vote

**Por que random features?**
- Reduces correlation entre árvores
- Forces trees to be different
- Previne que todas árvores usem same strong features

### Hiperparâmetros Importantes

```python
from sklearn.ensemble import RandomForestClassifier

rf = RandomForestClassifier(
    n_estimators=100,      # Número de árvores
    max_depth=10,          # Profundidade máxima
    min_samples_split=5,   # Mín samples para split
    max_features='sqrt',  # Features por split (sqrt is common)
    random_state=42        # Reprodutibilidade
)
```

### n_estimators

- Mais árvores = mais estável, melhor generalization
- Diminishing returns after some point
- Trade-off: more trees = more computation

### max_depth

Controla complexidade das árvores:
- None: trees grow until pure
- Limitar: reduces overfitting

### Feature Importance

Random Forests provide built-in importance:

```python
rf.fit(X, y)
importances = rf.feature_importances_
```

Baseado em how much each feature reduces impurity, averaged over all trees.

## Gradient Boosting

Outra técnica de ensemble — **boosting sequential**:

1. Treina árvore shallow
2. Calcula residuals (erros)
3. Próxima árvore learns to fix those errors
4. Repete

**Resultado**: Ensemble que corrige errors dos modelos anteriores.

### XGBoost, LightGBM, CatBoost

Implementações optimizadas de gradient boosting:

- Faster training
- Better handling of sparse data
- Regularização built-in
- Commonly used em competições (Kaggle)

## Quando Usar Cada Um

| Situação | Recomendação |
|----------|-------------|
| Precisa interpretabilidade | Árvore única |
| Dataset pequeno/médio | Random Forest |
| Dataset grande | XGBoost/LightGBM |
| Classificação binária | Logistic Regression ou SVM (linear) |
| Many features, sparse | Linear models ou tree-based |

## Exemplo Prático

```python
from sklearn.ensemble import RandomForestClassifier
from sklearn.model_selection import train_test_split
from sklearn.metrics import accuracy_score

# Split
X_train, X_test, y_train, y_test = train_test_split(X, y)

# Treinar
rf = RandomForestClassifier(n_estimators=100, random_state=42)
rf.fit(X_train, y_train)

# Prever
y_pred = rf.predict(X_test)
print(f"Accuracy: {accuracy_score(y_test, y_pred):.3f}")

# Feature importance
importances = pd.DataFrame({
    'feature': X.columns,
    'importance': rf.feature_importances_
}).sort_values('importance', ascending=False)
```

## XGBoost vs Random Forest

| Aspecto | Random Forest | XGBoost |
|---------|--------------|---------|
| Ensemble | Bagging | Boosting |
| Trees | Deep | Shallow (often) |
| Overfitting risk | Lower | Can overfit if tuned poorly |
| Training speed | Faster | Slower (but optimized) |
| Hyperparameters | Fewer | Many |

---

**Série: ML Prático**
1. [Árvores de Decisão e Random Forests]({{ site.baseurl }}/arvores-de-decisao-e-random-forests) ← *você está aqui*
2. [Engenharia de Features: O Básico]({{ site.baseurl }}/engenharia-de-features-o-basico)

## Leia Mais

- Breiman, L. et al. *Classification and Regression Trees*. Wadsworth, 1984.
- Breiman, L. "Random Forests". *Machine Learning*, 2001.
- Hastie, T., Tibshirani, R. & Friedman, J. *The Elements of Statistical Learning*. 2ª Ed. Springer, 2009.
- Chen, T. & Guestrin, C. "XGBoost". *KDD*, 2016.
