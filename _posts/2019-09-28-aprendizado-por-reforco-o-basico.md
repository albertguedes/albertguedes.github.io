---
layout: post
title: "Aprendizado por Reforço: O Básico"
description: "Entenda como agentes aprendem através de tentativa e erro, recebendo recompensas e penalidades."
date: 2019-09-28
---

**Aprendizado por Reforço (RL)** é uma das três grandes categorias de machine learning. Enquanto supervised learning aprende com exemplos e unsupervised learning encontra padrões, RL aprende através de interação com um ambiente, recebendo recompensas ou penalidades por suas ações.

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

O robô tenta ações, recebe feedback, ajusta estratégia.

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

- **Reforço positivo**: Aumenta probabilidade de comportamento
- **Reforço negativo**: Diminui probabilidade

O objetivo é maximizar a soma das recompensas futuras.

## O Retorno (Return)

A recompensa total acumulada:

```
G_t = r_{t+1} + r_{t+2} + r_{t+3} + ...
```

### Desconto (Discount Factor)

Para dar menos peso a recompensas distantes:

```
G_t = r_{t+1} + γr_{t+2} + γ²r_{t+3} + ...
```

onde γ (gamma) é o fator de desconto (0 < γ < 1).

**Por que descontar?**
- Recompensas futuras são incertas
- Preferência por recompensas mais cedo
- Evita loops infinitos

## Função Valor (Value Function)

### Valor de Estado (V)

Quanto vale estar em um estado, dada uma política π?

```
V^π(s) = E_π[G_t | S_t = s]
```

É o retorno esperado a partir desse estado.

### Valor Estado-Ação (Q)

Quanto vale tomar uma ação em um estado?

```
Q^π(s, a) = E_π[G_t | S_t = s, A_t = a]
```

### Equação de Bellman

Expressa recursivamente:

```
V^π(s) = Σ_a π(a|s) Σ_{s', r} p(s', r | s, a) [r + γV^π(s')]
```

O valor de um estado é a média ponderada dos valores dos estados seguintes.

## Q-Learning

### A Ideia Central

O agente aprende a função Q ótima diretamente:

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

1. **Experience Replay**: Armazena transições, amostra aleatoriamente para treinamento (quebra correlação)
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
π_θ(a|s) = probabilidade de tomar ação a dado estado s
```

### REINFORCE

```
∇_θ J(θ) = E[∇_θ log π_θ(a|s) × G_t]
```

Atualiza parâmetros na direção que aumenta probabilidade de boas ações.

### Vantagens sobre Q-Learning

- Pode aprender políticas estocásticas
- Melhor para espaços de ação contínuos
- Mais estável em certos domínios

## Actor-Critic

Combina benefícios de value-based e policy-based:

- **Actor**: Rede que produz políticas (π)
- **Critic**: Rede que estima função valor (V)

```
Actor atualiza política baseada no feedback do Critic
Critic atualiza estimativas de valor
```

## Aplicações Famosas

### AlphaGo (2016)

Programa da DeepMind derrotou campeão no Go:
- Usa Monte Carlo Tree Search + deep neural networks
- Treinado com supervised learning + RL + self-play

### Atari Games

DQN aprende a jogar 49 games diretamente de pixels:
- Sem conhecimento prévio sobre games
- Descobre estratégias sofisticadas

### Robótica

- Boston Dynamics robots
- Locomoção, manipulação
- Transferência simulação-para-realidade

### Outros

- Sistemas de recomendação
- Trading algorítmico
- Gerenciamento de recursos

## Desafios

### Sample Efficiency

RL tipicamente precisa de muitas interações — pode requerer milhões de passos.

### Exploration vs Exploitation

Encontrar equilíbrio entre explorar novas ações e explorar ações conhecidas boas.

### Reward Hacking

Agente encontra formas de maximizar recompensa sem alcançar o objetivo pretendido:

```
Recompensa = número de pontos
    → Agente encontra bug que dá pontos infinitos
```

### Esquecimento Catastrófico

Rede esquece como fazer tarefas anteriores ao aprender novas.

## Hierarchical RL

Decompor problemas em múltiplos níveis de abstração:

```
Meta-controller → subtasks → primitive actions
```

## Model-Based RL

Aprende modelo do ambiente (transições e recompensas), depois planeja:

```
Transitions: p(s'|s, a)
Rewards: r(s, a)
```

Mais eficiente em samples, mas mais difícil aprender modelo preciso.

---

**Série: IA Avançada**
1. [Aprendizado por Reforço: O Básico]({{ site.baseurl }}/aprendizado-por-reforco-o-basico) ← *você está aqui*
2. [AGI: Inteligência Artificial Geral]({{ site.baseurl }}/agi-inteligencia-artificial-geral)

## Leia Mais

- Sutton, R. S. & Barto, A. G. *Reinforcement Learning: An Introduction*. 2nd Ed. MIT Press, 2018.
- Mnih, V. et al. "Human-level control through deep reinforcement learning". *Nature*, 2015.
- Silver, D. et al. "Mastering the game of Go with deep neural networks". *Nature*, 2016.
- OpenAI. "Spinning Up in Deep RL".
