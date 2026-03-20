---
layout: post
title: "Raciocínio Baseado em Regras"
description: "Entenda sistemas especialistas e raciocínio lógico que usam regras SE-ENTÃO."
date: 2014-07-22
---

**Raciocínio baseado em regras** é uma das formas mais antigas e intuitivas de implementar inteligência. Esses sistemas usam **regras SE-ENTÃO** (IF-THEN) para representar conhecimento e fazer inferências, imitando o raciocínio humano através de lógica.

## O que são Sistemas Baseados em Regras?

Sistemas que usam **regras de produção** para representar conhecimento:

```text
SE <condição> ENTÃO <ação>
```

- **Condição**: fatos ou padrões na memória de trabalho
- **Ação**: adicionar fatos, executar operações, modificar estado

### Componentes

1. **Base de Conhecimento**: Conjunto de regras
2. **Working Memory**: Fatos atuais sobre o problema
3. **Motor de Inferência**: Aplica regras aos facts
4. **Interface de Explicação**: Justifica o raciocínio

## Estrutura de Regras

### Regras Simples

```text
SE temperatura > 37.5 ENTÃO febre = verdadeiro
```

### Regras Compostas

```text
SE temperatura > 37.5 E dor_cabeca = verdadeira
ENTÃO possivel_influenza = verdadeiro
```

### Operadores Lógicos

- **E (AND)**: Todas condições devem ser verdadeiras
- **OU (OR)**: Pelo menos uma deve ser verdadeira
- **NÃO (NOT)**: Negação da condição

## Motor de Inferência

### Encadeamento para Frente (Forward Chaining)

Começa dos fatos conhecidos e vai aplicando regras até atingir um objetivo:

```text
Facts iniciais → [Regras aplicáveis] → Novas facts → [Mais regras] → Solução
```

**Exemplo médico:**

```text
1. Facts: paciente.temperatura = 39, paciente.dor_garganta = true
2. Regra: SE temperatura > 38 ENTÃO febre = true
   → Adiciona: febre = true
3. Regra: SE febre = true E dor_garganta = true ENTÃO suspecto_gripe = true
   → Adiciona: suspecto_gripe = true
```

### Encadeamento para Trás (Backward Chaining)

Começa do goal e busca facts que sustentam:

```text
Objetivo → [Que regras podem concluir isso?] → Quais facts preciso? → Perguntar
```

Útil quando há muitas possibilidades mas poucos objetivos.

## Máquina de Inferência em Detalhe

### Ciclo de Execução

```text
1. MATCH: Encontrar todas as regras cujas condições são satisfeitas
2. CONFLICT RESOLUTION: Escolher qual regra executar (se múltiplas)
3. ACT: Executar a ação da regra selecionada
4. Voltar ao passo 1 até não haver regras aplicáveis ou goal atingido
```

### Resolução de Conflitos

Quando múltiplas regras se aplicam:

- **Prioridade**: Regras têm salience ou priority
- **Especificidade**: Regras mais específicas têm preferência
- **Recência**: Fatos mais recentemente adicionados têm precedência
- **Ordem de definição**: Primeira definida, primeira executada

## Exemplo: Sistema de Recomendação de Investimento

### Base de Conhecimento

```prolog
/* Perfil de Risco */
SE idade < 30 E renda_alta = true ENTÃO perfil_agressivo = true
SE idade >= 30 E idade < 50 AND renda_media = true ENTÃO perfil_moderado = true
SE idade >= 50 ENTÃO perfil_conservador = true

/* Alocação de Ativos */
SE perfil_agressivo = true ENTÃO alocar(acoes=80%, Renda_fixa=20%)
SE perfil_moderado = true ENTÃO alocar(acoes=50%, Renda_fixa=40%, caixa=10%)
SE perfil_conservador = true ENTÃO alocar(acoes=20%, Renda_fixa=70%, caixa=10%)

/* Restrições */
SE historico_patrimonial = ruin ENTÃO risco_elevado = true
SE risco_elevado = true ENTÃO NAO recomendar(acoes)
```

### Consulta

```text
Pergunta: Qual alocação para João, 45 anos, renda média, patrimônio OK?
Resposta: Perfil moderado → 50% ações, 40% RF, 10% caixa
```

## Sistemas Especialistas Famosos

### MYCIN (1970s)

Diagnosticar infecções bacterianas:
- Recomendava antibióticos
- Considerava peso do paciente e função renal
- Atingia performance comparável a especialistas humanos

### DENDRAL (1965)

Identificar estrutura molecular de compostos químicos orgânicos.

### XCON (1980)

Configure computers na Digital Equipment Corporation. Economia de $40M anualmente.

## Vantagens

- **Interpretabilidade**: Regras são fáceis de entender e explicar
- **Modularidade**: Cada regra é independente
- **Explicação**: Sistema pode justificar seu raciocínio
- **Desenvolvimento incremental**: Adicionar regras é simples

## Desvantagens

- **Aquisição de conhecimento**: Difícil extrair regras de especialistas
- **Escalabilidade**: Muitas regras podem retardar a inferência
- **Lidando com incerteza**: Dificultoso sem extensões
- **Não aprende**: Precisa ser explicitamente programado

## Extensões

### Fatores de Certeza

```text
SE sintoma = tosse ENTÃO possível_gripe (FC = 0.7)
```

incerteza como números.

### Lógica Fuzzy

Valores contínuos entre 0 e 1:
```text
SE temperatura é ALTA E pressão é BAIXA ENTÃO perigo = MÉDIO
```

### Redes Bayesianas

Modelam probabilidades condicionais entre fatos.

## Hoje: Híbridos

Modernos sistemas combinam:

- **Rules + ML**: Regras para conhecimento explícito, ML para padrões complexos
- **Embedding de conhecimento**: Representar regras como vetores
- **LLMs + RAG**: Retrieval augmented generation com bases de conhecimento

---

**Série: IA Fundamentos**
1. [O que é Inteligência Artificial?]({{ site.baseurl }}/o-que-e-inteligencia-artificial)
2. [Raciocínio Baseado em Regras]({{ site.baseurl }}/raciocinio-baseado-em-regras) ← *você está aqui*
3. [Aprendizado por Reforço: O Básico]({{ site.baseurl }}/aprendizado-por-reforco-o-basico)

## Leia Mais

- Russell, S. & Norvig, P. *Inteligência Artificial*. 3ª Ed. Elsevier, 2013.
- Jackson, P. *Introduction to Expert Systems*. 3rd Ed. Addison-Wesley, 1998.
- Durkin, J. *Expert Systems: Design and Development*. Prentice Hall, 1994.
- Clancey, W. J. "Heuristic Classification". *Artificial Intelligence*, 1985.
