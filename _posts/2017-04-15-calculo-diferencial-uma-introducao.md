---
layout: post
title: "Cálculo Diferencial: Uma Introdução"
description: "Entenda derivadas, taxas de variação e como calcular a inclinação de curvas."
date: 2017-04-15
---

**Cálculo diferencial** é o ramo do cálculo relacionado a taxas de variação e inclinações de curvas. É fundamental para física, engenharia, economia e especialmente machine learning — onde usamos derivadas para otimizar modelos.

## A Ideia Fundamental

### Problema da Tangente

Qual é a inclinação de uma curva em um ponto?

```
       /
      /
     /
    /
   /____
```

A inclinação de uma reta é \(\Delta y / \Delta x\). Mas para uma curva, isso muda de ponto para ponto.

### Limites (Limits)

Antes de derivadas, precisamos de limites:

$$\lim_{x \to a} f(x) = L$$

O valor que f(x) se aproxima quando x se aproxima de a.

```python
# Symbolic computation
from sympy import limit, Symbol
x = Symbol('x')
limit(x**2, x, 2)  # 4
```

### Continuidade

Uma função é contínua se:

1. \(f(a)\) existe
2. \(\lim_{x \to a} f(x)\) existe
3. \(\lim_{x \to a} f(x) = f(a)\)

## A Derivada

### Definição

A derivada é o limite do quociente de diferenças:

$$f'(x) = \lim_{\Delta x \to 0} \frac{f(x+\Delta x) - f(x)}{\Delta x}$$

É a taxa instantânea de mudança — como y muda quando x muda.

### Interpretações

1. **Inclinação da tangente**: interpretação geométrica
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

$$\frac{d}{dx}[c] = 0$$

### Potência

$$\frac{d}{dx}[x^n] = n \times x^{n-1}$$

### Multiplicação por Constante

$$\frac{d}{dx}[c \times f(x)] = c \times f'(x)$$

### Soma

$$\frac{d}{dx}[f + g] = f' + g'$$

### Produto (Regra do Produto)

$$\frac{d}{dx}[f \times g] = f'g + fg'$$

### Quociente (Regra do Quociente)

$$\frac{d}{dx}\left[\frac{f}{g}\right] = \frac{f'g - fg'}{g^2}$$

### Cadeia (Regra da Cadeia)

Para funções compostas \(f(g(x))\):

$$\frac{d}{dx}[f(g(x))] = f'(g(x)) \times g'(x)$$

## Derivadas Comuns

| Função | Derivada |
|--------|----------|
| \(x^n\) | \(n x^{n-1}\) |
| \(\sin(x)\) | \(\cos(x)\) |
| \(\cos(x)\) | \(-\sin(x)\) |
| \(e^x\) | \(e^x\) |
| \(\ln(x)\) | \(1/x\) |
| \(\log_a(x)\) | \(1/(x \ln(a))\) |

## Aplicações

### Otimização

Encontrar máximo ou mínimo de funções:

```
f'(x) = 0 → pontos críticos
f''(x) > 0 → mínimo local
f''(x) < 0 → máximo local
```

**Exemplo:** Maximizar área dado o perímetro.

### Máquinas

Em ML, usamos derivadas para gradient descent:

```python
theta = theta - alpha * delta_J/delta_theta
```

Onde J é a função de perda.

### Física

- **Velocidade**: derivada da posição
- **Aceleração**: derivada da velocidade
- **Força**: derivada do momento

## Regras de L'Hôpital

Para limites de formas indeterminadas \((0/0)\) ou \((\infty/\infty)\):

$$\lim \frac{f(x)}{g(x)} = \lim \frac{f'(x)}{g'(x)}$$

Aplique repetidamente até obter forma determinada.

## Derivadas Parciais

Para funções com múltiplas variáveis:

$$\frac{\partial f}{\partial x} = 2x + y$$

$$\frac{\partial f}{\partial y} = x + 2y$$

Mantém outras variáveis constantes.

**Importante em ML:**
- Gradientes são vetores de derivadas parciais
- Usamos para otimizar funções de perda multivariáveis

## Gradiente

O vetor de derivadas parciais:

$$\nabla f = \left(\frac{\partial f}{\partial x_1}, \frac{\partial f}{\partial x_2}, ..., \frac{\partial f}{\partial x_n}\right)$$

**Propriedades:**
- Aponta na direção de maior aumento
- Perpendicular às curvas/superfícies de nível

## Taylor Series

Aproximar funções usando derivadas:

$$f(x) \approx f(a) + f'(a)(x-a) + \frac{f''(a)(x-a)^2}{2!} + ...$$

Usado para:
- Aproximação de funções
- Métodos numéricos
- Entender paisagens de otimização

---

**Série: Matemática**
1. [Cálculo Diferencial: Uma Introdução]({{ site.baseurl }}/calculo-diferencial-uma-introducao) ← *você está aqui*

## Leia Mais

- Stewart, J. *Cálculo*. Vol. 1. 8ª Ed. Cengage, 2017.
- Thomas, G. B. *Cálculo*. Vol. 1. 12ª Ed. Pearson, 2012.
- Apostol, T. M. *Calculus*. 2nd Ed. Wiley, 1967.
- Khan Academy. *Differential Calculus*.