---
layout: post
title: "Introdução à Termodinâmica"
description: "Conheça as leis fundamentais que governam calor, temperatura e energia."
date: 2017-06-15
---

A **termodinâmica** é a ciência que estuda calor, temperatura e sua relação com energia e trabalho. É fundamental para compreender desde o funcionamento de motores de carros até a evolução do universo. Suas leis, elegantes em sua simplicidade, governam todos os processos físicos.

## Conceitos Fundamentais

### Sistema e Vizinhança

- **Sistema**: A parte do universo que estudamos (um gás, um motor, uma célula)
- **Vizinhança**: Tudo fora do sistema
- **Fronteira**: Limite entre sistema e vizinhança

### Tipos de Sistema

- **Aberto**: Troca massa e energia com a vizinhança
- **Fechado**: Só troca energia (massa constante)
- **Isolado**: Não troca nada com a vizinhança

### Variáveis de Estado

Propriedades que definem o estado do sistema:
- **Temperatura (T)**: Medida de quão quente/frio
- **Pressão (P)**: Força por unidade de área
- **Volume (V)**: Espaço ocupado
- **Energia interna (U)**: Energia total das partículas

## Temperatura e Calor

### Temperatura vs Calor

**Temperatura** mede a média da energia cinética das partículas. **Calor** é energia transferida devido a diferença de temperatura.

```text
Temperatura alta = partículas se movem rapidamente (em média)
Temperatura baixa = partículas se movem lentamente (em média)
```

### Escalas de Temperatura

| Escala | Ponto de Água Congelando | Ponto de Água Fervendo |
|--------|--------------------------|------------------------|
| Celsius (°C) | 0°C | 100°C |
| Fahrenheit (°F) | 32°F | 212°F |
| Kelvin (K) | 273.15 K | 373.15 K |

Kelvin é a escala absoluta, usada em física.

## Primeira Lei da Termodinâmica

> "A energia não pode ser criada nem destruída, apenas transformada."

Matematicamente:

$$\Delta U = Q - W$$

Onde:
- **ΔU**: Variação da energia interna
- **Q**: Calor transferido para o sistema
- **W**: Trabalho realizado pelo sistema

### Exemplo: Motor de Carro

1. Combustível queima (Q entra como calor)
2. Gases se expandem, movendo o pistão (W é trabalho realizado)
3. Energia interna do sistema diminui
4. ΔU = Q - W

## Segunda Lei da Termodinâmica

A segunda lei diz que processos naturais têm uma **direção preferencial**.

> "O calor flui espontaneamente de um corpo quente para um corpo frio, nunca o contrário."

### Entropia

**Entropia (S)** mede a desordem ou aleatoriedade de um sistema:

$$\Delta S \geq 0$$

A entropia total do universo sempre aumenta em processos naturais.

### Consequências da Segunda Lei

- Máquinas térmicas nunca podem ser 100% eficientes
- Não existe motor perpétuo
- Eventualmente, toda energia se degradará para calor uniforme

### Ciclo de Carnot

O ciclo mais eficiente possível entre duas temperaturas:
$$\text{Eficiência} = 1 - \frac{T_{frio}}{T_{quente}}$$

Nenhum motor real pode superar a eficiência de Carnot.

## Terceira Lei da Termodinâmica

> "É impossível alcançar o zero absoluto (0 K) em um número finito de passos."

Zero Kelvin seria quando todas as partículas teriam energia mínima (zero movimento). Na prática, podemos nos aproximar, mas nunca alcançar.

## Máquinas Térmicas

Dispositivos que convertem calor em trabalho:

```text
Fonte quente → Máquina térmica → Fonte fria
   (T alta)                (T baixa)
```

### Componentes

1. **Fonte quente**: Fornece calor (combustível)
2. **Trabalho útil**: Energia mecânica produzida
3. **Fonte fria**: Calor rejeitado

### Eficiência

$$\text{Eficiência} = \frac{\text{Trabalho}}{\text{Calor fornecido}} = \frac{Q_{quente} - Q_{frio}}{Q_{quente}} = 1 - \frac{Q_{frio}}{Q_{quente}}$$

## Refrigeradores

O inverso das máquinas térmicas — usam trabalho para transferir calor de local frio para local quente:

```text
Trabalho → Refrigerador → Calor vai do frio para o quente
```

Quanto mais frio o interior, mais trabalho é necessário.

## Aplicações Práticas

### Motores de Combustão

- 4 tempos: admissão, compressão, combustão, escape
- Eficiência típica: 25-30%

### Usinas Termelétricas

Convertem calor em eletricidade:
- Carvão, gás natural, nuclear
- Eficiência: 30-45%

### Geladeiras e Ar Condicionado

Usam refrigerantes que mudam de fase, absorvendo e liberando calor.

### Atmosfera e Clima

O transporte de calor na atmosfera impulsiona padrões climáticos e clima.

## Tabela Resumo das Leis

| Lei | Enunciado Informal |
|-----|-------------------|
| **Zero** | Se A está em equilíbrio com B, e B com C, então A está em equilíbrio com C |
| **Primeira** | Energia se conserva |
| **Segunda** | Entropia do universo aumenta |
| **Terceira** | Zero absoluto é inacessível |

---

**Série: Mecânica Clássica** (relacionado)
1. [As Três Leis de Newton Explicadas]({{ site.baseurl }}/as-tres-leis-de-newton-explicadas)
2. [O que é Energia? Tipos e Conservação]({{ site.baseurl }}/o-que-e-energia-tipos-e-conservacao)
3. [Introdução à Termodinâmica]({{ site.baseurl }}/introducao-a-termodinamica) ← *você está aqui*

## Leia Mais

- Halliday, D., Resnick, R. & Walker, J. *Fundamentos de Física*. Vol. 2. 10ª Ed. LTC, 2016.
- Cengel, Y. A. & Boles, M. A. *Termodinâmica*. 8ª Ed. McGraw-Hill, 2018.
- Zemansky, M. W. & Dittman, R. H. *Heat and Thermodynamics*. 8ª Ed. McGraw-Hill, 1997.
- Fermi, E. *Thermodynamics*. Dover, 1956.
