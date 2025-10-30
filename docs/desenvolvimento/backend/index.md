# Backend

Esta seção detalha as tecnologias e configurações dos serviços de backend do projeto "Estadia Já".

O backend é composto por múltiplos microsserviços que operam em repositórios separados para garantir a separação de responsabilidades. Os principais serviços são:

* **Serviço de Autenticação**: Responsável pelo cadastro, login e gerenciamento de usuários.
* **Serviço de Negócios**: Responsável pela lógica principal da aplicação (imóveis, reservas, etc.).

---

## Links dos Repositórios

* **Repositório de Autenticação:** [Repositório](https://github.com/estadia-ja/Autenticacao)
* **Repositório de Backend:** [Repositório](https://github.com/estadia-ja/Backend)

---

## Tecnologias (Stack Comum)

O stack principal utilizado na maioria dos serviços de backend é:

* **Runtime:** Node.js (v18-alpine, conforme Dockerfile)
* **Framework:** Express.js
* **Banco de Dados:** PostgreSQL
* **ORM:** Prisma
* **Autenticação:** `bcrypt` / `bcryptjs`, `jsonwebtoken`
* **Validação:** `joi`
* **Documentação da API:** `swagger-jsdoc`, `swagger-ui-express`
* **Outros:** `cors`, `dotenv`, `multer`

---

## Documentação da API (Swagger)

Graças ao `swagger-ui-express`, a documentação da API de cada serviço é gerada automaticamente e pode ser acessada no navegador em sua respectiva porta (quando o projeto estiver rodando).

* **Exemplo (auth-service):** `http://localhost:3001/docs`
* **Exemplo (property-service):** `http://localhost:3000/docs` 

## Histórico de Commits

|    Data    |   Tipo   |                              Descrição                            |
| :--------- | :------- | :---------------------------------------------------------------- |
| 30/10/2025 | **feat** | Adiciona documentação inicial do Bckend. |