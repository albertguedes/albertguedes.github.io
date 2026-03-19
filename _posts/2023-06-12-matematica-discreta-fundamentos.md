---
layout: post
title: "Matemática Discreta: Fundamentos"
description: "Explore os conceitos matemáticos essenciais para ciência da computação."
date: 2023-06-12
---

**Matemática discreta** é o estudo de estruturas matemáticas que são fundamentally discrete (contáveis), opposed to continuous. É a linguagem mathematical da ciência da computação.

## Por que Discreta?

Computadores são discretos:
- Bits: 0 ou 1
- Integers vs real numbers
- Logic: true ou false

### Contínuo vs Discreto

| Contínuo | Discreto |
|-----------|----------|
| Números reais | Números inteiros |
| Curvas suaves | Grafos |
| Integração | Somatórios |
| Cálculo | Lógica |

## Lógica Proposicional

### Proposições

Afirmações que são verdadeiras ou falsas:

```
p: "2 + 2 = 4"  (verdadeiro)
q: "π = 3"       (falso)
```

### Operadores Lógicos

**E (∧):** Ambas verdadeiras
```
V ∧ V = V, V ∧ F = F, F ∧ F = F
```

**OU (∨):** Pelo menos uma verdadeira
```
V ∨ V = V, V ∨ F = V, F ∨ F = F
```

**NÃO (¬):** Inverte
```
¬V = F, ¬F = V
```

**IMPLICA (→):**
```
V → V = V, V → F = F, F → V = V, F → F = V
```

### Tabelas Verdade

Úteis para verificar equivalências e tautologias.

### Equivalências

```
¬(¬p) = p (dupla negação)
¬(p ∧ q) = ¬p ∨ ¬q (De Morgan)
¬(p ∨ q) = ¬p ∧ ¬q (De Morgan)
```

## Teoria dos Grafos

### O que é um Grafo?

```
G = (V, E)
```

- **V**: Conjunto de vértices (nodes)
- **E**: Conjunto de arestas (edges)

```
    A --- B
   /|     |
  C |     D
   \|     |
    ------
```

### Tipos

**Direcionado:** Arestas têm direção
**Não-direcionado:** Sem direção
**Ponderado:** Arestas têm pesos
**Cíclico:** Contém ciclos
**Acíclico:** Sem ciclos

### Aplicações

- Redes sociais (amizades)
- Internet (links entre páginas)
- GPS (rotas entre lugares)
- Scheduling (dependências)

## Combinatória

### Princípios Básicos

**Adição:**
Se A e B são disjoint, |A ∪ B| = |A| + |B|

**Multiplicação:**
Se há m ways para A e n ways para B, há m × n ways.

### Permutações

Ordem importa:

```
P(n,r) = n! / (n-r)!
```

**Exemplo:** Quantas ways de arrange 3 people em 5 cadeiras?

```
P(5,3) = 5! / 2! = 60
```

### Combinações

Ordem não importa:

```
C(n,r) = n! / (r!(n-r)!)
```

**Exemplo:** Quantas ways de choose 3 people de 5?

```
C(5,3) = 5! / (3!2!) = 10
```

## Princípio da Inclusão-Exclusão

Para contar uniões de conjuntos:

```
|A ∪ B| = |A| + |B| - |A ∩ B|
```

Para 3 conjuntos:

```
|A ∪ B ∪ C| = |A| + |B| + |C| 
            - |A∩B| - |A∩C| - |B∩C| 
            + |A∩B∩C|
```

## Relaciones

### Propriedades

Para R on A:

- **Reflexiva:** (a,a) ∈ R for all a
- **Simétrica:** (a,b) ∈ R → (b,a) ∈ R
- **Transitiva:** (a,b) ∈ R e (b,c) ∈ R → (a,c) ∈ R

### Relações de Equivalência

Relações que são reflexivas, simétricas e transitivas.

**Exemplo:** Congruência módulo n
- Reflexiva: a ≡ a (mod n)
- Simétrica: a ≡ b → b ≡ a
- Transitiva: a ≡ b e b ≡ c → a ≡ c

## Indução Matemática

### Princípio

Para provar P(n) for all n ≥ n₀:

1. **Base:** Prove P(n₀)
2. **Inductive step:** Assuma P(k) é verdade, prove P(k+1)

### Exemplo

Prove: 1 + 2 + ... + n = n(n+1)/2

**Base:** n=1: 1 = 1(2)/2 = 1 ✓

**Step:** Assuma true for k:
```
1 + ... + k = k(k+1)/2
```
Prove for k+1:
```
1 + ... + k + (k+1) = k(k+1)/2 + (k+1)
= (k+1)(k/2 + 1)
= (k+1)(k+2)/2
= (k+1)((k+1)+1)/2 ✓
```

## Recursão

### Definindo Functions Recursively

```
f(0) = 0
f(n) = f(n-1) + n
```

Isto define f(n) = n(n+1)/2.

### Recursão em Estruturas

```python
def fib(n):
    if n <= 1:
        return n
    return fib(n-1) + fib(n-2)
```

### Resolução de Recorrências

**Método de guess:**
1. Guess a forma (ex: c × 2ⁿ)
2. Verifique substitution
3. Encontre constants

## Teoria dos Números (Básico)

### Divisibilidade

```
a divides b: a | b if b = k × a for some integer k
```

### Algoritmo da Divisão

Para a, b > 0, existem únicos q, r such that:

```
a = q × b + r, 0 ≤ r < b
```

### MDC e MMC

**MDC:** Maior divisor comum
**MMC:** Mínimo múltiplo comum

```
MDC(a,b) × MMC(a,b) = a × b
```

### Algoritmo de Euclides

Para encontrar MDC efficiently:

```
MDC(a, 0) = a
MDC(a, b) = MDC(b, a mod b)
```

```python
def mdc(a, b):
    while b:
        a, b = b, a % b
    return a
```

## Árvores e Estruturas de Dados

### Árvores

Grafos acíclicos conectados:

- **Rooted trees:** Uma raiz designated
- **Binary trees:** Cada nó tem ≤ 2 children
- **Binary search trees:** Left < parent < right

### Propriedades de Árvores

Para árvore com n vértices:
- Se rooted, há n-1 edges
- Árvore binária completa de altura h tem ≤ 2^(h+1) - 1 nós

---

**Série: Matemática** (relacionado)
1. [Álgebra Linear: Vetores e Matrizes]({{ site.baseurl }}/algebra-linear-vetores-e-matrizes)
2. [Probabilidade: Conceitos Básicos]({{ site.baseurl }}/probabilidade-conceitos-basicos)
3. [Matemática Discreta: Fundamentos]({{ site.baseurl }}/matematica-discreta-fundamentos) ← *você está aqui*

## Leia Mais

- Rosen, K. H. *Matemática Discreta e suas Aplicações*. 8ª Ed. McGraw-Hill, 2019.
- Epp, S. S. *Discrete Mathematics with Applications*. 4th Ed. Cengage, 2011.
- Cormen, T. H. et al. *Algoritmos: Teoria e Prática*. 3ª Ed. Elsevier, 2012.
- Lehman, E., Leighton, F. T. & Meyer, A. R. *Mathematics for Computer Science*. MIT, 2017.
