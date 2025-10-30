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

## Configuração de Ambiente (.env)

Cada serviço de backend (ex: `auth-service`) possui seu próprio arquivo `.env` para configuração e outro para teste.

**Importante:** As variáveis `POSTGGRES_USER`, `POSTGRES_PASSWORD` e `POSTGRES_DB` são geralmente definidas em um arquivo `.env` na **raiz do projeto**, que é lido pelo `docker-compose`. O serviço então as utiliza para construir a `DATABASE_URL`.

Arquivo `.env` para o `auth-service`:

```ini
    PORT=3000
    
    DATABASE_URL="postgresql://USUARIO_POSTGRES:SENHA_POSTGRES@db:5432/NOME_DO_BANCO?schema=public"
    
    JWT_SECRET="SUA_CHAVE_SECRETA_AQUI"
```

Arquivo `.env.test` para o `auth-service`:

```ini
    PORT=3000
    
    DATABASE_URL="postgresql://USUARIO_POSTGRES:SENHA_POSTGRES@db:5432/NOME_DO_BANCO?schema=public"
    
    JWT_SECRET="SUA_CHAVE_SECRETA_AQUI"
```

Arquivo `.env` para a `api`:

```ini
    PORT=3000
    
    DATABASE_URL="postgresql://USUARIO_POSTGRES:SENHA_POSTGRES@db:5432/NOME_DO_BANCO?schema=public"
    
    JWT_SECRET="SUA_CHAVE_SECRETA_AQUI"
```

Arquivo `.env.test` para a `api`:

```ini
    PORT=3000
    
    DATABASE_URL="postgresql://USUARIO_POSTGRES:SENHA_POSTGRES@db:5432/NOME_DO_BANCO?schema=public"
    
    JWT_SECRET="SUA_CHAVE_SECRETA_AQUI"
```

---

## Documentação da API (Swagger)

Graças ao `swagger-ui-express`, a documentação da API de cada serviço é gerada automaticamente e pode ser acessada no navegador em sua respectiva porta (quando o projeto estiver rodando).

* **Exemplo (auth-service):** `http://localhost:3001/docs`
* **Exemplo (property-service):** `http://localhost:3000/docs` 

## Histórico de Commits

|    Data    |   Tipo   |                              Descrição                            |
| :--------- | :------- | :---------------------------------------------------------------- |
| 30/10/2025 | **feat** | Adiciona documentação inicial do Bckend. |