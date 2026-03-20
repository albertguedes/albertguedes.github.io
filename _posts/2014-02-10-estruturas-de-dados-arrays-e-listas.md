---
layout: post
title: "Estruturas de Dados: Arrays e Listas"
description: "Conheça as estruturas de dados mais fundamentais da programação e quando usar cada uma."
date: 2014-02-10
---

Se os algoritmos são os passos para resolver problemas, as **estruturas de dados** são os containers que armazenam e organizam as informações que esses algoritmos processam. Escolher a estrutura de dados correta pode ser a diferença entre um programa que roda em milissegundos e um que leva horas.

## O que são Estruturas de Dados?

Uma **estrutura de dados** é uma forma organizada de armazenar e gerenciar dados para que possam ser acessados e modificados eficientemente. Diferentes estruturas são otimizadas para diferentes operações.

A escolha da estrutura certa depende de:
- Que operações você precisa realizar com frequência
- O tamanho dos seus dados
- Requisitos de performance

## Arrays (Vetores)

O **array** (ou vetor) é a estrutura de dados mais fundamental e comum.

### Características

- Elementos armazenados em posições de memória contínuas
- Acesso direto por índice (posição)
- Tamanho fixo na maioria das linguagens (exceto linguagens dinâmicas)

### Representação Visual

```
Índice:    [0]    [1]    [2]    [3]    [4]
Valor:     10     25     37     42     58
```

### Operações

| Operação | Complexidade | Descrição |
|----------|--------------|----------|
| Acesso | O(1) | Acessar elemento por índice |
| Busca | O(n) | Procurar elemento |
| Inserção | O(n) | Inserir no meio |
| Remoção | O(n) | Remover do meio |

### Vantagens e Desvantagens

**Vantagens:**
- Acesso extremamente rápido por índice
- Memória contígua, cache-friendly
- Simples de implementar

**Desvantagens:**
- Tamanho fixo (em linguagens tradicionais)
- Inserção/remoção custosa no meio

### Arrays Multidimensionais

Arrays podem ter múltiplas dimensões:

```python
# Array 2D (matriz)
matriz = [
    [1, 2, 3],
    [4, 5, 6],
    [7, 8, 9]
]
```

## Listas Encadeadas (Linked Lists)

A **lista encadeada** resolve a limitação de tamanho fixo do array usando nós dispersos em memória, conectados por ponteiros.

### Estrutura de um Nó

```
[Nó]
┌─────┬──────┐
│Dado │Próx  │
└─────┴──────┘
   ↓
[Nó] ─→ [Nó] ─→ [Nó] ─→ null
```

### Tipos de Listas

1. **Lista Encadeada Simples**: Cada nó aponta para o próximo
2. **Lista Duplamente Encadeada**: Cada nó aponta para próximo e anterior
3. **Lista Circular**: Último nó aponta para o primeiro

### Operações

| Operação | Complexidade | Descrição |
|----------|--------------|----------|
| Acesso | O(n) | Precisa percorrer |
| Inserção | O(1) | No início ou fim |
| Remoção | O(1) | No início ou fim |
| Busca | O(n) | Procurar elemento |

### Vantagens e Desvantagens

**Vantagens:**
- Tamanho dinâmico
- Inserção/remoção eficiente no início/fim

**Desvantagens:**
- Acesso sequencial (não direto por índice)
- Mais memória por elemento (armazenar ponteiros)
- Cache-unfriendly

## Quando Usar Cada Uma

### Use Array Quando:
- Você precisa de acesso rápido por índice
- O tamanho dos dados é conhecido antecipadamente
- Inserções/remoções no meio são raras

### Use Lista Encadeada Quando:
- O tamanho dos dados varia frequentemente
- Você insere/remove elementos frequentemente no início
- Memória fragmentada está disponível

## Implementação em Pseudocódigo

### Array

```
criar_array(tamanho):
    return alocar(tamanho)

aceder_elemento(array, índice):
    se índice < 0 ou índice >= tamanho(array):
        erro "Índice fora dos limites"
    return array[índice]
```

### Lista Encadeada

```
criar_lista():
    cabeça = null
    return cabeça

inserir_no_início(lista, valor):
    novo_nó = criar_nó(valor)
    novo_nó.próximo = lista
    return novo_nó

percorrer(lista):
    atual = lista
    enquanto atual != null:
        processar(atual.dado)
        atual = atual.próximo
```

## Outras Variantes

### Dynamic Arrays (ArrayLists)

Algumas linguagens oferecem arrays de tamanho dinâmico (Java ArrayList, Python list). Eles combinam benefícios de arrays e listas:

- Acesso por índice O(1)
- Inserção O(1) amortizado
- Duplicam tamanho quando lotam

### Stacks e Queues

Estruturas especializadas derivadas de arrays/listas:

- **Stack (Pilha)**: LIFO (último a entrar, primeiro a sair)
- **Queue (Fila)**: FIFO (primeiro a entrar, primeiro a sair)

---

**Série: Fundamentos da Programação**
1. [Lógica de Programação para Iniciantes]({{ site.baseurl }}/logica-de-programacao-para-iniciantes)
2. [O que é um Algoritmo?]({{ site.baseurl }}/o-que-e-um-algoritmo)
3. [Estruturas de Dados: Arrays e Listas]({{ site.baseurl }}/estruturas-de-dados-arrays-e-listas) ← *você está aqui*

## Leia Mais

- Cormen, T. H. et al. *Algoritmos: Teoria e Prática*. 3ª Ed. Elsevier, 2012.
- Sedgewick, R. & Wayne, K. *Algorithms*. 4ª Ed. Addison-Wesley, 2011.
- Goodrich, M. T. & Tamassia, R. *Estruturas de Dados e Algoritmos em Java*. Bookman, 2013.
- Ziviani, N. *Projeto de Algoritmos com Implementações em Java e C++*. 2ª Ed. Cengage, 2011.
