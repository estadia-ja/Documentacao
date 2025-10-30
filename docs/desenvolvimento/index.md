# Visão Geral (Desenvolvimento)

Esta seção é o guia central para qualquer desenvolvedor que queira configurar e rodar o projeto **"Estadia Já"** em sua máquina local.

---

## Pré-requisitos

Antes de começar, garanta que você tenha as seguintes ferramentas instaladas:

- **Git**
- **Docker**
- **Docker Compose**

---

## Arquitetura de Alto Nível

O projeto é dividido em múltiplos **serviços containerizados** que se comunicam através da rede `estadia_ja_network`:

1. **Frontend:** Aplicação Web (React) responsável pela interface do usuário.  
2. **Backend:** API REST (Node.js/Express) que gerencia a lógica de negócio (ex: propriedades, reservas).  
3. **Autenticação:** API REST (Node.js/Express) que gerencia o login dos usuários (`auth-service`).  
4. **Banco de Dados:** (PostgreSQL) Armazenamento persistente dos dados.


Um diagrama simples da comunicação:

## Histórico de Commits

|    Data    |   Tipo   |                              Descrição                            |
| :--------- | :------- | :---------------------------------------------------------------- |
| 30/10/2025 | **feat** | Adiciona a visão geral. |
