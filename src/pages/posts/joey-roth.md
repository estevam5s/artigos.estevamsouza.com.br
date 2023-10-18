---
description: API REST com NestJS, Prisma, PostgreSQL e Swagger
public: true
layout: ../../layouts/BlogPost.astro
title: Nestjs
createdAt: 1663138617853
updatedAt: 1663138677695
tags:
  - Backend
heroImage: /posts/nestjs-prisma-rest-api.png
slug: Backend
---


# Criando uma API REST com NestJS, Prisma, PostgreSQL e Swagger

Neste guia, vamos criar uma API RESTful com TypeScript usando o framework NestJS, um banco de dados PostgreSQL através do Prisma, e documentar a API com o Swagger.
## Tópico 1: Configuração Inicial
### 1.1 Instalação de Dependências

Comece instalando as dependências necessárias em seu projeto:

```bash
npm install --save @nestjs/core @nestjs/common @nestjs/microservices @nestjs/swagger @nestjs/testing
npm install --save @nestjs/typeorm pg typeorm
npm install --save prisma @prisma/client
```


### 1.2 Configuração do Banco de Dados

Configure o banco de dados PostgreSQL no arquivo `ormconfig.json`:

```json
{
  "type": "postgres",
  "host": "localhost",
  "port": 5432,
  "username": "seu-usuario",
  "password": "sua-senha",
  "database": "sua-base-de-dados",
  "entities": ["dist/**/*.entity{.ts,.js}"],
  "synchronize": true
}
```


### 1.3 Configuração do Prisma

Configure o Prisma para gerenciar seu banco de dados PostgreSQL:

```bash
npx prisma init
```


## Tópico 2: Criando Endpoints
### 2.1 Criando Controladores

Crie controladores para definir endpoints e lógica de roteamento.

```typescript
// user.controller.ts
import { Controller, Get } from '@nestjs/common';

@Controller('users')
export class UserController {
  @Get()
  findAll(): string[] {
    return ['user1', 'user2'];
  }
}
```


### 2.2 Definindo Rotas

Configure as rotas no módulo da aplicação:

```typescript
// app.module.ts
import { Module } from '@nestjs/common';
import { UserController } from './user.controller';

@Module({
  controllers: [UserController],
})
export class AppModule {}
```


## Tópico 3: Documentação com Swagger
### 3.1 Configuração do Swagger

Configure o Swagger para documentar automaticamente a API:

```typescript
// main.ts
import { NestFactory } from '@nestjs/core';
import { SwaggerModule, DocumentBuilder } from '@nestjs/swagger';
import { AppModule } from './app.module';

async function bootstrap() {
  const app = await NestFactory.create(AppModule);

  const options = new DocumentBuilder()
    .setTitle('API Documentation')
    .setDescription('API endpoints documentation')
    .setVersion('1.0')
    .addTag('users')
    .build();

  const document = SwaggerModule.createDocument(app, options);
  SwaggerModule.setup('api', app, document);

  await app.listen(3000);
}
bootstrap();
```


## Tópico 4: Práticas Recomendadas
### 4.1 Práticas Recomendadas

Siga as práticas recomendadas do NestJS e do Prisma para criar uma API robusta e eficiente.
## Tópico 5: Conclusão
### 5.1 Aprofundando-se

Este guia fornece um ponto de partida para criar uma API RESTful com NestJS, Prisma, PostgreSQL e Swagger. Explore a documentação oficial dessas ferramentas e aprofunde-se em áreas específicas de interesse.
