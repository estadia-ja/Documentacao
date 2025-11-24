# Frontend

Esta seção detalha as tecnologias, configurações e a estrutura da interface web do projeto "Estadia Já".

O frontend é uma aplicação web estruturada em múltiplas rotas, desenvolvida para atender diferentes perfis de usuários (locatários e proprietários), garantindo uma navegação clara entre a busca, visualização e gerenciamento de reservas.

---

## Links dos Repositórios

* **Repositório de Frontend:** [Repositório](https://github.com/estadia-ja/Frontend)

---

## Tecnologias (Stack)

As principais ferramentas e bibliotecas utilizadas no desenvolvimento da interface são:

* **Biblioteca Principal:** React 
* **Estilização:** Tailwind CSS
* **Roteamento:** React Router DOM
* **Gerenciamento de Estado:** Context API / Hooks
* **Consumo de API:** Axios
* **Ícones:** Lucide React
* **Testes E2E:** Selenium WebDriver (JavaScript/Node)
* **Build Tool:** Vite

---

## Testes End-to-End (E2E)

Para garantir a qualidade do fluxo do usuário, utilizamos testes automatizados de ponta a ponta com **Selenium**.

### O que é testado?
Os testes simulam o comportamento de um usuário real no navegador (cliente ou proprietário), cobrindo fluxos críticos como: <br>
1. Login e Autenticação.<br>
2. Busca e filtro de imóveis.<br>
3. Fluxo de reserva.<br>
4. Cadastro de imóvel

### Como rodar os testes
Para executar os scripts de teste Selenium localmente:

```bash
    # Instalar dependências de teste
    npm install

    # Executar suite de testes
    node e2e/clientLifeCycle.js
    node e2e/ownerLifeCycle.js
```

## Histórico de Commits

|    Data    |   Tipo   |                              Descrição                            |
| :--------- | :------- | :---------------------------------------------------------------- |
| 24/11/2025 | **feat** | Adiciona documentação inicial do Frontend. |