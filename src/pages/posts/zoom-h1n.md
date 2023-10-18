---
description: Prisma + Nestjs + GraphQL
slug: zoom-h1n
public: true
layout: ../../layouts/BlogPost.astro
title: Prisma
createdAt: 1663635962095
updatedAt: 1663636477234
tags:
  - ORM
heroImage: /posts/nestjs_prisma_graphql.png
---


# Para criar uma API RESTful com Prisma, GraphQL, PostgreSQL e Nest.js, siga estas etapas:

**Passo 1: Configuração Inicial** 

Certifique-se de que você tenha o Node.js e o PostgreSQL instalados em seu sistema. Em seguida, crie um novo projeto Nest.js usando o Nest CLI:

```bash
npx @nestjs/cli new nest-graphql-prisma
cd nest-graphql-prisma
```



**Passo 2: Instale as Dependências** 

Instale as dependências necessárias, incluindo o Prisma, GraphQL e outras bibliotecas relacionadas:

```bash
npm install @nestjs/graphql graphql-tools graphql apollo-server-express @prisma/client prisma
```



**Passo 3: Configurar o Prisma** 

Configure o Prisma para se conectar ao PostgreSQL. Execute o comando para criar um arquivo `schema.prisma` na pasta `prisma` e defina o esquema do banco de dados:

```bash
npx prisma init
```



Edite o arquivo `schema.prisma` de acordo com suas necessidades para definir os modelos de dados e configurações de banco de dados.

**Passo 4: Criar os Modelos GraphQL** 

Crie os modelos GraphQL para definir como os dados serão expostos via GraphQL. Você pode criar um arquivo, por exemplo, `task.graphql` no diretório `src`:

```graphql
# src/task.graphql

type Task {
  id: Int
  title: String
  description: String
  done: Boolean
}

input CreateTaskInput {
  title: String!
  description: String
}
```



**Passo 5: Criar o Resolver GraphQL** 

Crie um resolver GraphQL que irá lidar com as consultas e mutações. Você pode criar um arquivo, por exemplo, `tasks.resolver.ts` no diretório `src`:

```typescript
// src/tasks.resolver.ts

import { Resolver, Query, Mutation, Args } from '@nestjs/graphql';
import { PrismaService } from './prisma.service';
import { Task, CreateTaskInput } from './task.graphql';

@Resolver()
export class TasksResolver {
  constructor(private readonly prismaService: PrismaService) {}

  @Query(() => [Task])
  async tasks(): Promise<Task[]> {
    return this.prismaService.task.findMany();
  }

  @Mutation(() => Task)
  async createTask(@Args('input') input: CreateTaskInput): Promise<Task> {
    return this.prismaService.task.create({
      data: input,
    });
  }
}
```



**Passo 6: Configurar o Prisma Service** 

Crie um serviço para interagir com o Prisma e o banco de dados. Crie um arquivo, por exemplo, `prisma.service.ts`, no diretório `src`:

```typescript
// src/prisma.service.ts

import { Injectable } from '@nestjs/common';
import { PrismaClient } from '@prisma/client';

@Injectable()
export class PrismaService {
  constructor() {
    this.prisma = new PrismaClient();
  }
}
```



**Passo 7: Configurar o Apollo Server** 

Configure o Apollo Server Express para criar uma instância do GraphQL. Você pode fazer isso no arquivo `main.ts`:

```typescript
import { ApolloServer } from 'apollo-server-express';

const server = new ApolloServer({
  typeDefs, // Defina seu esquema GraphQL aqui
  resolvers, // Importe seus resolvers
  context: ({ req }) => ({ req }),
});

server.applyMiddleware({ app });

// Resto do código do main.ts
```



**Passo 8: Definir o Esquema GraphQL** 

No arquivo `main.ts`, importe e defina seus tipos GraphQL e resolvers:

```typescript
import { typeDefs } from './src/task.graphql'; // Importe o esquema GraphQL
import { resolvers } from './src/tasks.resolver'; // Importe os resolvers
```



**Passo 9: Executar o Servidor** 

Agora você pode executar o servidor Nest.js:

```bash
npm run start
```



Acesse o GraphQL Playground em `http://localhost:3000/graphql` e comece a testar suas consultas e mutações.

Isso é uma visão geral de como criar uma API RESTful com Prisma, GraphQL, PostgreSQL e Nest.js.