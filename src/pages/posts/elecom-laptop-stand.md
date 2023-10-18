---
description: ORM
public: true
layout: ../../layouts/BlogPost.astro
title: Build REST Api with Prisma + Nestjs
createdAt: 1663636049020
updatedAt: 1663636078085
tags:
  - ORM
heroImage: /posts/prisma.png
slug: elecom-laptop-stand
---



# Criando uma REST API com Nest.js e Prisma ORM

Neste tutorial, vamos criar uma REST API simples usando o framework Nest.js e o Prisma ORM (Object-Relational Mapping) para interagir com um banco de dados. Vamos seguir as etapas a seguir: 
1. **Configuração Inicial** : Instale o Nest.js e o Prisma ORM e configure um projeto básico. 
2. **Definindo um Modelo de Dados** : Crie um modelo de dados para a nossa aplicação. 
3. **Criando um Controlador** : Crie um controlador para gerenciar as rotas da API. 
4. **Conectando ao Banco de Dados** : Configure a conexão com o banco de dados usando o Prisma. 
5. **Criando Rotas e Controladores** : Defina rotas para criar, ler, atualizar e excluir registros no banco de dados. 
6. **Testando a API** : Use uma ferramenta como o [Postman](https://www.postman.com/)  ou o [Insomnia](https://insomnia.rest/)  para testar a API.
## 1. Configuração Inicial

Certifique-se de que você tenha o Node.js instalado no seu sistema. Em seguida, vamos criar um novo projeto Nest.js e instalar o Prisma CLI:

```bash
npx @nestjs/cli new nest-prisma-api
cd nest-prisma-api
npm install @prisma/client prisma --save
```


## 2. Definindo um Modelo de Dados

Vamos criar um modelo de dados simples para um aplicativo de tarefas. No diretório `src`, crie um arquivo chamado `task.model.ts` e defina o seguinte modelo:

```typescript
// src/task.model.ts

export class Task {
  id: number;
  title: string;
  description: string;
  done: boolean;
}
```


## 3. Criando um Controlador

Agora, vamos criar um controlador para gerenciar as rotas da API. Execute o seguinte comando para gerar um controlador:

```bash
npx @nestjs/cli generate controller tasks
```



Isso criará um controlador chamado `tasks.controller.ts` no diretório `src`.
## 4. Conectando ao Banco de Dados

Configure o Prisma para se conectar ao seu banco de dados. Crie um arquivo `prisma/schema.prisma` com o seguinte conteúdo:

```prisma
generator client {
  provider = "prisma-client-js"
  output = "./src/prisma/client"
}

// Configure a conexão com o seu banco de dados
datasource db {
  provider = "sqlite"
  url      = "file:./dev.db"
}

model Task {
  id          Int      @id @default(autoincrement())
  title       String
  description String?
  done        Boolean  @default(false)
}
```



Em seguida, execute o comando para criar um cliente Prisma:

```bash
npx prisma generate
```


## 5. Criando Rotas e Controladores

Vamos definir rotas no controlador `tasks.controller.ts` para realizar operações CRUD no modelo de tarefas. Por exemplo, para criar uma nova tarefa:

```typescript
import { Controller, Get, Post, Body } from '@nestjs/common';
import { Task } from '../task.model';
import { PrismaClient } from '@prisma/client';

const prisma = new PrismaClient();

@Controller('tasks')
export class TasksController {
  @Get()
  async findAll(): Promise<Task[]> {
    return await prisma.task.findMany();
  }

  @Post()
  async create(@Body() taskData: Task): Promise<Task> {
    return await prisma.task.create({ data: taskData });
  }
}
```


## 6. Testando a API

Agora você pode usar o Postman, o Insomnia ou qualquer outra ferramenta para testar sua API. Aqui estão exemplos de endpoints: 
- **GET /tasks** : Recuperar todas as tarefas. 
- **POST /tasks** : Criar uma nova tarefa.

Lembre-se de configurar e executar o servidor Nest.js:

```bash
npm run start
```