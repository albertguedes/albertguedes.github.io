---
layout: post
title: "S.O.L.I.D.: Princípios de Design Orientado a Objetos em PHP"
description: "Uma análise prática dos cinco princípios S.O.L.I.D. de design orientado a objetos, com exemplos implementados em PHP que demonstram como criar código mais manutenível e extensível."
date: 2026-04-19
tags: ["projects", "github", "php", "oop", "design-patterns", "software-engineering"]
categories: ["software-engineering", "php"]
---

O projeto **solid-principles-with-php** é uma demonstração prática dos cinco princípios fundamentais de design orientado a objetos conhecidos como **S.O.L.I.D.** Estes princípios, formalizados por Robert C. Martin (Uncle Bob), são a espinha dorsal de código orientado a objetos de alta qualidade.

## Os Cinco Princípios

```
S — Single Responsibility Principle (SRP)
O — Open/Closed Principle (OCP)
L — Liskov Substitution Principle (LSP)
I — Interface Segregation Principle (ISP)
D — Dependency Inversion Principle (DIP)
```

## 1. Single Responsibility Principle (SRP)

**Uma classe deve ter apenas uma razão para mudar.**

### Violação do SRP

```php
// Classe com múltiplas responsabilidades
class User {
    public function setName(string $name) { /* ... */ }
    public function setEmail(string $email) { /* ... */ }
    public function saveToDatabase() { /* ... */ } // Responsabilidade de persistência
    public function sendEmail() { /* ... */ } // Responsibilidade de comunicação
    public function generateReport() { /* ... */ } // Responsabilidade de relatório
}
```

### Conformidade com SRP

```php
class User {
    private string $name;
    private string $email;
    
    public function setName(string $name): void { $this->name = $name; }
    public function setEmail(string $email): void { $this->email = $email; }
    public function getName(): string { return $this->name; }
    public function getEmail(): string { return $this->email; }
}

class UserRepository {
    private DatabaseConnection $db;
    
    public function save(User $user): void { /* persistência */ }
    public function find(int $id): User { /* busca */ }
}

class EmailService {
    public function send(User $user, string $message): void { /* envio */ }
}

class UserReportGenerator {
    public function generate(User $user): Report { /* relatório */ }
}
```

## 2. Open/Closed Principle (OCP)

**Entidades de software devem estar abertas para extensão, mas fechadas para modificação.**

### Violação do OCP

```php
class AreaCalculator {
    public function calculate($shape): float {
        if ($shape instanceof Square) {
            return $shape->side * $shape->side;
        }
        if ($shape instanceof Circle) {
            return pi() * $shape->radius * $shape->radius;
        }
        // Cada nova forma exige modificação desta classe
    }
}
```

### Conformidade com OCP

```php
interface Shape {
    public function area(): float;
}

class Square implements Shape {
    private float $side;
    public function area(): float { return $this->side * $this->side; }
}

class Circle implements Shape {
    private float $radius;
    public function area(): float { return pi() * $this->radius * $this->radius; }
}

class AreaCalculator {
    public function calculate(Shape $shape): float {
        return $shape->area(); // Polymorphism resolve o problema
    }
}
```

## 3. Liskov Substitution Principle (LSP)

**Objetos de uma superclasse devem poder ser substituídos por objetos de subclasses sem quebrar a aplicação.**

### O Problema do Quadrado/Retângulo

```php
class Rectangle {
    protected float $width;
    protected float $height;
    
    public function setWidth(float $width): void { $this->width = $width; }
    public function setHeight(float $height): void { $this->height = $height; }
    public function area(): float { return $this->width * $this->height; }
}

class Square extends Rectangle {
    // Um quadrado viola LSP se tratado como retângulo
    public function setWidth(float $width): void {
        $this->width = $width;
        $this->height = $width; // Força igualdade
    }
    
    public function setHeight(float $height): void {
        $this->width = $height;
        $this->height = $height;
    }
}

// Teste que falha
function testRectangleArea(Rectangle $rect) {
    $rect->setWidth(5);
    $rect->setHeight(4);
    // Espera 20, mas com Square retorna 16
    assert($rect->area() === 20);
}
```

### Solução Compatível com LSP

```php
interface Shape {
    public function area(): float;
}

class Rectangle implements Shape {
    private float $width;
    private float $height;
    
    public function __construct(float $width, float $height) {
        $this->width = $width;
        $this->height = $height;
    }
    
    public function area(): float { return $this->width * $this->height; }
}

class Square implements Shape {
    private float $side;
    
    public function __construct(float $side) {
        $this->side = $side;
    }
    
    public function area(): float { return $this->side * $this->side; }
}
```

## 4. Interface Segregation Principle (ISP)

**Clientes não devem ser forçados a depender de interfaces que não usam.**

### Violação do ISP

```php
interface Worker {
    public function work(): void;
    public function eat(): void;
    public function sleep(): void;
}

class HumanWorker implements Worker {
    public function work(): void { /* ... */ }
    public function eat(): void { /* ... */ }
    public function sleep(): void { /* ... */ }
}

class RobotWorker implements Worker {
    public function work(): void { /* ... */ }
    // Robôs não comem nem dormem, mas são forçados a implementar
    public function eat(): void { throw new Exception("Robots don't eat"); }
    public function sleep(): void { throw new Exception("Robots don't sleep"); }
}
```

### Conformidade com ISP

```php
interface Workable {
    public function work(): void;
}

interface Eatable {
    public function eat(): void;
}

interface Sleepable {
    public function sleep(): void;
}

class HumanWorker implements Workable, Eatable, Sleepable {
    public function work(): void { /* ... */ }
    public function eat(): void { /* ... */ }
    public function sleep(): void { /* ... */ }
}

class RobotWorker implements Workable {
    public function work(): void { /* ... */ }
    // Apenas implementa o que precisa
}
```

## 5. Dependency Inversion Principle (DIP)

**Módulos de alto nível não devem depender de módulos de baixo nível. Ambos devem depender de abstrações.**

### Violação do DIP

```php
class MySQLConnection {
    public function connect() { /* conexão MySQL */ }
    public function query(string $sql) { /* ... */ }
}

class PasswordReminder {
    private MySQLConnection $dbConnection; // Depende de implementação concreta
    
    public function __construct(MySQLConnection $dbConnection) {
        $this->dbConnection = $dbConnection;
    }
}
```

### Conformidade com DIP

```php
interface DatabaseConnection {
    public function connect(): void;
    public function query(string $sql): array;
}

class MySQLConnection implements DatabaseConnection {
    public function connect(): void { /* ... */ }
    public function query(string $sql): array { /* ... */ }
}

class PostgreSQLConnection implements DatabaseConnection {
    public function connect(): void { /* ... */ }
    public function query(string $sql): array { /* ... */ }
}

class PasswordReminder {
    private DatabaseConnection $dbConnection; // Depende de abstração
    
    public function __construct(DatabaseConnection $dbConnection) {
        $this->dbConnection = $dbConnection;
    }
}
```

## Benefícios Práticos

| Princípio | Benefício |
|-----------|-----------|
| SRP | Classes menores, mais cohesionadas, mais fáceis de testar |
| OCP | Adição de features sem modificar código existente |
| LSP | Sistemas mais previsíveis e testáveis |
| ISP | Interfaces mais enxutas, clientes não dependem de métodos não utilizados |
| DIP | Baixo acoplamento, facilidade de swapping de implementações |

## Conclusão

Os princípios S.O.L.I.D. não são dogmas, mas diretrizes que, quando aplicadas judiciosamente, resultam em código mais manutenível, testável e extensível. O projeto **solid-principles-with-php** demonstra cada princípio com código PHP moderno, mostrando como aplicá-los na prática.

**Repositório**: [github.com/albertguedes/solid-principles-with-php](https://github.com/albertguedes/solid-principles-with-php)
