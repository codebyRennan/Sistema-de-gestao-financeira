# Sistema-de-gestao-financeira
Um sistema para que o usuário tenha facilidade em visualizar suas finanças.

## Resumo do Projeto

O que queremos fazer:

Desenvolver um Sistema de Controle Financeiro Pessoal em Python, que permita:

Registrar receitas e despesas

Categorizar movimentações

Gerar relatórios mensais

Persistir dados em SQLite

Integrar com uma API externa (ex: cotação de moedas)

Inicialmente pode ser um sistema via terminal (CLI), mas estruturado de forma que possa evoluir para API Web futuramente.

## Exemplos de API pública de cotação de moedas que podemos usar:

ExchangeRate-API

AwesomeAPI

# 💡 Aplicação prática no sistema

Exemplo de uso real:

Usuário registra uma despesa em dólar

O sistema consulta a API de cotação

Converte automaticamente para reais

Salva o valor convertido no banco

## 📌 Fluxo técnico usando requests

Usuário informa valor e moeda

Sistema faz requisição HTTP:

import requests

response = requests.get("https://api.exemplo.com/usd-brl")
data = response.json()
cotacao = data["rate"]

Converte valor

Salva no banco

# 🏆 O que isso vai demonstrar:

Consumo de API REST

Manipulação de JSON

Tratamento de erros (timeout, status code)

Integração entre serviço externo e banco

Porque isso é valorizado para estágio

# 🗄 SQLite (sqlite3)

SQLite será o banco local do sistema.

Vocês podem criar tabelas como:

users
transactions
categories
### 📌 Estrutura sugerida:
Tabela categories
id    name
1    Alimentação
2    Transporte
Tabela transactions

| id | type | amount | category_id | date | currency |

type → receita ou despesa

amount → valor final (já convertido)

currency → moeda original

### 📌 Exemplo básico de uso no Python
import sqlite3

conn = sqlite3.connect("finance.db")
cursor = conn.cursor()

cursor.execute("""
CREATE TABLE IF NOT EXISTS transactions (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    type TEXT NOT NULL,
    amount REAL NOT NULL,
    category_id INTEGER,
    date TEXT NOT NULL
)
""")

conn.commit()
conn.close()

# 👥 Melhor divisão entre 2 pessoas

### Divisão profissional baseada em camadas.

## 👨‍💻 Pessoa 1 – Camada de Serviço & API

Responsável por:

Integração com API de cotação

Regras de negócio

Conversão de moeda

Validações

Tratamento de erros

Testes da camada de serviço

Arquivos:

services/
    currency_service.py
    transaction_service.py
## 👨‍💻 Pessoa 2 – Banco de Dados & Persistência

Responsável por:

Modelagem do banco

Criação das tabelas

Funções CRUD

Queries de relatório

Conexão SQLite

Arquivos:

database/
    connection.py
    transaction_repository.py
    category_repository.py
### 📌 Ambos trabalham juntos em:

main.py

README

organização do projeto

versionamento no GitHub
#### 📁 Estrutura Profissional Recomendada:
    finance-control/

    ├── app/
    │   ├── database/
    │   │   ├── connection.py
    │   │   ├── transaction_repository.py
    │   │   └── category_repository.py
    │   │
    │   ├── services/
    │   │   ├── currency_service.py
    │   │   └── transaction_service.py
    │   │
    │   ├── models/
    │   │   └── transaction.py
    │   │
    │   └── main.py
    │
    ├── tests/
    ├── requirements.txt
    ├── README.md
    ├── .gitignore
    └── finance.db
#### 📊 Funcionalidades para Impressionar:

### Versão 1:

 Cadastrar receita/despesa

 Listar transações

 Saldo total

 Relatório mensal

### Versão 2:

 Conversão automática de moeda

 Relatório por categoria

 Exportar CSV

 Logs estruturados

### Versão 3 (extra):

Criar API REST com Flask

# Páginas que devem ser criadas:

### -- Página de login
### -- Página com seus dados iniciais
### -- Aba de gastos esperados de cada mês (pré configuração de gastos padrão configurada pelo usuário
### -- Aba para importar CSV com dados bancários do cliente
### -- Aba com integração pública onde mostra a variação de valor de cada moeda podendo escolher o período
### --Categorização de tipos de despesas e ganhos do usuário
### -- Integração com IA para funcionar como consultor particular
### --Exportação de dados via CSV 
