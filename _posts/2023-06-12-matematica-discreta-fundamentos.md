---
layout: post
title: "Matemática Discreta: Fundamentos"
description: "Explore os conceitos matemáticos essenciais para ciência da computação."
date: 2023-06-12
---

**Matemática discreta** é o estudo de estruturas matemáticas que são fundamentalmente discretas (contáveis), ao invés de contínuas. É a linguagem matemática da ciência da computação.

## Por que Discreta?

Computadores são discretos:
- Bits: 0 ou 1
- Inteiros vs números reais
- Lógica: verdadeiro ou falso

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

```text
p: "2 + 2 = 4"  (verdadeiro)
q: "π = 3"       (falso)
```

### Operadores Lógicos

**E (∧):** Ambas verdadeiras
```text
V ∧ V = V, V ∧ F = F, F ∧ F = F
```

**OU (∨):** Pelo menos uma verdadeira
```text
V ∨ V = V, V ∨ F = V, F ∨ F = F
```

**NÃO (¬):** Inverte
```text
¬V = F, ¬F = V
```

**IMPLICA (→):**
```text
V → V = V, V → F = F, F → V = V, F → F = V
```

### Tabelas Verdade

Úteis para verificar equivalências e tautologias.

### Equivalências

```text
¬(¬p) = p (dupla negação)
¬(p ∧ q) = ¬p ∨ ¬q (De Morgan)
¬(p ∨ q) = ¬p ∧ ¬q (De Morgan)
```

## Teoria dos Grafos

### O que é um Grafo?

```text
G = (V, E)
```

- **V**: Conjunto de vértices (nodes)
- **E**: Conjunto de arestas (edges)

```text
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
Se A e B são disjuntos, \(|A \cup B| = |A| + |B|\)

**Multiplicação:**
Se há m maneiras para A e n maneiras para B, há \(m \times n\) maneiras.

### Permutações

Ordem importa:

```text
P(n,r) = n! / (n-r)!
```

**Exemplo:** Quantas maneiras de arranjar 3 pessoas em 5 cadeiras?

```text
P(5,3) = 5! / 2! = 60
```

### Combinações

Ordem não importa:

```text
C(n,r) = n! / (r!(n-r)!)
```

**Exemplo:** Quantas maneiras de escolher 3 pessoas de 5?

```text
C(5,3) = 5! / (3!2!) = 10
```

## Princípio da Inclusão-Exclusão

Para contar uniões de conjuntos:

```text
|A ∪ B| = |A| + |B| - |A ∩ B|
```

Para 3 conjuntos:

```text
|A ∪ B ∪ C| = |A| + |B| + |C| 
             - |A∩B| - |A∩C| - |B∩C| 
             + |A∩B∩C|
```

## Relaciones

### Propriedades

Para R on A:

- **Reflexiva:** \((a,a) \in R\) para todo a
- **Simétrica:** \((a,b) \in R \rightarrow (b,a) \in R\)
- **Transitiva:** \((a,b) \in R\) e \((b,c) \in R \rightarrow (a,c) \in R\)

### Relações de Equivalência

Relações que são reflexivas, simétricas e transitivas.

**Exemplo:** Congruência módulo n
- Reflexiva: \(a \equiv a \pmod{n}\)
- Simétrica: \(a \equiv b \rightarrow b \equiv a\)
- Transitiva: \(a \equiv b\) e \(b \equiv c \rightarrow a \equiv c\)

## Indução Matemática

### Princípio

Para provar P(n) para todo \(n \geq n_0\):

1. **Base:** Prove \(P(n_0)\)
2. **Inductive step:** Assuma \(P(k)\) é verdade, prove \(P(k+1)\)

### Exemplo

Prove: \(1 + 2 + ... + n = n(n+1)/2\)

**Base:** n=1: \(1 = 1(2)/2 = 1\) ✓

**Passo:** Assuma verdadeiro para k:
```text
1 + ... + k = k(k+1)/2
```
Prove para k+1:
```text
1 + ... + k + (k+1) = k(k+1)/2 + (k+1)
= (k+1)(k/2 + 1)
= (k+1)(k+2)/2
= (k+1)((k+1)+1)/2 ✓
```

## Recursão

### Definindo Functions Recursively

```text
f(0) = 0
f(n) = f(n-1) + n
```

Isto define \(f(n) = n(n+1)/2\).

### Recursão em Estruturas

```python
def fib(n):
    if n <= 1:
        return n
    return fib(n-1) + fib(n-2)
```

### Resolução de Recorrências

**Método de guess:**
1. Adivinhe a forma (ex: \(c \times 2^n\))
2. Verifique substituição
3. Encontre constantes

## Teoria dos Números (Básico)

### Divisibilidade

```text
a divide b: a | b se b = k × a para algum inteiro k
```

### Algoritmo da Divisão

Para a, b > 0, existem únicos q, r tais que:

```text
a = q × b + r, 0 ≤ r < b
```

### MDC e MMC

**MDC:** Maior divisor comum
**MMC:** Mínimo múltiplo comum

```text
MDC(a,b) × MMC(a,b) = a × b
```

### Algoritmo de Euclides

Para encontrar MDC eficientemente:

```text
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

- **Rooted trees:** Uma raiz designada
- **Binary trees:** Cada nó tem ≤ 2 filhos
- **Binary search trees:** Esquerda < pai < direita

### Propriedades de Árvores

Para árvore com n vértices:
- Se rooted, há n-1 arestas
- Árvore binária completa de altura h tem \(\leq 2^{h+1} - 1\) nós

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
