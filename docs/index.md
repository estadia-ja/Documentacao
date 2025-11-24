# Bem-vindo à Documentação do Estadia Já

Bem-vindo à documentação oficial do projeto **Estadia Já**.

O **Estadia Já** é uma plataforma web completa voltada para o aluguel de casas de temporada. O sistema conecta proprietários que desejam anunciar seus imóveis a locatários que buscam a estadia perfeita, gerenciando desde a busca e visualização até a reserva e gestão de disponibilidade.

O projeto foi desenvolvido com uma arquitetura moderna baseada em microsserviços, garantindo escalabilidade e separação de responsabilidades.

---

## Deploys e Ambientes

Abaixo estão os links para acessar as versões de produção dos serviços.

| Serviço | URL de Acesso | Plataforma | Status |
| :--- | :--- | :--- | :--- |
| **Frontend (Web)** | [https://frontend-estadia-ja.vercel.app/](https://frontend-estadia-ja.vercel.app/) | **Vercel** | 🟢 Online |
| **Backend (API)** | [https://estadia-ja-backend.onrender.com/docs/](https://estadia-ja-backend.onrender.com/docs/) | **Render** | 🟢 Online |
| **Auth Service** | [https://autenticacao-3uun.onrender.com/docs/](https://autenticacao-3uun.onrender.com/docs/) | **Render** | 🟢 Online |
| **Documentação** | *Você está aqui* | **Vercel/Pages** | 🟢 Online |

---

## Decisões de Infraestrutura

Para o deploy da aplicação, adotamos uma estratégia híbrida focada em performance e facilidade de CI/CD:

### Por que Vercel para o Frontend?
Optamos pela **Vercel** para hospedar o cliente React devido à sua integração nativa com o ecossistema Javascript e otimização para SPAs e aplicações web modernas.
* **Performance:** CDN global (Edge Network) garante carregamento rápido dos ativos estáticos.
* **CI/CD:** Deploy automático a cada push na branch `main`.
* **Preview:** Geração de links de preview para Pull Requests.

### Por que Render para o Backend?
Escolhemos o **Render** para hospedar nossos serviços Node.js (API e Auth) e o Banco de Dados.
* **Suporte a Docker:** O Render possui suporte nativo e robusto para containers Docker, permitindo que subamos exatamente o mesmo ambiente definido no nosso `docker-compose`.
* **Serviços Gerenciados:** Facilidade na configuração e manutenção do banco de dados PostgreSQL.
* **Persistência:** Melhor gerenciamento de conexões persistentes (WebSockets, DB connections) comparado a funções serverless puras.

---

## Guia de Navegação

A documentação está organizada seguindo a estrutura de pastas do projeto para facilitar a localização de informações técnicas. Utilize o menu lateral para navegar:

1.  **Arquitetura:**
    * Visão geral da arquitetura em camadas e MVC.
    * Diagramas de componentes e comunicação entre microsserviços.
    
2.  **Backend & Autenticação:**
    * Detalhes técnicos dos serviços Node.js/Express.

3.  **Frontend:**
    * Estrutura do projeto React e Tailwind CSS.
    * Lógica de rotas e perfis de usuário (Proprietário vs. Locatário).
    * Configuração dos testes E2E com Selenium.

4.  **Banco de Dados:**
    * Modelagem de dados (DER Conceitual).
    * Scripts de migração.

5.  **DevOps & Qualidade:**
    * Configurações de Docker e Docker Compose.
    * Pipelines de CI/CD (GitHub Actions).
    * Estratégias de testes (Unitários com Vitest e Integração).

---

## Stack Tecnológico Resumido

* **Linguagem:** TypeScript / JavaScript (Node.js)
* **Frontend:** React, Tailwind CSS, Vite
* **Backend:** Express, Node.js
* **Database:** PostgreSQL, Prisma ORM
* **Testes:** Vitest (Unit/Int), Selenium (E2E)
* **Infra:** Docker, Vercel, Render

---

## Histórico de Commits

|    Data    |   Tipo   |                              Descrição                            |
| :--------- | :------- | :---------------------------------------------------------------- |
| 24/11/2025 | **feat** | Adiciona documentação inicial sobre o projeto. |