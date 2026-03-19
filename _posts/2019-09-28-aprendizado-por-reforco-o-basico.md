---
layout: post
title: "Aprendizado por Reforço: O Básico"
description: "Entenda como agentes aprendem através de tentativa e erro, recebendo recompensas e penalidades."
date: 2019-09-28
---

**Aprendizado por Reforço (RL)** é uma das três grandes categorias de machine learning. Enquanto supervised learning aprende com examples e unsupervised learning encontra patterns, RL aprende through interaction with an environment, receiving rewards or penalties for its actions.

## O Problema de RL

Imagine um agente (robot, programa, algoritmo) interagindo com um ambiente:

```
Agente → Ação → Ambiente → Novo Estado + Recompensa → Agente
```

O agente deve aprender a **maximizar a recompensa total acumulada**.

### Exemplo: Aprender a Andar

- **Agente**: Robô
- **Ambiente**: simulação física
- **Ações**: aplicar torque nos motores
- **Recompensa**: distância percorrida para frente
- **Penalidade**: quedas

O robô tenta actions, receives feedback, adjusts strategy.

## Conceitos Fundamentais

### Agente e Ambiente

**Agente**: Toma decisões (política)
**Ambiente**: Tudo que o agente interage com

### Estado e Ação

- **Estado (s)**: Representação do que o agente precisa saber
- **Ação (a)**: O que o agente pode fazer
- **Política (π)**: Mapeamento de estados para ações: π(s) → a

### Recompensa

```
r_t = feedback no instante t
```

- **Reforço positivo**: Aumenta likelihood de comportamento
- **Reforço negativo**: Diminui likelihood

O objetivo é maximizar a soma das recompensas futuras.

## O Retorno (Return)

A recompensa total acumulada:

```
G_t = r_{t+1} + r_{t+2} + r_{t+3} + ...
```

### Descont (Discount Factor)

Para dar menos weight a recompensas distantes:

```
G_t = r_{t+1} + γr_{t+2} + γ²r_{t+3} + ...
```

onde γ (gamma) é o fator de desconto (0 < γ < 1).

**Por que descontar?**
- Recompensas futuras são incertas
- Preferência por recompensas sooner
- Evita loops infinitos

## Função Valor (Value Function)

### Valor de Estado (V)

Quanto vale estar em um estado, given policy π?

```
V^π(s) = E_π[G_t | S_t = s]
```

É a expected return from that state onwards.

### Valor Estado-Ação (Q)

Quanto vale tomar uma ação em um estado?

```
Q^π(s, a) = E_π[G_t | S_t = s, A_t = a]
```

### Equação de Bellman

Expressa recursively:

```
V^π(s) = Σ_a π(a|s) Σ_{s', r} p(s', r | s, a) [r + γV^π(s')]
```

A value de um estado é a weighted average dos values dos estados seguintes.

## Q-Learning

### A Ideia Central

O agente learns the optimal Q-function directly:

```
Q(s, a) ← Q(s, a) + α [r + γ max_{a'} Q(s', a') - Q(s, a)]
```

- **α**: Taxa de aprendizado
- **r + γ max Q**: TD target
- **Q(s,a)**: Old estimate

### Algoritmo

```python
# Inicialize Q(s,a) arbitrariamente
# Para cada episódio:
    # Estado inicial s
    # Enquanto não terminal:
        # Escolha ação a (ε-greedy)
        # Execute a, observe r, s'
        # Atualize Q(s,a)
        # s ← s'
```

### ε-greedy

- Com probabilidade ε: escolha ação aleatória (exploração)
- Com probabilidade 1-ε: escolha argmax Q(s,a) (exploração)

## Deep Q-Network (DQN)

Q-learning com deep neural networks:

```
Rede Neural: Input = estado, Output = Q(s,a) para cada a
```

### DQN Tricks

1. **Experience Replay**: Armazena transições, sample aleatoriamente para training (breaks correlation)
2. **Target Network**: Rede separada para calcular targets (estável)

```python
# Sample from replay buffer
(s, a, r, s', done) = sample(buffer)

# Target
if done:
    target = r
else:
    target = r + γ * max_a' Q_target(s', a')

# Update network to predict target
```

## Policy Gradients

Métodos que aprendem diretamente a política:

```
π_θ(a|s) = probability of taking action a given state s
```

### REINFORCE

```
∇_θ J(θ) = E[∇_θ log π_θ(a|s) × G_t]
```

Update parameters in direction that increases probability of good actions.

### Vantagens sobre Q-Learning

- Pode aprender políticas estocásticas
- Melhor para espaços de ação contínuos
- Mais estável em certos domínios

## Actor-Critic

Combina benefits de value-based e policy-based:

- **Actor**: Rede que outputs políticas (π)
- **Critic**: Rede que estimates value function (V)

```
Actor atualiza política based on feedback do Critic
Critic updates value estimates
```

## Aplicaçõees Famosas

### AlphaGo (2016)

DeepMind's program beat champion at Go:
- Usa Monte Carlo Tree Search + deep neural networks
- Treinado com supervised learning + RL + self-play

### Atari Games

DQN aprende a jogar 49 games diretamente from pixels:
- Sem knowledge prévio sobre games
- Descobre estratégias sophisticated

### Robótica

- Boston Dynamics robots
- Locomotion, manipulation
- Sim-to-real transfer

### Other

- Recomendação systems
- Trading algorítmico
- Resource management

## Desafios

### Sample Efficiency

RL typically precisa de muitas interações — pode requiring millions de steps.

### Exploration vs Exploitation

Encontrar balance entre explorar novas ações e exploit known good actions.

### Reward Hacking

Agente encontra formas de maximizar recompensa sem achieving intended goal:

```
Recompensa = número de pontos
    → Agente finds bug que dá pontos infinitos
```

### Catastrofic Forgetting

Rede esquece como fazer earlier tasks ao aprender new ones.

## Hierarchical RL

Decompor problemas em multiple levels of abstraction:

```
Meta-controller → subtasks → primitive actions
```

## Model-Based RL

Aprende modelo do ambiente (transitions e rewards), then plans:

```
Transitions: p(s'|s, a)
Rewards: r(s, a)
```

Mais sample efficient, but harder to learn accurate model.

---

**Série: IA Avançada**
1. [Aprendizado por Reforço: O Básico]({{ site.baseurl }}/aprendizado-por-reforco-o-basico) ← *você está aqui*
2. [AGI: Inteligência Artificial Geral]({{ site.baseurl }}/agi-inteligencia-artificial-geral)

## Leia Mais

- Sutton, R. S. & Barto, A. G. *Reinforcement Learning: An Introduction*. 2nd Ed. MIT Press, 2018.
- Mnih, V. et al. "Human-level control through deep reinforcement learning". *Nature*, 2015.
- Silver, D. et al. "Mastering the game of Go with deep neural networks". *Nature*, 2016.
- OpenAI. "Spinning Up in Deep RL".
