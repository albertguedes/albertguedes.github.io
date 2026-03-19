---
layout: post
title: "Cálculo Diferencial: Uma Introdução"
description: "Entenda derivadas, taxas de variação e como calcular a inclinação de curvas."
date: 2017-04-15
---

**Cálculo diferencial** é o ramo do cálculo concerned with rates of change e slopes of curves. É fundamental para física, engenharia, economia e especialmente machine learning — onde usamos derivatives para otimizar modelos.

## A Ideia Fundamental

### Problema da Tangente

Qual é a inclinação de uma curva em um ponto?

```
       /
      /
     /
    /
   /______
```

A inclinação de uma reta é Δy/Δx. Mas para uma curva, isso muda de ponto para ponto.

### Limites (Limits)

Antes de derivatives, precisamos de limits:

```
lim(x→a) f(x) = L
```

O valor que f(x) se aproxima quando x se aproxima de a.

```python
# Symbolic computation
from sympy import limit, Symbol
x = Symbol('x')
limit(x**2, x, 2)  # 4
```

### Continuidade

Uma função é contínua se:

1. f(a) exists
2. lim(x→a) f(x) exists
3. lim(x→a) f(x) = f(a)

## A Derivada

### Definição

A derivative is the limit of the difference quotient:

```
f'(x) = lim(Δx→0) [f(x+Δx) - f(x)] / Δx
```

É a taxa instantânea de mudança — como y muda quando x changes.

### Interpretações

1. **Inclinação da tangente**: geometric interpretation
2. **Taxa de variação**: "por unidade de x, y varia tanto"
3. **Velocidade instantânea**: se y é posição, f'(x) é velocidade

### Notações

```
f'(x)          (Lagrange)
df/dx          (Leibniz)
Dxf            (Newton)
```

## Regras de Derivação

### Constante

```
d/dx [c] = 0
```

### Potência

```
d/dx [xⁿ] = n × xⁿ⁻¹
```

### Multiplicação por Constante

```
d/dx [c × f(x)] = c × f'(x)
```

### Soma

```
d/dx [f + g] = f' + g'
```

### Produto (Regra do Produto)

```
d/dx [f × g] = f'g + fg'
```

### Quociente (Regra do Quociente)

```
d/dx [f/g] = (f'g - fg') / g²
```

### Cadeia (Regra da Cadeia)

Para composed functions f(g(x)):

```
d/dx [f(g(x))] = f'(g(x)) × g'(x)
```

## Derivadas Comuns

| Função | Derivada |
|--------|----------|
| xⁿ | nxⁿ⁻¹ |
| sin(x) | cos(x) |
| cos(x) | -sin(x) |
| eˣ | eˣ |
| ln(x) | 1/x |
| logₐ(x) | 1/(x ln(a)) |

## Aplicações

### Otimização

Encontrar maximum ou minimum de funções:

```
f'(x) = 0 → pontos críticos
f''(x) > 0 → mínimo local
f''(x) < 0 → máximo local
```

**Exemplo:** Maximizar área given perimeter.

### Máquinas

Em ML, usamos derivatives para gradient descent:

```
θ = θ - α × ∂J/∂θ
```

Where J is the loss function.

### Física

- **Velocidade**: derivative da posição
- **Aceleração**: derivative da velocidade
- **Força**: derivative do momento

## Regras de L'Hôpital

Para limits of indeterminate forms (0/0 ou ∞/∞):

```
lim f(x)/g(x) = lim f'(x)/g'(x)
```

Apply repeatedly until you get determinate form.

## Derivadas Parciais

Para funções com múltiplas variáveis:

```
f(x, y) = x² + xy + y²

∂f/∂x = 2x + y
∂f/∂y = x + 2y
```

Mantém outras variáveis constantes.

**Importante em ML:**
- Gradients são vetores de derivadas parciais
- Usamos para otimizar loss functions multivariable

## Gradiente

O vector of partial derivatives:

```
∇f = (∂f/∂x₁, ∂f/∂x₂, ..., ∂f/∂xₙ)
```

**Propriedades:**
- Aponta na direção de maior aumento
- Perpendicular to level curves/surfaces

## Taylor Series

Aproximar funções usando derivatives:

```
f(x) ≈ f(a) + f'(a)(x-a) + f''(a)(x-a)²/2! + ...
```

Used para:
- Function approximation
- Numerical methods
- Understanding optimization landscapes

---

**Série: Matemática**
1. [Cálculo Diferencial: Uma Introdução]({{ site.baseurl }}/calculo-diferencial-uma-introducao) ← *você está aqui*

## Leia Mais

- Stewart, J. *Cálculo*. Vol. 1. 8ª Ed. Cengage, 2017.
- Thomas, G. B. *Cálculo*. Vol. 1. 12ª Ed. Pearson, 2012.
- Apostol, T. M. *Calculus*. 2nd Ed. Wiley, 1967.
- Khan Academy. *Differential Calculus*.
