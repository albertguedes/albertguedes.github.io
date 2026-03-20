---
layout: post
title: "O que é Machine Learning?"
description: "Uma introdução ao machine learning, suas categorias principais e aplicações no mundo real."
date: 2014-09-05
---

**Machine Learning** (aprendizado de máquina) é um subcampo da inteligência artificial que permite sistemas aprenderem e melhorarem automaticamente a partir da experiência, sem serem explicitamente programados para cada tarefa. É a tecnologia por trás de recomendações da Netflix, reconhecimento facial em smartphones, traduções automáticas e muito mais.

## A Ideia Fundamental

Em programação tradicional, escrevemos regras explícitas:

```text
SE email.contém("ganhou") E email.contém("prêmio")
E email.contém("clique aqui")
ENTÃO marcar como spam
```

Em machine learning, fornecemos dados e respostas, e o algoritmo **descobre** as regras:

```text
dados: milhares de emails marcados como spam/não-spam
resultado: modelo que prediz se novo email é spam
```

O modelo "aprende" padrões nos dados de treinamento que distinguem spam de emails legítimos.

## Categorias de Machine Learning

### Aprendizado Supervisionado

O algoritmo aprende a partir de **dados rotulados** — exemplos com entrada e saída desejada.

**Exemplos:**
- Classificação: spam/não-spam, gato/cachorro em imagens
- Regressão: predizer preço de casas, temperatura

**Algoritmos comuns:**
- Regressão Linear e Logística
- Árvores de Decisão
- Random Forests
- SVM (Support Vector Machines)
- Redes Neurais

### Aprendizado Não-Supervisionado

O algoritmo encontra **padrões em dados não rotulados** — não há "resposta correta".

**Exemplos:**
- Clustering: agrupar clientes por comportamento similar
- Redução de dimensionalidade: simplificar dados mantendo estrutura
- Detecção de anomalias: identificar padrões raros

**Algoritmos comuns:**
- K-Means
- DBSCAN
- PCA (Principal Component Analysis)
- Autoencoders

### Aprendizado por Reforço

Um **agente** aprende a tomar decisões através de tentativa e erro, recebendo recompensas ou penalidades.

**Exemplos:**
- Jogar xadrez contra si mesmo
- Robôs que aprendem a andar
- Otimização de rotas de entrega

## Conceitos-Chave

### Features (Atributos)

São as características individuais mensuráveis dos dados. Para um carro, features poderiam ser: ano, quilometragem, marca, potência.

A engenharia de features — escolher e transformar atributos relevantes — é crucial para o sucesso de modelos.

### Overfitting e Underfitting

- **Overfitting**: Modelo "decore" os dados de treino, mas não generaliza. Como um aluno que memoriza as provas antigas mas não entende o conteúdo.
- **Underfitting**: Modelo simples demais, não captura nem mesmo os padrões básicos. Como um aluno que chuta todas as respostas.

### Validação Cruzada

Técnica para avaliar modelos: divide-se os dados em folds, treina-se em alguns e testa-se em outros, repetidamente.

### Métricas de Avaliação

- **Accuracy**: Proporção de predições corretas
- **Precision**: Das predições positivas, quantas são realmente positivas
- **Recall**: Dos positivos reais, quantos foram identificados
- **F1-Score**: Média harmônica de precision e recall

## Aplicações do Mundo Real

### Sistemas de Recomendação
Netflix, Spotify, Amazon usam ML para recomendar conteúdo baseado em seu histórico e preferências.

### Processamento de Linguagem Natural
Tradução automática, chatbots, análise de sentimentos em redes sociais.

### Visão Computacional
Reconhecimento facial, diagnóstico médico por imagens, carros autônomos.

### Detecção de Fraudes
Bancos identificam transações suspeitas em tempo real.

### Saúde
Predição de doenças, descoberta de medicamentos, personalização de tratamentos.

## Ferramentas e Bibliotecas

O ecossistema de ML é rico:

- **Python**: Linguagem dominante em ML
- **scikit-learn**: Biblioteca para algoritmos clássicos
- **TensorFlow, PyTorch**: Deep learning
- **Keras**: API de alto nível para redes neurais
- **Pandas, NumPy**: Manipulação de dados
- **Jupyter Notebooks**: Ambiente interativo de desenvolvimento

## O Futuro do Machine Learning

- **AutoML**: Automação do processo de seleção e ajuste de modelos
- **ML explicável**: Entender por que modelos fazem certas predições
- **Federated learning**: Treinar modelos sem centralizar dados (privacidade)
- **ML em edge**: Inferência em dispositivos IoT

---

**Série: ML Básico**
1. [O que é Machine Learning?]({{ site.baseurl }}/o-que-e-machine-learning) ← *você está aqui*
2. [Aprendizado Supervisionado vs Não-Supervisionado]({{ site.baseurl }}/aprendizado-supervisionado-vs-nao-supervisionado)
3. [Regressão Linear: Uma Introdução]({{ site.baseurl }}/regressao-linear-uma-introducao)
4. [Classificação: Como Máquinas Categorizam]({{ site.baseurl }}/classificacao-como-maquinas-categorizam)

## Leia Mais

- Mitchell, T. *Machine Learning*. McGraw-Hill, 1997.
- Bishop, C. M. *Pattern Recognition and Machine Learning*. Springer, 2006.
- Hastie, T., Tibshirani, R. & Friedman, J. *The Elements of Statistical Learning*. 2ª Ed. Springer, 2009.
- Chollet, F. *Deep Learning with Python*. Manning, 2017.
