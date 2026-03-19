---
layout: post
title: "AGI: Inteligência Artificial Geral"
description: "Entenda o conceito de IA geral, seus desafios e o debate sobre quando chegaremos lá."
date: 2024-03-20
---

**Inteligência Artificial Geral (AGI)** — também chamada de "IA forte" ou "IA completa" — é o objetivo de criar máquinas com intelligence comparável à humana em praticamente qualquer domínio cognitivo. É um dos objetivos mais ambiciosos e controversos da ciência.

## O que é AGI?

### Definições

AGI seria um sistema com:

- **Raciocínio**: Capaz de resolver problemas novos e complexos
- **Aprendizado**: Pode aprender from any experience, like humans
- **Abstração**: Working with concepts, not just pattern matching
- **Transfer**: Aplicar conhecimento de um domain to another
- **Understanding**: Compreensão genuine, not just statistical correlation
- **Autonomy**: Pode pursue goals without constant human guidance

### Diferença de IA Estreita

| IA Estreita ( atual) | AGI |
|--------------------|-----|
| Uma tarefa | Qualquer tarefa |
| Não transfere | Transfere entre domínios |
| Não Generaliza | Generaliza |
| "AlfaGo não sabe jogar xadrez" | Seria capaz de aprender ambos |

## Por que AGI é Difícil?

### O Problema do Sentido Comum

Humanos have "common sense" about the physical and social world:

- Objetos caem, não flutuam
- Água molha, fire burns
- Pessoas têm goals e beliefs

Trazêmo isso para machines é surpreendentemente difícil.

### Amostras de Comportamento vs. Understanding Real

Sistemas atuais podem passing tests designed for humans without truly understanding:

```
GPT-4 passes bar exam, medical boards
Mas não "entende" direito como um humano faria
```

É isso inteligente ou apenas muito good at pattern matching?

### Frame Problem

Humanos naturalmente know what is and isn't relevant in a situation. Computadores struggle with determining what information is relevant.

### The Building Blocks Question

Não sabemos what we need to build AGI:

- Transformers são suficientes com mais scale?
- Precisamos de novas arquiteturas?
- Integração de simbolismo e conexionismo?
- Algo completamente diferente?

## Abordagens para AGI

### Scaling Current Approaches

Hipótese: Transformers + mais dados + mais compute = AGI.

**Arguments for:**
- Language, vision, code all solved by similar architectures
- Emergent capabilities at scale
- Diminishing returns not seen yet

**Arguments against:**
- Pure statistical learning may have limits
- Missing something fundamental
- Physical grounding lacking

### Neurociência Inspirada

Understanding how the brain works and duplicating it:

- spiking neural networks
- Memory systems (hippocampus)
- Attention mechanisms

### Hybrid Approaches

Combinando múltiplas técnicas:

- Symbolic AI + neural networks
- Knowledge graphs + embeddings
- Classical planning + learning

### Whole Brain Emulation

Scan brain em nível细致 and simulate digitally:

- Connectomics: map all neural connections
- Simulation: run on computer
- Extremely ambitious, requires technology that doesn't exist yet

## Marcos e Definições

### Marcos Típicos

| Marco | Descrição |
|-------|-----------|
| **Narrow Superhuman** | Supera humanos em todas as tarefas narrow |
| **Reasoning** | Capaz de research autonomously |
| **Learning** | Learns any skill from experience |
| **Autonomy** | Can pursue open-ended goals |
| **General** | Equivalente a humano médio |

### Problemas de Definição

Não há consensus:

- O que significa "equivalente a humano"?
- Teste de Turing é suficiente?
- Devemos measure outcomes or process?
- Humano médio or genius?

## Timeline: Quando?

Opiniões variam wildly:

**Próximos 5-10 anos:**
- Kurzweil (Google): 2029
- Some researchers: AGI by 2030

**10-20 anos:**
- OpenAI's Sam Altman: "significantly" by 2030s
- DeepMind's Demis Hassabis: 2030s-2040s

**Nunca / muito mais longe:**
- Yoshua Bengio: ainda décadas de distância
- Many AI researchers: unknown, possibly never

**Incerteza:**
Experts admit not knowing. Could be 5 years or 500.

## Implicações de AGI

### Positivas

- **Scientific discovery**: Milhares de hipóteses testadas
- **Pobreza**: Automation de trabalho tedioso
- **Conhecimento**: Education personalizada para todos
- **Riscos globais**: Climate, pandemics, asteroids

### Negativas / Riscos

**Existential risk:**
Se AGI is misaligned with human values:
- Could pursue goals harmful to humanity
- Hard to control once superintelligent

**Economic disruption:**
Automation of cognitive work could displace billions.

**Weaponization:**
AGI optimized for harmful goals.

## Alinhamento (Alignment)

O problema central: how to ensure AGI's goals align with human values.

### O Problema

Specifying human values precisely is hard:
- Incomplete specifications
- Specification gaming
- Corrigibility: can we turn it off if needed?

### Abordagens

- **RLHF**: Learn from human feedback
- **Constitutional AI**: Learn from principles
- **Interpretability**: Understand what it's doing
- **Formal verification**: Prove properties of systems

## O Debate Atual

### Bostrom (Superinteligência, 2014)

> "The first superintelligent AI will be the last invention humanity needs to make."

Preocupação com controle e alinhamento.

### Russell (Human Compatible, 2019)

Three principles for beneficial machines:
1. Be purely altruistic
2. Learn human values by observation
3. Uncertain about human values

### Yudkowsky (MIRI, etc.)

AI alignment is the most important problem, and we're not ready.

### LeCun, Bengio (Meta AI)

AGI is possible but not imminent. Current approaches can get us there.

## O Que Podemos Fazer

### Agora

- Desenvolver alinhamento e interpretability
- Governança e regulations
- Pensar about values and goals
- Desenvolver IA narrow responsibly

### A Longo Prazo

- Preparar society for changes
- Distributed benefits
- International cooperation
- Safety research

---

**Série: IA Avançada**
1. [AGI: Inteligência Artificial Geral]({{ site.baseurl }}/agi-inteligencia-artificial-geral) ← *você está aqui*
2. [Ética em IA: Vieses e Responsabilidade]({{ site.baseurl }}/etica-em-ia-vieses-e-responsabilidade)

## Leia Mais

- Bostrom, N. *Superinteligência*. Intrínseca, 2018.
- Russell, S. *Human Compatible*. Viking, 2019.
- Yudkowsky, E. "Aligning a superintelligent AGI". *Medium*, 2022.
- Müller, V. & Bostrom, N. "Future Progress in AI". *In: Springer*, 2016.
- Grace, K. et al. "When Will AI Exceed Human Performance?". *JAIR*, 2018.
