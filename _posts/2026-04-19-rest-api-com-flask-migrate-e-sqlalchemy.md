---
layout: post
title: "REST API com Flask: Migrates, Seeds e Arquitetura Limpa"
description: "Implementação de uma REST API robusta com Flask, Flask-Migrate e SQLAlchemy, demonstrando padrões de arquitetura e boas práticas para APIs Python."
date: 2026-04-19
tags: ["projects", "github", "python", "flask", "rest-api", "sqlalchemy"]
categories: ["backend", "api", "python"]
---

O projeto **python-flask-api** demonstra a construção de uma REST API profissional com Flask, utilizando **Flask-Migrate** para versionamento de banco de dados e **SQLAlchemy** como ORM. O foco está em arquitetura limpa e práticas de engenharia de software.

## Arquitetura do Projeto

```
python-flask-api/
├── app/
│   ├── __init__.py          # Factory pattern
│   ├── models.py            # Definições SQLAlchemy
│   ├── routes/              # Blueprints de rotas
│   └── utils/               # Helpers
├── migrations/              # Alembic migrations
├── seeds/                   # Seed data
├── requirements.txt
└── config.py
```

## Factory Pattern para Aplicação

O projeto utiliza o **Factory Pattern** para inicialização flexível da aplicação:

```python
from flask import Flask
from flask_sqlalchemy import SQLAlchemy
from flask_migrate import Migrate

db = SQLAlchemy()
migrate = Migrate()

def create_app(config_name='development'):
    app = Flask(__name__)
    
    # Configuração
    app.config.from_object(f'config.{config_name.capitalize()}Config')
    
    # Inicialização de extensões
    db.init_app(app)
    migrate.init_app(app, db)
    
    # Registro de blueprints
    from app.routes import api_bp
    app.register_blueprint(api_bp, url_prefix='/api/v1')
    
    return app
```

## Modelagem com SQLAlchemy

### Definição de Models

```python
from datetime import datetime
from app import db

class User(db.Model):
    __tablename__ = 'users'
    
    id = db.Column(db.Integer, primary_key=True)
    username = db.Column(db.String(80), unique=True, nullable=False)
    email = db.Column(db.String(120), unique=True, nullable=False)
    password_hash = db.Column(db.String(255), nullable=False)
    created_at = db.Column(db.DateTime, default=datetime.utcnow)
    updated_at = db.Column(db.DateTime, default=datetime.utcnow, onupdate=datetime.utcnow)
    
    # Relacionamentos
    posts = db.relationship('Post', backref='author', lazy='dynamic')
    
    def to_dict(self):
        return {
            'id': self.id,
            'username': self.username,
            'email': self.email,
            'created_at': self.created_at.isoformat()
        }

class Post(db.Model):
    __tablename__ = 'posts'
    
    id = db.Column(db.Integer, primary_key=True)
    title = db.Column(db.String(200), nullable=False)
    content = db.Column(db.Text, nullable=False)
    user_id = db.Column(db.Integer, db.ForeignKey('users.id'), nullable=False)
    published = db.Column(db.Boolean, default=False)
    created_at = db.Column(db.DateTime, default=datetime.utcnow)
    
    def to_dict(self):
        return {
            'id': self.id,
            'title': self.title,
            'content': self.content,
            'author': self.author.username,
            'published': self.published,
            'created_at': self.created_at.isoformat()
        }
```

## Migrations com Flask-Migrate (Alembic)

### Inicialização

```bash
flask db init
flask db migrate -m "Create initial models"
flask db upgrade
```

### Criando uma Migration

```python
# migrations/versions/abc123_create_posts.py
from alembic import op
import sqlalchemy as sa

def upgrade():
    op.create_table(
        'posts',
        sa.Column('id', sa.Integer(), nullable=False),
        sa.Column('title', sa.String(length=200), nullable=False),
        sa.Column('content', sa.Text(), nullable=False),
        sa.Column('user_id', sa.Integer(), nullable=False),
        sa.Column('published', sa.Boolean(), nullable=True),
        sa.Column('created_at', sa.DateTime(), nullable=True),
        sa.ForeignKeyConstraint(['user_id'], ['users.id']),
        sa.PrimaryKeyConstraint('id')
    )

def downgrade():
    op.drop_table('posts')
```

### Rollback

```bash
flask db downgrade -1  # Rollback última migration
flask db history      # Ver histórico
```

## Rotas RESTful com Blueprints

### Estrutura de Routes

```python
from flask import Blueprint, request, jsonify
from app import db
from app.models import User, Post

api_bp = Blueprint('api', __name__)

@api_bp.route('/users', methods=['GET'])
def get_users():
    users = User.query.all()
    return jsonify([user.to_dict() for user in users])

@api_bp.route('/users/<int:user_id>', methods=['GET'])
def get_user(user_id):
    user = User.query.get_or_404(user_id)
    return jsonify(user.to_dict())

@api_bp.route('/users', methods=['POST'])
def create_user():
    data = request.get_json()
    
    if not data or not 'username' in data:
        return jsonify({'error': 'Username required'}), 400
    
    user = User(
        username=data['username'],
        email=data['email'],
        password_hash=data['password']  # Em produção: hash!
    )
    
    db.session.add(user)
    db.session.commit()
    
    return jsonify(user.to_dict()), 201

@api_bp.route('/users/<int:user_id>', methods=['PUT'])
def update_user(user_id):
    user = User.query.get_or_404(user_id)
    data = request.get_json()
    
    if 'username' in data:
        user.username = data['username']
    if 'email' in data:
        user.email = data['email']
    
    db.session.commit()
    return jsonify(user.to_dict())

@api_bp.route('/users/<int:user_id>', methods=['DELETE'])
def delete_user(user_id):
    user = User.query.get_or_404(user_id)
    db.session.delete(user)
    db.session.commit()
    return '', 204
```

## Seed Data

### Script de Seeding

```python
# seeds/seed.py
from app import create_app, db
from app.models import User, Post

def seed_data():
    app = create_app()
    
    with app.app_context():
        # Limpa dados existentes
        db.drop_all()
        db.create_all()
        
        # Cria usuários
        users = [
            User(username='admin', email='admin@example.com', password_hash='hashed'),
            User(username='user1', email='user1@example.com', password_hash='hashed'),
            User(username='user2', email='user2@example.com', password_hash='hashed'),
        ]
        
        for user in users:
            db.session.add(user)
        
        db.session.commit()
        
        # Cria posts
        posts = [
            Post(title='First Post', content='Content here', author=users[0]),
            Post(title='Hello World', content='Another post', author=users[1]),
        ]
        
        for post in posts:
            db.session.add(post)
        
        db.session.commit()
        print(f"Seeded {len(users)} users and {len(posts)} posts")

if __name__ == '__main__':
    seed_data()
```

## Configuração por Ambiente

```python
# config.py
import os

class Config:
    SECRET_KEY = os.environ.get('SECRET_KEY') or 'dev-secret-key'
    SQLALCHEMY_TRACK_MODIFICATIONS = False

class DevelopmentConfig(Config):
    DEBUG = True
    SQLALCHEMY_DATABASE_URI = 'sqlite:///dev.db'

class ProductionConfig(Config):
    DEBUG = False
    SQLALCHEMY_DATABASE_URI = os.environ.get('DATABASE_URL')

class TestingConfig(Config):
    TESTING = True
    SQLALCHEMY_DATABASE_URI = 'sqlite:///test.db'
```

## Stack Tecnológico

| Componente | Tecnologia | Propósito |
|-----------|------------|-----------|
| Framework | Flask | API web framework |
| ORM | SQLAlchemy | Abstração de banco de dados |
| Migrations | Flask-Migrate/Alembic | Versionamento de schema |
| Database | SQLite (dev) / PostgreSQL (prod) | Persistência |
| Validation | Flask request parsing | Input validation |

## Boas Práticas Demonstradas

1. **Factory Pattern**: Aplicação configurável e testável
2. **Blueprints**: Organização modular de rotas
3. **Migrations**: Versionamento seguro do banco
4. **Separation of Concerns**: Models, Routes, Utils em módulos separados
5. **Error Handling**: HTTP status codes apropriados
6. **Seed Data**: Dados de desenvolvimento consistentes

## Conclusão

O **python-flask-api** demonstra uma arquitetura profissional para APIs Flask, cobrindo desde setup inicial até deployment. As práticas de migrations, seeds e organização em blueprints fornecem uma base sólida para aplicações em produção.

**Repositório**: [github.com/albertguedes/python-flask-api](https://github.com/albertguedes/python-flask-api)
