---
layout: post
title: "Álgebra Linear: Vetores e Matrizes"
description: "Conheça os fundamentos da álgebra linear, essencial para machine learning e computação gráfica."
date: 2016-09-08
---

**Álgebra linear** é a matemática de espaços multidimensionais. É fundamental para machine learning, computação gráfica, física, engenharia e muitas outras áreas. Entender vetores e matrizes é essencial para quem trabalha com dados.

## Vetores

### O que é um Vetor?

Um **vetor** é uma quantidade com magnitude e direção:

```
→  = (3, 4)  em 2D
v
```

Pode ser pensado como:
- Um ponto no espaço
- Uma seta do origem ao ponto
- Uma lista ordenada de números

### Representação

```python
import numpy as np

# Vetor coluna
v = np.array([3, 4])
print(v.shape)  # (2,)
```

### Operações

**Adição:**
```
(1, 2) + (3, 4) = (4, 6)
```

**Multiplicação por escalar:**
```
2 × (3, 4) = (6, 8)
```

**No NumPy:**
```python
a = np.array([1, 2])
b = np.array([3, 4])
print(a + b)  # [4, 6]
print(2 * a)  # [2, 4]
```

## Norma (Comprimento)

O comprimento (magnitude) de um vetor:

```
||v|| = √(x² + y² + ...)
```

```python
np.linalg.norm(v)  # 5.0 for v = [3, 4]
```

## Produto Escalar (Dot Product)

Multiplica componentes correspondentes e soma:

```
a · b = a₁b₁ + a₂b₂ + ...
```

**Exemplo:**
```
(1, 2) · (3, 4) = 1×3 + 2×4 = 11
```

**Interpretações:**
- Mede alinhamento entre vetores
- Útil para similaridade
- Base para projeção

```python
np.dot(a, b)  # 11
# ou
a @ b         # 11
```

### Ângulo Entre Vetores

```
cos(θ) = (a · b) / (||a|| × ||b||)
```

- **θ = 0°**: paralelo, produto escalar máximo
- **θ = 90°**: ortogonal, produto escalar = 0
- **θ = 180°**: oposto, mais negativo

## Matrizes

### O que é uma Matriz?

Matriz é uma tabela de números organizados em linhas e colunas:

```
┌ ┌     ┐┐
││ 1  2 ││
││ 3  4 ││
└└     ┘┘
  2×2 matrix
```

```python
A = np.array([[1, 2],
              [3, 4]])
```

### Operações

**Adição:** Soma elementos correspondentes
**Multiplicação por escalar:** Cada elemento
**Transposta:** Linhas viram colunas (Aᵀ)
**Multiplicação:** Mais complexo (veja abaixo)

```python
print(A.T)  # Transposta
```

## Multiplicação de Matrizes

### Regra

Para matrizes A (m×n) e B (n×p), resultado é C (m×p):

```
C[i,j] = sum over k of A[i,k] × B[k,j]
```

**Exemplo 2×2:**

```
┌┌     ┐┐   ┌┌     ┐┐   ┌┌                    ┐┐
││ 1  2 ││ × ││ 5  6 ││ = ││ 1×5+2×7  1×6+2×8 ││
││ 3  4 ││   ││ 7  8 ││   ││ 3×5+4×7  3×6+4×8 ││
└└     ┘┘   └└     ┘┘   └└                    ┘┘
              =    ┌┌           ┐┐
                   ││ 19    22  ││
                   ││ 43    50  ││
                   └└           ┘┘
```

```python
A @ B  # Multiplicação
```

### Propriedades

- **Não comutativa**: A×B ≠ B×A em geral
- **Associativa**: (A×B)×C = A×(B×C)
- **Distributiva**: A×(B+C) = A×B + A×C

## Matriz Identidade

Matriz que age como 1:

```
I = ┌┌     ┐┐
    ││ 1  0 ││
    ││ 0  1 ││
    └└     ┘┘
```

A×I = A

```python
np.eye(3)  # 3×3 identity
```

## Determinante

Escalar derivado de uma matriz:

```
det(A) = ad - bc  for 2×2 matrix [[a, b], [c, d]]
```

**Interpretação:**
- det ≠ 0: Matriz é inversível
- det = 0: Singular, não inversível
- |det|: Fator de escala de volume

```python
np.linalg.det(A)
```

## Matriz Inversa

Matriz que, multiplicada por A, resulta na identidade:

```
A × A⁻¹ = I
```

```python
A_inv = np.linalg.inv(A)
```

Usado para resolver sistemas lineares.

## Sistemas Lineares

### Representação

```
a₁x + b₁y = c₁
a₂x + b₂y = c₂
```

Em forma matricial:

```
┌┌     ┐┐ ┌┌ ┐┐   ┌┌  ┐┐
││ a₁ b₁ ││ ││x││ = ││c₁││
││ a₂ b₂ ││ ││y││   ││c₂││
└└     ┘┘ └└ ┘┘   └└  ┘┘
      A       x       b
```

### Resolver com NumPy

```python
x = np.linalg.solve(A, b)
# ou
x = np.linalg.inv(A) @ b
```

## Autovetores e Autovalores

### Definição

```
A × v = λ × v
```

- **v**: autovetor (eigenvector)
- **λ**: autovalor (eigenvalue)

O vetor que, ao ser multiplicado por A, só é redimensionado, não rotacionado.

### Por que Importam?

- PCA (Principal Component Analysis)
- Sistemas de equações diferenciais
- PageRank
- Compressão de dados

```python
autovalores, autovetores = np.linalg.eig(A)
```

## Aplicações em ML

### Regressão Linear

```
y = Xβ

Solving: β = (XᵀX)⁻¹Xᵀy
```

### Redes Neurais

- Weights são matrizes
- Forward pass: matrix multiplications
- Backpropagation: gradients via álgebra linear

### PCA

Encontra componentes principais (autovetores da matriz de covariância) para redução de dimensionalidade.

### Embeddings

Palavras/documentos como vetores em espaço de alta dimensionalidade. Operações capturam relacionamentos semânticos.

---

**Série: Matemática**
1. [Álgebra Linear: Vetores e Matrizes]({{ site.baseurl }}/algebra-linear-vetores-e-matrizes) ← *você está aqui*

## Leia Mais

- Strang, G. *Álgebra Linear e suas Aplicações*. 4ª Ed. Cengage, 2014.
- Poole, D. *Álgebra Linear*. 3ª Ed. Cengage, 2011.
- Lang, S. *Introduction to Linear Algebra*. 2nd Ed. Springer, 2003.
- Khan Academy. *Linear Algebra*.
