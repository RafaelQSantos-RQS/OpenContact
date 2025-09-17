# OpenContact

Este é o repositório principal do projeto OpenContact, uma aplicação de gerenciamento de contatos composta por uma API RESTful (Java com Spring Boot) e um frontend (Angular). O projeto foi construído para ser executado de forma simples e unificada usando o Docker Compose.

## ✨ Funcionalidades

### Backend (API)

- **Gerenciamento de Agendas e Contatos**: Ciclo de vida completo (CRUD) para ambas as entidades.
- **Listagem Otimizada**: Listagem paginada e com filtros dinâmicos por nome e telefone para os contatos.
- **Controle de Versão de Banco de Dados**: Schema versionado com Liquibase, incluindo um seed de dados de exemplo para desenvolvimento.
- **Documentação Automática**: Documentação da API interativa e completa com Swagger (OpenAPI).
- **Health Check**: Endpoint para monitoramento da saúde da aplicação e da conexão com o banco de dados.
- **Testes Automatizados**: Implementação de testes unitários e de integração.

### Frontend

- **Interface Moderna**: Desenvolvida como uma Single-Page Application (SPA) com as melhores práticas do Angular 20+.
- **Gerenciamento de Agendas**: Criação, edição, listagem em formato de card e exclusão de agendas com diálogos de confirmação.
- **Gerenciamento de Contatos**: Funcionalidades CRUD completas para contatos de uma agenda específica.
- **Tabela de Dados Interativa**: A tabela de contatos possui paginação e busca em tempo real, otimizando a performance com RxJS.
- **UI Profissional**: Interface construída com Angular Material, com um layout coeso e ícones customizados.
- **Containerização Otimizada**: `Dockerfile` multi-stage que gera uma imagem leve e flexível com Nginx.

## 🛠️ Stack de Tecnologias

- **Backend:** Java 21, Spring Boot 3.5.5, Spring Data JPA, Springdoc OpenAPI, Maven.
- **Frontend:** Angular 20+, TypeScript, SCSS, RxJS, Angular Material.
- **Banco de Dados:** PostgreSQL 17.6.
- **Versionamento de Schema:** Liquibase.
- **Containerização:** Docker e Docker Compose.

## ▶️ Como Executar com Docker Compose

O arquivo `docker-compose.yaml` na raiz do projeto orquestra a API, o Frontend e o banco de dados, criando um ambiente de desenvolvimento completo e pronto para uso.

1. **Pré-requisitos**:

      - [Git](https://git-scm.com/)
      - [Docker](https://www.docker.com/products/docker-desktop/) e [Docker Compose](https://docs.docker.com/compose/)

2. **Clone o repositório principal**:

    ```bash
    git clone https://github.com/RafaelQSantos-RQS/OpenContact.git
    cd OpenContact
    ```

3. **Crie seu arquivo de ambiente**:
    Copie o template para criar o arquivo `.env` que será usado pelo Docker Compose. As configurações padrão já são suficientes para o ambiente de desenvolvimento.

    ```bash
    cp .env.template .env
    ```

    Conteúdo de `.env.template`:

    ```ini
    # Database
    POSTGRES_USER=opencontact
    POSTGRES_PASSWORD=opencontact
    POSTGRES_DB=opencontact

    # Fronte Settings
    BACKEND_API_URL=http://app:8080

    # Spring
    ## DataSource
    SPRING_DATASOURCE_URL="jdbc:postgresql://db:5432/${POSTGRES_DB}"
    SPRING_DATASOURCE_USERNAME="${POSTGRES_USER}"
    SPRING_DATASOURCE_PASSWORD="${POSTGRES_PASSWORD}"

    ## JPA
    JPA_DDL_AUTO=validate
    JPA_SHOW_SQL=false
    JPA_FORMAT_SQL=false

    ## Liquibase
    SPRING_LIQUIBASE_CONTEXTS=dev
    ```

4. **Inicie a aplicação**:
    Este comando irá construir as imagens necessárias (API e Frontend) e iniciar os três serviços em segundo plano.

    ```bash
    docker compose up --build -d
    ```

      - A API estará disponível em `http://localhost:8080`.
      - O Frontend estará disponível em `http://localhost:8080` (graças à configuração do Nginx no container do frontend que serve a aplicação e faz o proxy para a API).

## 📖 Documentação da API

A documentação interativa da API, gerada pelo Swagger UI, pode ser acessada após a inicialização dos containers em `http://localhost:8080/api/v1/swagger-ui.html`.

## 📈 Health Check

Para verificar a saúde dos containers, você pode usar os seguintes endpoints (após a inicialização):

- **Frontend**: O acesso a `http://localhost:8080` deve retornar a página inicial do Angular.
- **Backend**: O endpoint de saúde do Actuator pode ser acessado em `http://localhost:8080/api/v1/management/health`.
