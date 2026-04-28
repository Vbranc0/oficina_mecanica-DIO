# 🔧 Projeto Conceitual de Banco de Dados - Oficina Mecânica

## 📖 Contexto

Este projeto consiste na modelagem conceitual de um banco de dados para um sistema de **gerenciamento de ordens de serviço em uma oficina mecânica**, desenvolvido como parte do desafio da DIO.

O objetivo é controlar desde o cadastro de clientes e veículos até a execução de serviços e peças em ordens de serviço.

---

## 🎯 Escopo do Modelo

O modelo atende aos seguintes requisitos da narrativa:

### 👥 Clientes e Veículos
- Clientes podem ser **Pessoa Física (PF)** ou **Pessoa Jurídica (PJ)**, controlados por uma entidade `Documento`.
- Dados comuns de clientes e funcionários são armazenados na entidade `Cadastro` (generalização).
- Cada cliente pode ter **vários veículos** cadastrados.

### 👨‍🔧 Equipes e Mecânicos
- Cada veículo é designado a uma **equipe de mecânicos**.
- Mecânicos possuem código, nome, endereço e especialidade.
- Uma equipe possui turno e responsável.

### 📝 Ordem de Serviço (OS)
- Cada OS possui: número, data de emissão, valor total, status, data de solicitação e data de entrega.
- A OS registra qual veículo foi atendido e qual equipe executou os serviços.
- O cliente deve autorizar a execução dos serviços.

### 🔧 Serviços e Peças
- Uma OS pode conter **vários serviços** (relacionamento N:N).
- Um serviço pode estar presente em **várias OS** (relacionamento N:N).
- Uma OS pode conter **várias peças** (relacionamento N:N).
- Uma peça pode estar presente em **várias OS** (relacionamento N:N).
- Serviços são classificados em **Conserto** (corretivo) e **Revisão** (programada), com atributos específicos para cada tipo.

### 📊 Cálculo de Valores
- O valor de cada serviço é consultado em uma tabela de referência (`Serviços.Valor`).
- O valor das peças também compõe o total da OS.

---

## 🧩 Estrutura do Modelo (Principais Entidades)

| Entidade | Descrição |
|----------|-----------|
| `Cadastro` | Dados comuns a clientes e funcionários (nome, endereço, telefone, e-mail) |
| `Documento` | CPF ou CNPJ, com tipo (PF/PJ) |
| `Cliente` | Especialização de `Cadastro` com data de cadastro |
| `Funcionário` | Especialização de `Cadastro` com cargo, admissão e especialidade |
| `Equipe` | Equipe de mecânicos (turno, responsável) |
| `Veículo` | Veículos dos clientes (placa, fabricante, modelo, ano, chassi, etc.) |
| `Ordem de serviço` | OS com data, valor, autorização, status, etc. |
| `Serviços` | Serviços oferecidos (grupo, descrição, valor) |
| `Conserto` | Especialização de serviço para consertos corretivos |
| `Revisão` | Especialização de serviço para revisões programadas (com km mínima e prazos) |
| `Peça` | Peças utilizadas nos serviços |
| `OS_has_Serviços` | Tabela associativa entre OS e Serviços (quantidade, valor unitário) |
| `OS_has_Peça` | Tabela associativa entre OS e Peças (quantidade) |

---

## 🔗 Relacionamentos Principais

| Relacionamento | Cardinalidade | Descrição |
|----------------|---------------|-----------|
| `Cadastro` → `Cliente` | 1 : 1 | Um cadastro pode ser um cliente |
| `Cadastro` → `Funcionário` | 1 : 1 | Um cadastro pode ser um funcionário |
| `Cliente` → `Veículo` | 1 : N | Um cliente pode ter vários veículos |
| `Equipe` → `Funcionário` | 1 : N | Uma equipe tem vários funcionários |
| `Veículo` → `Ordem de serviço` | 1 : N | Um veículo pode ter várias OS |
| `Equipe` → `Ordem de serviço` | 1 : N | Uma equipe executa várias OS |
| `Ordem de serviço` ↔ `Serviços` | N : N | OS contém vários serviços |
| `Ordem de serviço` ↔ `Peça` | N : N | OS contém várias peças |
| `Serviços` → `Conserto` | 1 : 1 | Especialização de serviço |
| `Serviços` → `Revisão` | 1 : 1 | Especialização de serviço |

---

## 🛠️ Ferramenta Utilizada

- **MySQL Workbench** – Para modelagem conceitual e diagrama EER.

---

## 📂 Estrutura do Repositório
