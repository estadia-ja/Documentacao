<!-- docker compose exec app npx prisma migrate dev -->
# Docker

Esta seção é o guia principal para configurar e rodar todo o ecossistema do projeto "Estadia Já" usando Docker.

## Por que usamos Docker?

Nosso projeto é dividido em múltiplos repositórios e serviços (Frontend, Backend, Autenticação), cada um com suas próprias dependências (Node 18, Node 20, Postgres, etc.). O Docker é essencial por três motivos:

* **Padronização:** Garante que todos os desenvolvedores rodem os serviços exatamente com as mesmas versões, eliminando o problema de "funciona na minha máquina".
* **Gerenciamento de Microsserviços:** Permite que nossos três repositórios rodem de forma isolada, mas se comuniquem perfeitamente através de uma rede Docker única (`estadia_ja_network`).
* **Simplificação do Setup:** Automatiza a criação de toda a infraestrutura necessária (banco de dados principal, banco de testes, DBeaver) com poucos comandos.

---

## Passo a Passo para Rodar o Projeto

Para subir todo o ambiente, você precisará de **3 terminais abertos**, um para cada repositório.

### Passo 1: Configuração dos Ambientes (.env)

Você precisa criar os arquivos `.env` em dois locais:

**1. No Repositório Backend (o principal):**

Crie um arquivo `.env` na raiz deste repositório. Ele é o mais importante, pois define as credenciais do banco de dados que serão usadas por todos.

    ```ini
        # Database
        POSTGRES_USER=postgres
        POSTGRES_PASSWORD=senha123
        POSTGRES_DB=estadia_db
        DATABASE_URL=postgresql://postgres:senha123@db:5432/estadia_db

        # Node App
        PORT=3000
        NODE_ENV=development

        # CloudBeaver
        CB_SERVER_NAME=CloudBeaver
        CB_ADMIN_NAME=admin
        CB_ADMIN_PASSWORD=admin

        JWT_SECRET="sua_chave_secreta_forte_para_desenvolvimento_123"
    ```

Crie um arquivo `.env.test` na raiz deste repositório. Ele será muito importante para os testes de integração, pois define as credenciais do banco de teste que será usado.

    ```ini
        #Database
        DATABASE_URL="postgresql://postgres:senha123@localhost:5434/estadia_test_db"
        POSTGRES_USER=postgres
        POSTGRES_PASSWORD=senha123
        POSTGRES_DB=estadia_test_db

        JWT_SECRET="esta_e_uma_chave_secreta_para_testes_12345"
    ```

**2. No Repositório de Autenticação:**

Crie um arquivo `.env` na raiz deste repositório. Ele precisa das credenciais do banco (para se conectar) e das suas próprias variáveis.

    ```ini
        # Database
        POSTGRES_USER=postgres
        POSTGRES_PASSWORD=senha123
        POSTGRES_DB=estadia_db
        DATABASE_URL=postgresql://postgres:senha123@db:5432/estadia_db

        # Node App
        PORT=3000
        NODE_ENV=development

        # CloudBeaver
        CB_SERVER_NAME=CloudBeaver
        CB_ADMIN_NAME=admin
        CB_ADMIN_PASSWORD=admin

        JWT_SECRET="sua_chave_secreta_forte_para_desenvolvimento_123"
    ```

### Passo 2: Criar a Rede (Apenas uma vez)

Antes de tudo, crie a rede externa que conectará todos os serviços:

    ```bash
        docker network create estadia_ja_network
    ```

### Passo 3: Subir os Serviços (3 Terminais)

Com os arquivos `.env` prontos e a rede criada, abra um terminal para cada repositório e execute os comandos:

**Terminal 1: Backend (Infraestrutura)**
(Este é o mais importante, suba ele primeiro)

    ```bash
        # No diretório do repositório Backend
        docker compose up -d
    ```
    *(Isso irá iniciar: `db`, `db-test`, `dbeaver` e o `app` principal)*

**Terminal 2: Autenticação**
(Espere pelo menos o container do banco de dados subir.)

    ```bash
        # No diretório do repositório Autenticação
        docker compose up -d
    ```
    *(Isso irá iniciar: `auth-service` conectado com o db que o Backend subiu)*

**Terminal 3: Frontend**

    ```bash
        # No diretório do repositório Frontend
        docker compose up -d
    ```
    *(Isso irá iniciar: `frontend`)*

### Passo 4: Acessar os Serviços

Seu ambiente completo está no ar!

* **Frontend (App):** `http://localhost:5173`
* **Backend (API Principal):** `http://localhost:3000`
* **Backend (API Autenticação):** `http://localhost:3001`
* **Banco de Dados (DBeaver):** `http://localhost:8978`

---

## Rodando Migrations (Prisma)

As migrações do banco de dados devem ser executadas **dentro** dos containers de backend.

**Importante:** O Backend e a Autenticação têm o mesmo banco de dados (ou shema) e, portanto, você precisa realizar a mesma migração nos dois.

**Para rodar as migrações do Backend Principal:**

    ```bash
        # No diretório do repositório Backend
        docker compose exec app npx prisma migrate dev
    ```

**Para rodar as migrações do serviço de Autenticação:**

    ```bash
        # No diretório do repositório Autenticação
        docker compose exec auth-service npx prisma migrate dev
    ```

---

## Rodando os Testes

Os testes são executados de formas diferentes em cada repositório:

**1. Testes do Backend (Principal):**

O `docker-compose.yml` do backend já possui um serviço dedicado (`tester`) para rodar todos os testes (unitários e integração) em um ambiente limpo.

    ```bash
        # No diretório do repositório Backend
        # Este comando sobe o db-test, roda os testes e se desliga.
        docker compose run --rm tester
    ```

Caso queria rodar só os unitários ou só os de integração rode esses comandos.

    ```bash
        #Unitários
        docker compose exec app npm unit:test

        #Integração
        docker compose exec app npm test:integration:run
    ```


**2. Testes do Frontend:**

No Frontend foi implementado os teste end-to-end com selenium e para rodalos rode os comandos

    ```bash
        node e2e/clientLifeCycle.js
        node e2e/ownerLifeCycle.js
    ```

**3. Testes da Autenticação:**

Atualmente o serviço de autenticação só possui testes unitários e para roda-los rode esses comandos:

    ```bash
        docker compose exec auth-service npm test

        #ou 

        docker compose exec auth-service npm test:coverage
    ```


## Histórico de Commits

|    Data    |   Tipo   |                              Descrição                            |
| :--------- | :------- | :---------------------------------------------------------------- |
| 31/10/2025 | **feat** | Adiciona documentação inicial do Docker. |
| 24/11/2025 | **feat e fix** | Adiciona documentação dos testes do Front e Autenticação e muda os .env de configuração. |