---
layout: post
title: "Bancos de Dados: Conceitos Fundamentais"
description: "Aprenda como dados são armazenados e organizados em sistemas de banco de dados."
date: 2014-11-15
---

**Bancos de dados** são sistemas essenciais para armazenar, organizar e gerenciar informações. De pequenas aplicações a gigantescos sistemas corporativos, a capacidade de persistir e recuperar dados eficientemente é fundamental.

## O que é um Banco de Dados?

Coleção organizada de dados armazenados eletronicamente:

- **Persistente**: Dados sobrevivem após o programa fechar
- **Organizado**: Estruturado para recuperação eficiente
- **Compartilhável**: Múltiplos usuários e aplicações podem acessar

### Componentes

- **Dados**: A informação real
- **SGBD**: Sistema Gerenciador de Banco de Dados (software)
- **Schema**: Estrutura que define organização
- **Linguagem**: SQL para manipular dados

## Tipos de Bancos de Dados

### Relacionais (SQL)

Dados organizados em **tabelas** com linhas e colunas:

```
┌─────────────────────────────┐
│         USUÁRIOS            │
├──────┬────────┬────────────┤
│  ID  │  NOME  │    EMAIL   │
├──────┼────────┼────────────┤
│  1   │ João   │joao@email  │
│  2   │ Maria  │maria@email │
└──────┴────────┴────────────┘
```

**Chave Primária**: Identificador único de cada linha
**Chave Estrangeira**: Link para outra tabela

### Não-Relacionais (NoSQL)

```
├── Documentos (MongoDB)     → Documentos estilo JSON
├── Chave-Valor (Redis)      → Pares simples
├── Grafos (Neo4j)           → Relacionamentos
└── Colunar (Cassandra)      → Colunas largas
```

### Quando Usar Cada

| SQL | NoSQL |
|-----|-------|
| Dados estruturados | Estrutura flexível |
| Transações ACID | Alta escala |
| Queries complexas | Performance em leitura |
| Maturidade | Documents heterogêneos |

## SQL: Linguagem de Consulta

### CREATE TABLE

```sql
CREATE TABLE usuarios (
    id INT PRIMARY KEY,
    nome VARCHAR(100) NOT NULL,
    email VARCHAR(100) UNIQUE
);
```

### INSERT

```sql
INSERT INTO usuarios (id, nome, email)
VALUES (1, 'João', 'joao@email.com');
```

### SELECT

```sql
SELECT nome, email 
FROM usuarios 
WHERE id > 1;
```

### UPDATE

```sql
UPDATE usuarios 
SET email = 'novo@email.com' 
WHERE id = 1;
```

### DELETE

```sql
DELETE FROM usuarios 
WHERE id = 2;
```

## Normalização

Processo de organizar dados para minimizar redundância:

### Formas Normais

- **1NF**: Valores atômicos, sem grupos repetitivos
- **2NF**: Sem dependências parciais
- **3NF**: Sem dependências transitivas

### Exemplo

```
NÃO NORMALIZADO:
Pedido: João, Tel: 123, Item: Livro, Qtd: 2, Item: Caneta, Qtd: 3

NORMALIZADO:
Clientes: ID, Nome, Tel
Pedidos: ID, ClienteID
ItensPedido: PedidoID, Item, Qtd
```

## Transações e ACID

Propriedades que garantem integridade dos dados:

- **Atomicidade**: Tudo ou nada
- **Consistência**: Regras sempre respeitadas
- **Isolamento**: Transações não se interferem
- **Durabilidade**: Confirmação persiste

## Indexação

Estruturas que aceleram queries:

```sql
CREATE INDEX idx_email ON usuarios(email);
```

Sem índice: O(n) full table scan
Com índice: O(log n) lookup

### Trade-offs

- **Prós**: Queries mais rápidas
- **Contras**: Mais armazenamento, updates mais lentos

## ORM (Object-Relational Mapping)

Mapeia objetos de programação para tabelas:

```python
from sqlalchemy import Column, Integer, String
from sqlalchemy.ext.declarative import declarative_base

Base = declarative_base()

class Usuario(Base):
    __tablename__ = 'usuarios'
    id = Column(Integer, primary_key=True)
    nome = Column(String(100))
```

## Backup e Recuperação

### Estratégias

- **Full backup**: Tudo
- **Incremental**: Mudanças desde último backup
- **Point-in-time**: Recovery até momento específico

### Melhores Práticas

- Backups regulares
- Testar restauração
- Replicação para alta disponibilidade
- Cloud backups

---

**Série: Infraestrutura Web**
1. [Como Funciona a Internet?]({{ site.baseurl }}/como-funciona-a-internet)
2. [Redes de Computadores: Uma Introdução]({{ site.baseurl }}/redes-de-computadores-uma-introducao)
3. [Bancos de Dados: Conceitos Fundamentais]({{ site.baseurl }}/bancos-de-dados-conceitos-fundamentais) ← *você está aqui*
4. [Segurança da Informação: Princípios Básicos]({{ site.baseurl }}/seguranca-da-informacao-principios-basicos)

## Leia Mais

- Date, C. J. *Introdução a Sistemas de Bancos de Dados*. 8ª Ed. Campus, 2004.
- Elmasri, R. & Navathe, S. B. *Sistemas de Banco de Dados*. 7ª Ed. Pearson, 2018.
- Garcia-Molina, H., Ullman, J. D. & Widom, J. *Database Systems: The Complete Book*. 2nd Ed. Prentice Hall, 2008.
