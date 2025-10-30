# Documentação da Arquitetura do Backend

Nossa arquitetura de backend é baseada em um modelo **orientado a domínios de negócio**. Essa abordagem divide a aplicação em módulos, onde cada módulo é uma **camada de domínio** que encapsula toda a lógica e dados de uma funcionalidade específica (como `user`, `produto`, `pagamento`). Dentro de cada domínio, aplicamos o padrão **MVC (Model-View-Controller)** para organizar o código.

Essa escolha garante a **separação de responsabilidades**, **manutenção simplificada** e a preparação ideal para uma futura migração para **microsserviços**.

---

### 1. Estrutura das Camadas de Domínio (Baseada em MVC)

Cada domínio de negócio atua como uma **camada modular** que contém toda a lógica necessária para sua funcionalidade. A organização interna de cada domínio segue o padrão MVC, com responsabilidades bem definidas:

* **Camada de Apresentação (`routes.js`)**:
    * **Função**: Responsável por receber as requisições HTTP e atuar como o ponto de entrada da API.
    * **Responsabilidade**: Define os endpoints (por exemplo, `POST /users`) e direciona as requisições para o `Controller` do domínio.

* **Camada de Lógica de Negócio (`controller.js` e `service.js`)**:
    * **Função**: Contém a lógica central da aplicação e orquestra as operações.
    * **Responsabilidade**: O **Controller** recebe as requisições da camada de apresentação e chama o **Service**, que por sua vez executa as regras de negócio, validações e coordenação de ações.

* **Camada de Acesso a Dados (`model.js`)**:
    * **Função**: Interage diretamente com o banco de dados.
    * **Responsabilidade**: O **Model** lida com a entidade e utiliza o Prisma para realizar operações de **CRUD** (Criar, Ler, Atualizar, Deletar), garantindo a integridade dos dados.

---

### 2. Estrutura de Pastas do Projeto

A estrutura de pastas reflete a arquitetura de domínio e ajuda a manter a organização e a escalabilidade do projeto.

```plaintext
    src/
    ├── clientValuation/
    │   ├── controller.js
    │   ├── model.js
    │   ├── routes.js
    │   ├── service.js
    │   └── test/
    │   │   ├── clientValuation.controller.unit.test.js
    │   │   ├── clientValuation.integration.unit.test.js
    │   │   ├── clientValuation.model.unit.test.js
    │   │   └── clientValuation.service.unit.test.js
    ├── middlewares/
    │   ├── authMiddleware.js
    │   ├── clientValuationValidation.js
    │   ├── paymentValidation.js
    │   ├── propertyValidation.js
    │   ├── propertyValuationValidation.js
    │   ├── reserveValidation.js
    │   └── validation.js
    ├── payment/
    │   ├── controller.js
    │   ├── model.js
    │   ├── routes.js
    │   ├── service.js
    │   └── test/
    │   │   ├── payment.controller.unit.test.js
    │   │   ├── payment.integration.unit.test.js
    │   │   ├── payment.model.unit.test.js
    │   │   └── payment.service.unit.test.js
    ├── property/
    │   ├── controller.js
    │   ├── model.js
    │   ├── routes.js
    │   ├── service.js
    │   └── test/
    │   │   ├── property.controller.unit.test.js
    │   │   ├── property.integration.unit.test.js
    │   │   ├── property.model.unit.test.js
    │   │   └── property.service.unit.test.js
    ├── propertyValuation/
    │   ├── controller.js
    │   ├── model.js
    │   ├── routes.js
    │   ├── service.js
    │   └── test/
    │   │   ├── propertyValuation.controller.unit.test.js
    │   │   ├── propertyValuation.integration.unit.test.js
    │   │   ├── propertyValuation.model.unit.test.js
    │   │   └── propertyValuation.service.unit.test.js
    ├── reserve/
    │   ├── controller.js
    │   ├── model.js
    │   ├── routes.js
    │   ├── service.js
    │   └── test/
    │   │   ├── reserve.controller.unit.test.js
    │   │   ├── reserve.integration.unit.test.js
    │   │   ├── reserve.model.unit.test.js
    │   │   └── reserve.service.unit.test.js
    ├── user/
    │   ├── controller.js
    │   ├── model.js
    │   ├── routes.js
    │   ├── service.js
    │   └── test/
    │   │   ├── user.controller.unit.test.js
    │   │   ├── user.integration.unit.test.js
    │   │   ├── user.model.unit.test.js
    │   │   └── user.service.unit.test.js
    ├── validations/
    │   ├── clientValuationValidation.js
    │   ├── paymentValidation.js
    │   ├── propertyValidation.js
    │   ├── propertyValuationValidation.js
    │   ├── reserveValidation.js
    │   └── userValidation.js
    ├── app.js    
    ├── database.js
    ├── index.js
    └── swagger.js
```

* **`src/`**: Diretório principal que contém todo o código fonte da aplicação.
* **`src/user/`**: Representa um **domínio de negócio**. Essa estrutura será replicada para cada nova entidade, como `src/product/`, `src/payment/`, etc.
* **`src/middlewares/`**: Armazena middlewares genéricos que podem ser aplicados em diversas rotas, como middlewares de autenticação ou de logs.
* **`src/validations/`**: Contém as regras de validação específicas para cada entidade, garantindo que os dados que chegam ao Service estejam corretos.
* **`database.js`**: Isola a configuração e a conexão com o banco de dados, facilitando a troca de provedores de banco de dados no futuro.
* **`index.js`**: O ponto de entrada da aplicação.
* **`swagger.js`**: Arquivo de configuração para a documentação da API (Swagger/OpenAPI).

---

### 3. Fluxo de Dados (Request-Response)

O fluxo de uma requisição HTTP dentro de um domínio segue a seguinte sequência:

1.  A requisição chega ao arquivo de **rotas** (`routes.js`) na **Camada de Apresentação**.
2.  A rota a direciona para o **Controller** (`controller.js`).
3.  O `Controller` delega a lógica para o **Service** (`service.js`) na **Camada de Lógica de Negócio**.
4.  O `Service` interage com o **Model** (`model.js`) na **Camada de Acesso a Dados**.
5.  O `Model` usa o **Prisma** para a comunicação com o banco de dados.
6.  O resultado é retornado do `Model` para o `Service`, depois para o `Controller`, que formata a resposta e a envia de volta ao cliente.

---

### Histórico de Commits

|    Data    |   Tipo   |                              Descrição                            |
| :--------- | :------- | :---------------------------------------------------------------- |
| 22/09/2025 | **feat** | Adiciona a documentação da arquitetuta que o Banckend está usando |
| 22/09/2025 | **feat** | Atualiza a estrutura de pastas |
