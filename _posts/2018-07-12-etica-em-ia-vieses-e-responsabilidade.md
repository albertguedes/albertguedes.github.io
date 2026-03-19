---
layout: post
title: "Ética em IA: Vieses e Responsabilidade"
description: "Explore os desafios éticos da inteligência artificial, de vieses algorítmicos a responsabilidade."
date: 2018-07-12
---

À medida que sistemas de IA assumem decisões cada vez mais importantes — de quem recebe crédito a quem é contratado, de diagnósticos médicos a decisões judiciais — as questões éticas se tornam urgentes. Como garantimos que esses sistemas sejam justos, transparentes e responsáveis?

## O Problema dos Vieses Algorítmicos

### O que são Vieses?

Vieses algorítmicos são padrões sistemáticos e injustos que aparecem em sistemas de ML, resultando em decisões que desfavorecem certos grupos.

### Origens dos Vieses

**1. Dados de Treino Biasados**
```
Dados históricos reflectem discriminação passada
    ↓
Modelo aprende esses padrões
    ↓
Reproduz e amplifica viés
```

Exemplo: Se historicamente homens foram mais contratados para vagas de tecnologia, um modelo de recrutamento pode aprender a penalizar currículos femininos.

**2. Features Proxy**
即使 não usamos race diretamente, variáveis correlated with race (código postal, nome da escola) can serve as proxies.

**3. Viés de Confirmação em Desenvolvimento**
Desenvolvedores, muitas vezes sem diversidade, podem não identificar situações onde o sistema falha para certos grupos.

### Exemplos Reais

**COMPAS (Justiça Criminal)**
Sistema usado em tribunais americanos para predizer risco de recidiva. Estudos encontraram que falsos positivos (pessoas classificadas como alto risco que não reincidiram) eram mais comuns para réus negros.

**Amazon's Recruiting Tool**
Sistema de recrutamento que penalizava currículos com a palavra "women's" e graduates de faculdades só de mulheres. Desenvolvido predominantly by men, não identificou esse padrão.

**Reconhecimento Facial**
Sistemas de reconhecimento facial têm taxas de erro significativamente maiores para pessoas com pele escura, especialmente mulheres. Treinados majoritariamente com rostos claros.

## Dimensões de Justo

### Fairness não é único conceito

Multiple mathematical definitions of fairness conflict with each other. Escolher qual usar é uma decisão ética.

**1. Fairness through Awareness**
Tratar pessoas igualmente, mas considerar diferenças relevantes (like when offering a wheelchair to someone who needs it).

**2. Fairness through Unawareness**
Ignorar protected attributes entirely. Problema: mesmo ignorando, features correlated podem encode viés.

**3. Equalized Odds**
Mesma taxa de verdadeiros positivos e falsos positivos across groups.

**4. Predictive Parity**
Mesma accuracy preditiva across groups.

**Impossibility Theorem (Chouldechova, 2017)**
Não é possível satisfying all fairness criteria simultaneously in most cases. Trade-offs são inevitáveis.

## Transparência e Explicabilidade

### Por que Explicabilidade Importa?

- **Accountability**: Quando uma decisão afeta alguém, essa pessoa pode questionar a decisão
- **Debugging**: É mais fácil identificar e corrigir problemas
- **Trust**: Usuários confiam mais em sistemas que entendem

### O Problema da Caixa Preta

Redes neurais profundas são altamente não-lineares e complexas. É fundamentalmente difícil saber exactly why they made a specific decision.

### Abordagens

**SHAP (SHapley Additive exPlanations)**
Baseado em teoria de jogos, calcula a contribuição de cada feature para uma predição.

**LIME (Local Interpretable Model-agnostic Explanations)**
Aproxima o modelo complexo por um interpretável localmente around the prediction.

**Attention Maps (para CNNs e Transformers)**
Visualizam em quais partes da imagem/input o modelo está focando.

## Responsabilidade

### Quem é Responsável?

Quando um sistema de IA causa dano, quem é responsável?

- **Desenvolvedor**: Criou o sistema
- **Empresa**: Deployou e mantém
- **Usuário**: Usou de forma inapropriada
- **Regulador**: Não criou salvaguardas adequadas

### Frameworks de Responsabilidade

**1. accountability through tracking**
Manter logs detalhados de decisões para auditoria posterior.

**2. meaningful human control**
Garantir que humanos possam override decisões automatizadas.

**3. duty to explain**
Obrigação legal ou ética de explicar decisões que afetam individuals.

## Viés na Linguagem

### Modelos de Linguagem

LLMs treinados em billions de textos da internet absorvem:
- Esteréótipos de gênero
- Preconceitos raciais
- Informações falsas
- Discurso de ódio

**Exemplo**: "Doctor" association with male pronouns em modelos pré-treino.

### Mitigation

- Debiasing nos dados de treino
- Fine-tuning com dados mais equilibrados
- RLHF (Reinforcement Learning from Human Feedback)
- Constitutional AI

## O Futuro: IA Responsável

### Princípios Emergentes

- **Privacy by design**: Proteção de dados desde o início
- **Fairness through testing**: Testes rigorosos em grupos diversos
- **Human-in-the-loop**: Supervisão humana em decisões críticas
- **Algorithmic auditing**: Auditorias independientes

### Regulação Crescente

- **EU AI Act (2024)**: Classifica sistemas por risco, with requirements proporcionais
- **Brazil's LGPD**: Regras para uso de dados pessoais
- **NIST AI Risk Management Framework**: Guidelines for AI governance

## O que Podemos Fazer?

### Como Desenvolvedores

1. Priorizar diversity em times
2. Testar sistematicamente em grupos diversos
3. Documentar limitações Known
4. Implementar monitoramento contínuo
5. Criar canais de feedback para afetados

### Como Usadores

1. Questione decisões automatizadas
2. Report quando encontrar discriminação
3. Apoie transparência
4. Eduque-se sobre como ML funciona

---

**Série: IA e Sociedade**
1. [Ética em IA: Vieses e Responsabilidade]({{ site.baseurl }}/etica-em-ia-vieses-e-responsabilidade) ← *você está aqui*
2. [O Futuro da IA: Tendências e Desafios]({{ site.baseurl }}/o-futuro-da-ia-tendencias-e-desafios)
3. [IA na Saúde e Educação]({{ site.baseurl }}/ia-na-saude-e-educacao)

## Leia Mais

- O'Neil, C. * Weapons of Math Destruction*. Crown, 2016.
- Noble, S. U. *Algorithms of Oppression*. NYU Press, 2018.
- Crawford, K. *The Atlas of AI*. Yale UP, 2021.
- Floridi, L. et al. "AI4People—An Ethical Framework for a Good AI Society". *Minds and Machines*, 2018.
- EU AI Act. European Commission, 2024.
