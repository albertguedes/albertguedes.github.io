---
layout: post
title: "Algoritmos de Busca: DFS, BFS e A*"
description: "Explore os algoritmos fundamentais para navegar em grafos e encontrar caminhos."
date: 2014-04-05
---

**Algoritmos de busca** são fundamentais em ciência da computação. Desde encontrar o menor caminho em um mapa até resolver puzzles, a busca em estruturas de dados é essencial.

## Grafos: Estrutura de Dados Fundamental

Um **grafo** consiste de:
- **Vértices (nodes)**: pontos
- **Arestas (edges)**: conexões entre pontos

```text
    A
   /|\
  B C D
  |/ \|
  E---F--G
```

### Tipos de Grafos

- **Direcionado**: Arestas têm direção (A → B, mas não B → A)
- **Não-direcionado**: Arestas são bidirecionais
- **Ponderado**: Arestas têm pesos (distâncias, custos)
- **Com ciclos**: Caminhos que voltam ao ponto inicial

## Busca em Largura (BFS)

**Breadth-First Search** explora nível por nível.

### Funcionamento

1. Começa na origem
2. Explora todos os vizinhos imediatos
3. Depois os vizinhos dos vizinhos
4. Usa **fila** (FIFO)

```text
Início: A
Nível 0: A
Nível 1: B, C, D
Nível 2: E, F
Nível 3: G
```

### Implementação

```python
from collections import deque

def bfs(grafo, inicio):
    visitados = {inicio}
    fila = deque([inicio])
    
    while fila:
        vertice = fila.popleft()
        print(vertice)  # Processar
        
        for vizinho in grafo[vertice]:
            if vizinho not in visitados:
                visitados.add(vizinho)
                fila.append(vizinho)
```

### Propriedades

- **Complexidade**: O(V + E) onde V = vértices, E = arestas
- **Encontra caminho mínimo** (em termos de número de arestas)
- **Útil para**: encontrar distância mínima, componentes conectados

## Busca em Profundidade (DFS)

**Depth-First Search** vai o mais fundo possível antes de voltar.

### Funcionamento

1. Começa na origem
2. Segue por um caminho até o fim
3. Volta e tenta outro caminho
4. Usa **pilha** (LIFO) ou recursão

```text
Início: A
Caminho: A → B → E → F → (volta) → C → (volta) → D → G
```

### Implementação

```python
def dfs(grafo, inicio, visitados=None):
    if visitados is None:
        visitados = set()
    
    visitados.add(inicio)
    print(inicio)  # Processar
    
    for vizinho in grafo[inicio]:
        if vizinho not in visitados:
            dfs(grafo, vizinho, visitados)
```

### Variantes

- **Pré-ordem**: Processa antes de explorar
- **Pós-ordem**: Processa depois de explorar
- **Ordem central**: Processa no meio

### Propriedades

- **Complexidade**: O(V + E)
- **Usa menos memória que BFS** em grafos amplos
- **Útil para**: detectar ciclos, topological sort, labirintos

## Busca com Custo Uniforme

Extensão do BFS para grafos ponderados:

- Explora nós em ordem de custo total acumulado
- Garante caminho mínimo quando todos os pesos são não-negativos

```python
import heapq

def ucs(grafo, inicio, objetivo):
    fila = [(0, inicio)]
    visitados = set()
    
    while fila:
        custo, vertice = heapq.heappop(fila)
        
        if vertice in visitados:
            continue
        if vertice == objetivo:
            return custo
        
        visitados.add(vertice)
        
        for vizinho, peso in grafo[vertice]:
            if vizinho not in visitados:
                heapq.heappush(fila, (custo + peso, vizinho))
```

## Algoritmo A*

A* combina:
- **Custo real do início ao nó atual** (como UCS)
- **Estimativa do nó ao objetivo** (heurística)

$$f(n) = g(n) + h(n)$$

- g(n): custo do início até n
- h(n): estimativa de n até objetivo
- f(n): custo total estimado através de n

### Heurística

Deve ser **admissível** (nunca superestima o custo real) para garantir optimalidade.

**Exemplos de heurísticas:**
- Distância em linha reta (para mapas)
- Número de peças fora do lugar (para puzzles)
- Distância de Manhattan (grid)

### Implementação

```python
import heapq

def a_star(grafo, inicio, objetivo, h):
    # h = função heurística
    fila = [(h(inicio), 0, inicio)]
    visitados = {}
    
    while fila:
        _, custo, vertice = heapq.heappop(fila)
        
        if vertice == objetivo:
            return custo
        
        if vertice in visitados:
            continue
        visitados[vertice] = custo
        
        for vizinho, peso in grafo[vertice]:
            if vizinho not in visitados:
                novo_custo = custo + peso
                prioridade = novo_custo + h(vizinho)
                heapq.heappush(fila, (prioridade, novo_custo, vizinho))
```

## Comparação

| Algoritmo | Usa Heurística | Optimalidade | Memória |
|-----------|---------------|--------------|---------|
| BFS | Não | Sim (passos) | Alta |
| DFS | Não | Não | Baixa |
| UCS | Não | Sim (custo) | Alta |
| A* | Sim | Sim | Variável |

## Aplicações

- **GPS/Navegação**: A* para encontrar rotas
- **Jogos**: DFS para explorar jogadas, A* para otimizar
- **Redes sociais**: BFS para encontrar conexões
- **Compiladores**: DFS para parse trees
- **Resolução de labirintos**: BFS ou DFS

---

**Série: IA Fundamentos**
1. [O que é Inteligência Artificial?]({{ site.baseurl }}/o-que-e-inteligencia-artificial)
2. [História da IA: Dos Inícios aos Dias Atuais]({{ site.baseurl }}/historia-da-ia-dos-inicios-aos-dias-atuais)
3. [Algoritmos de Busca: DFS, BFS e A*]({{ site.baseurl }}/algoritmos-de-busca-dfs-bfs-e-a) ← *você está aqui*

## Leia Mais

- Cormen, T. H. et al. *Algoritmos: Teoria e Prática*. 3ª Ed. Elsevier, 2012.
- Russell, S. & Norvig, P. *Inteligência Artificial*. 3ª Ed. Elsevier, 2013.
- Sedgewick, R. & Wayne, K. *Algorithms*. 4ª Ed. Addison-Wesley, 2011.
- Hart, P., Nilsson, N. & Raphael, B. "A Formal Basis for the Heuristic Determination of Minimum Cost Paths". *IEEE Transactions on Systems Science and Cybernetics*, 1968.
