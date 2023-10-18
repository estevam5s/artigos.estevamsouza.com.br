---
description: Guia Completo do Hasura
public: true
layout: ../../layouts/BlogPost.astro
title: Hasura
createdAt: 1663635822758
updatedAt: 1663635843390
tags:
  - Hasura
heroImage: /posts/hasura.png
slug: anker-usb-c-2-in-1-card-reader
---


# Guia Completo do Hasura: Transformando Rapidamente seu Banco de Dados em uma API GraphQL

O [Hasura](https://hasura.io/)  é uma plataforma de código aberto que permite transformar instantaneamente seu banco de dados em uma API GraphQL totalmente funcional. Neste guia, vamos explorar os recursos e as capacidades do Hasura e mostrar como você pode começar a usá-lo em seus projetos.
## O que é o Hasura?

O Hasura é uma camada de serviço que se conecta ao seu banco de dados PostgreSQL e, em seguida, expõe automaticamente um endpoint GraphQL para interação com os dados do banco de dados. Isso significa que você pode criar uma API GraphQL poderosa e personalizável sem a necessidade de escrever manualmente consultas SQL ou criar uma camada de servidor personalizada.
## Vantagens do Hasura 
- **Rapidez** : Você pode configurar uma API GraphQL totalmente funcional em questão de minutos. 
- **Escalabilidade** : O Hasura é escalável e pode lidar com cargas de tráfego significativas. 
- **Segurança** : O Hasura inclui controles de segurança e autorização para proteger seus dados. 
- **Real-time** : Suporta consultas em tempo real (subscrições) para obter atualizações em tempo real dos dados. 
- **Extensibilidade** : Você pode adicionar lógica de negócios personalizada usando webhooks.
## Configuração Inicial
### Passo 1: Instalação

Primeiro, você precisa instalar o Hasura. Você pode fazer isso usando o Docker Compose ou implantando-o no Kubernetes. Para este guia, usaremos o Docker Compose. 
1. Crie um arquivo `docker-compose.yaml` com o seguinte conteúdo:

```yaml
version: '3.7'
services:
  hasura:
    image: hasura/graphql-engine:latest
    ports:
      - "8080:8080"
    environment:
      HASURA_GRAPHQL_DATABASE_URL: "postgres://user:password@your-db:5432/your-db"
      HASURA_GRAPHQL_ENABLE_CONSOLE: "true"
```



Substitua `"user"`, `"password"`, `"your-db"`, e `"your-db"` pelas informações do seu banco de dados PostgreSQL.
1. Execute o Hasura:

```bash
docker-compose up -d
```


### Passo 2: Acesso à Console

O Hasura possui uma interface de administração que você pode acessar em `http://localhost:8080`.
### Passo 3: Configurando o Schema

Na interface do Hasura, você pode criar tabelas, definir relacionamentos e especificar permissões. 
1. Na seção "Data" da interface, você pode adicionar suas tabelas e relacionamentos. 
2. Na seção "Permissions", você pode definir permissões para controlar quem pode acessar os dados.
### Passo 4: Testando a API GraphQL

Agora que seu schema está configurado, você pode acessar a API GraphQL em `http://localhost:8080/v1/graphql`. Experimente criar consultas e mutações para acessar seus dados.
## Usando o Hasura em seu Projeto

Para usar o Hasura em seu projeto, você pode fazer solicitações à API GraphQL do Hasura usando qualquer cliente GraphQL, como Apollo Client em JavaScript ou Relay em React. Aqui está um exemplo de como você pode fazer uma consulta usando o Apollo Client:

```javascript
import { ApolloClient, InMemoryCache, createHttpLink } from '@apollo/client';

const httpLink = createHttpLink({
  uri: 'http://localhost:8080/v1/graphql',
});

const client = new ApolloClient({
  link: httpLink,
  cache: new InMemoryCache(),
});

// Exemplo de consulta GraphQL
client.query({
  query: gql`
    query {
      users {
        id
        name
        email
      }
    }
  `,
})
  .then(result => console.log(result));
```


## Adicionando Lógica de Negócios Personalizada

O Hasura permite que você adicione lógica de negócios personalizada usando webhooks. Você pode definir gatilhos que invocam webhooks em resposta a eventos específicos no banco de dados. Isso permite estender a funcionalidade do seu aplicativo de maneira flexível.
## Conclusão

O Hasura é uma ferramenta poderosa para simplificar o desenvolvimento de APIs GraphQL, oferecendo rapidez e flexibilidade. Com a capacidade de se conectar ao seu banco de dados PostgreSQL e criar uma API GraphQL totalmente funcional, o Hasura é uma escolha valiosa para desenvolvedores que desejam acelerar o processo de desenvolvimento e criar aplicativos escaláveis com facilidade. Experimente o Hasura em seu próximo projeto e aproveite a velocidade e a eficiência que ele oferece.
