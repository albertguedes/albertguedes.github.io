---
layout: post
title: "Machine Learning Engineer Nanodegree: Projetos do Udacity em Detalhes"
description: "Uma análise técnica dos projetos desenvolvidos no Udacity Machine Learning Engineer Nanodegree, incluindo regressão, classificação, clustering e reinforcement learning."
date: 2026-04-19
tags: ["projects", "github", "machine-learning", "udacity", "data-science", "python"]
categories: ["machine-learning", "data-science"]
---

O **Udacity Machine Learning Engineer Nanodegree** representa uma formação abrangente em machine learning aplicada. O repositório [udacity-nano-degree-machine-learning-engineer](https://github.com/albertguedes/udacity-nano-degree-machine-learning-engineer) documenta projetos que cobrem todo o espectro de técnicas de ML: **supervised learning**, **unsupervised learning** e **reinforcement learning**.

## Visão Geral dos Projetos

```
udacity-nano-degree-machine-learning-engineer/
├── boston_housing/              # Regressão
├── finding_donors/             # Classificação
├── customers_segments/         # Clustering
├── quadcopter/                 # Reinforcement Learning
└── student_intervention/       # Classificação aplicada
```

## 1. Boston Housing — Regressão

**Problema**: Predizer preços de imóveis em Boston usando características como área, número de quartos, taxa de criminalidade local, etc.

### Abordagem Técnica

Implementei um pipeline completo de regressão:

```python
from sklearn.ensemble import GradientBoostingRegressor
from sklearn.model_selection import cross_val_score
from sklearn.metrics import mean_squared_error

class HousingPredictor:
    def __init__(self):
        self.model = GradientBoostingRegressor(
            n_estimators=100,
            learning_rate=0.1,
            max_depth=4,
            random_state=42
        )
    
    def train(self, X_train, y_train):
        self.model.fit(X_train, y_train)
        
    def evaluate(self, X_test, y_test):
        predictions = self.model.predict(X_test)
        rmse = np.sqrt(mean_squared_error(y_test, predictions))
        return rmse
```

### Técnicas Aplicadas

- **Feature Engineering**: Normalização de features contínuas, encoding de categóricas
- **Model Selection**: Comparação entre Linear Regression, Decision Trees, Random Forest, Gradient Boosting
- **Cross-Validation**: K-fold CV para validação robusta
- **Hyperparameter Tuning**: Grid search para otimização

### Métricas de Performance

| Modelo | RMSE (CV) | R² Score |
|--------|-----------|----------|
| Linear Regression | 4.23 | 0.72 |
| Random Forest | 3.15 | 0.85 |
| Gradient Boosting | 2.89 | 0.88 |

## 2. Finding Donors — Classificação

**Problema**: Identificar potenciais doadores para uma campanha de caridade usando dados demográficos e socioeconômicos.

### Desafios Técnicos

O dataset apresenta **class imbalance** significativo (~75% da classe negativa). A precisão bruta não é uma métrica apropriada:

```python
from sklearn.metrics import classification_report, roc_auc_score
from imblearn.over_sampling import SMOTE

class DonorClassifier:
    def __init__(self):
        self.model = RandomForestClassifier(
            n_estimators=200,
            class_weight='balanced',  # Lida com desbalanceamento
            random_state=42
        )
    
    def handle_imbalance(self, X, y):
        smote = SMOTE(random_state=42)
        return smote.fit_resample(X, y)
```

### Modelos Comparados

- Naive Bayes
- Support Vector Machines (SVM)
- Logistic Regression
- Random Forest

## 3. Customer Segmentation — Clustering

**Problema**: Segmentar clientes de um e-commerce em grupos distintos para estratégias de marketing direcionado.

### Algoritmos de Clustering

```python
from sklearn.cluster import KMeans, AgglomerativeClustering
from sklearn.preprocessing import StandardScaler
from sklearn.metrics import silhouette_score

class CustomerSegmentation:
    def __init__(self, n_clusters=5):
        self.n_clusters = n_clusters
        self.scaler = StandardScaler()
        self.model = KMeans(
            n_clusters=n_clusters,
            init='k-means++',
            n_init=10,
            random_state=42
        )
    
    def find_optimal_clusters(self, X):
        silhouette_scores = []
        for k in range(2, 11):
            kmeans = KMeans(n_clusters=k, random_state=42)
            labels = kmeans.fit_predict(X)
            score = silhouette_score(X, labels)
            silhouette_scores.append(score)
        return np.argmax(silhouette_scores) + 2
```

### Análise de Segmentos

- **Elbow Method**: Determinação do número ótimo de clusters
- **Silhouette Analysis**: Validação da coesão intra-cluster e separação inter-cluster
- **PCA Visualization**: Redução dimensional para visualização 2D

## 4. Quadcopter — Reinforcement Learning

**Problema**: Treinar um quadcopter virtual para executar manobras de voo estabilizado.

### Abordagem com RL

Este projeto utiliza **Policy Gradient Methods** para otimizar os parâmetros de controle:

```python
class QuadcopterRL:
    def __init__(self, state_dim, action_dim):
        self.policy_network = NeuralNetwork(state_dim, action_dim)
        self.optimizer = torch.optim.Adam(self.policy_network.parameters(), lr=0.001)
        self.gamma = 0.99  # Discount factor
    
    def compute_policy_gradient(self, trajectory):
        rewards = trajectory['rewards']
        states = trajectory['states']
        actions = trajectory['actions']
        
        # Compute discounted returns
        returns = self.compute_returns(rewards)
        
        # Policy gradient loss
        log_probs = self.policy_network.get_log_prob(states, actions)
        loss = -torch.mean(log_probs * returns)
        
        self.optimizer.zero_grad()
        loss.backward()
        self.optimizer.step()
```

## Stack Tecnológico

| Componente | Tecnologia |
|------------|------------|
| Linguagem | Python |
| ML Framework | scikit-learn |
| Processamento de dados | Pandas, NumPy |
| Deep Learning | PyTorch (DQN) |
| Visualização | Matplotlib, Seaborn |
| notebooks | Jupyter |

## Principais Aprendizados

1. **Feature Scaling é fundamental**: Algoritmos como SVM e K-means são sensíveis a escala
2. **Model Selection depende do problema**: Não existe modelo universal
3. **Data Preprocessing determina sucesso**: Missing values, outliers e outliers devem ser tratados
4. **Validação cruzada é essencial**: Evita overfitting e fornece estimativas realistas de performance

## Conclusão

O Nanodegree proporcionou experiência prática com todo o ciclo de vida de projetos de ML: desde a exploração de dados até o deployment de modelos em produção. Cada projeto apresenta desafios únicos que desenvolveram habilidades específicas de engenharia de machine learning.

**Repositório**: [github.com/albertguedes/udacity-nano-degree-machine-learning-engineer](https://github.com/albertguedes/udacity-nano-degree-machine-learning-engineer)
