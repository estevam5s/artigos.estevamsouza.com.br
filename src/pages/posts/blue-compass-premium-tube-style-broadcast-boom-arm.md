---
description: Criando uma REST API
public: true
layout: ../../layouts/BlogPost.astro
title: Hasura
createdAt: 1663635792232
updatedAt: 1663635814121
tags:
  - Hasura
heroImage: /posts/restapi.jpg
slug: blue-compass-premium-tube-style-broadcast-boom-arm
---


# Criando uma REST API com Hasura, Docker, PostgreSQL e GraphQL

Neste blog, vamos explorar como criar uma REST API com a ajuda do Hasura, uma plataforma GraphQL de código aberto, juntamente com Docker e PostgreSQL. Vamos abordar a configuração inicial, o uso do Hasura para criar uma API GraphQL e, em seguida, como expor essa API como uma REST API.
## O que é Hasura?

O [Hasura](https://hasura.io/)  é uma plataforma de código aberto que simplifica o desenvolvimento de APIs GraphQL. Ele se integra diretamente com um banco de dados PostgreSQL e fornece recursos de autorização, autenticação e lógica de negócios personalizada. O Hasura torna mais fácil criar APIs escaláveis e eficientes em um tempo mínimo.
## Configuração Inicial
### Passo 1: Instalação do Docker e Docker Compose

Certifique-se de ter o Docker e o Docker Compose instalados em seu sistema. Você pode encontrar instruções de instalação em [https://docs.docker.com/get-docker/](https://docs.docker.com/get-docker/) .
### Passo 2: Configurando o Ambiente

Crie um diretório para o projeto e crie um arquivo `docker-compose.yaml` com o seguinte conteúdo:

```yaml
version: '3'
services:
  hasura:
    image: hasura/graphql-engine
    ports:
      - "8080:8080"
    environment:
      HASURA_GRAPHQL_DATABASE_URL: postgres://user:password@postgres:5432/mydb
      HASURA_GRAPHQL_ADMIN_SECRET: myadminsecret
  postgres:
    image: postgres
    environment:
      POSTGRES_DB: mydb
      POSTGRES_USER: user
      POSTGRES_PASSWORD: password
```



Certifique-se de substituir `"user"`, `"password"`, `"mydb"`, e `"myadminsecret"` pelas informações do seu banco de dados.
### Passo 3: Inicializando o Ambiente

No diretório do projeto, execute o seguinte comando para iniciar o Hasura e o PostgreSQL:

```bash
docker-compose up -d
```



Isso iniciará o Hasura em `http://localhost:8080`.
## Usando o Hasura para Criar uma API GraphQL

O Hasura fornece uma interface de administração que permite definir o esquema GraphQL, tabelas e relações. Siga estas etapas para criar um esquema simples:
### Passo 1: Acessando a Interface do Hasura

Acesse a interface do Hasura em `http://localhost:8080`.
### Passo 2: Definindo o Schema 
1. Clique na guia "Data" na interface do Hasura. 
2. Clique em "Track All" para adicionar todas as tabelas do banco de dados ao seu schema GraphQL.
### Passo 3: Configurando Permissões 
1. Clique na guia "Permissions". 
2. Defina as permissões para tabelas e colunas, controlando quem pode acessar e modificar os dados.
### Passo 4: Testando a API GraphQL

Agora que seu schema está configurado, você pode acessar a API GraphQL em `http://localhost:8080/v1/graphql`. Experimente criar consultas e mutações para acessar seus dados.
## Expondo a API GraphQL como REST API

Para expor a API GraphQL como REST API, você pode usar o [postgREST](http://postgrest.org/) . O postgREST é uma ferramenta que gera automaticamente uma API REST com base em um banco de dados PostgreSQL.
### Passo 1: Instalando o postgREST
1. Instale o postgREST usando o seguinte comando:

```bash
npm install -g postgrest
```

 
1. Crie um arquivo de configuração `postgrest.conf` com o seguinte conteúdo:

```json
{
  "db-uri": "postgres://user:password@postgres:5432/mydb",
  "db-schema": "public",
  "db-anon-role": "anonymous",
  "server-host": "0.0.0.0",
  "server-port": 3000,
  "jwt-secret": "myjwtsecret"
}
```



Substitua as informações do banco de dados e o segredo JWT apropriados.
### Passo 2: Inicializando o postgREST

Execute o postgREST com o seguinte comando:

```bash
postgrest postgrest.conf
```



Agora, sua API REST estará disponível em `http://localhost:3000`.
## Conclusão

Neste guia, você aprendeu a criar uma REST API usando o Hasura, Docker, PostgreSQL e GraphQL. O Hasura simplifica o processo de criação de APIs GraphQL, permitindo que você configure rapidamente seu esquema e defina permissões. Além disso, você pode expor essa API GraphQL como uma REST API usando o postgREST. Isso oferece uma maneira eficiente de criar APIs altamente flexíveis e escaláveis em um curto período de tempo. Experimente essas ferramentas em seu próximo projeto e aproveite os benefícios da velocidade de desenvolvimento e da eficiência que elas oferecem.
