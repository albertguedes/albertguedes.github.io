---
layout: post
title: "O que é um Algoritmo?"
description: "Uma introdução aos algoritmos, os passos fundamentais para resolver problemas na computação."
date: 2012-06-12
---

Um **algoritmo** é, fundamentalmente, uma sequência ordenada de instruções que permite resolver um problema ou realizar uma tarefa específica. O conceito não é novo — matemáticos como Euclides já descreviam algoritmos há mais de dois mil anos — mas foi com o surgimento dos computadores que sua importância tornou-se central na tecnologia moderna.

## Características de um Bom Algoritmo

Para ser considerado eficiente, um algoritmo deve possuir algumas qualidades essenciais:

**Precisão**: Cada passo deve ser definido de forma clara e inequívoca. Não pode haver ambiguidade nas instruções.

**Finitude**: O algoritmo deve terminar após um número finito de passos. Não pode entrar em loop infinito.

**Entrada e Saída**: Deve possuir dados de entrada (o problema) e produzir dados de saída (a solução).

**Efetividade**: Cada passo deve ser executável em tempo razoável.

## Exemplo Clássico: Algoritmo de Euclides

O algoritmo para encontrar o máximo divisor comum (MDC) entre dois números é um dos exemplos mais antigos:

```
1. Se B = 0, retorna A
2. Caso contrário, calcula o resto de A por B
3. Substitui A por B e B pelo resto
4. Repete até B = 0
```

Este algoritmo, desenvolvido há mais de 2000 anos, ainda é utilizado em computadores hoje em dia.

## Por que Estudar Algoritmos?

A eficiência de um algoritmo é medida principalmente por dois fatores:

- **Tempo de execução**: Quanto tempo leva para produzir o resultado
- **Espaço de memória**: Quanrta memória é necessária para executar

Um problema pode ser resolvido de múltiplas formas, cada uma com diferentes performances. Saber escolher ou criar o algoritmo correto é uma habilidade fundamental para qualquer desenvolvedor.

## Notação Big-O

Para comparar algoritmos, usamos a notação Big-O, que descreve o comportamento assintótico — ou seja, como o algoritmo se comporta quando a entrada cresce indefinidamente.

- O(1): Tempo constante
- O(log n): Tempo logarítmico
- O(n): Tempo linear
- O(n²): Tempo quadrático

Escolher um algoritmo com complexidade menor pode significar a diferença entre um programa que roda em segundos ou em horas.

---

**Série: Fundamentos da Programação**
1. [Lógica de Programação para Iniciantes]({{ site.baseurl }}/logica-de-programacao-para-iniciantes)
2. [O que é um Algoritmo?]({{ site.baseurl }}/o-que-e-um-algoritmo) ← *você está aqui*
3. [Estruturas de Dados: Arrays e Listas]({{ site.baseurl }}/estruturas-de-dados-arrays-e-listas)

## Leia Mais

- Cormen, T. H. et al. *Algoritmos: Teoria e Prática*. 3ª Ed. Elsevier, 2012.
- Sedgewick, R. & Wayne, K. *Algorithms*. 4ª Ed. Addison-Wesley, 2011.
- Knuth, D. E. *The Art of Computer Programming*. Vol. 1. 3ª Ed. Addison-Wesley, 1997.
