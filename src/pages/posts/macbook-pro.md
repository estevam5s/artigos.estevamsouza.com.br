---
description: Criando uma API RESTful Profissional
slug: Backend
public: true
layout: ../../layouts/BlogPost.astro
title: Typescript
createdAt: 1663205542000
updatedAt: 1663138785310
tags:
  - Backend
heroImage: /posts/Nest_TS_90e48e5541.png
---


# Criação de uma API RESTful com TypeScript e Nest.js

## Tópico 1: Configuração Inicial
### 1.1 Instalação e Configuração

```bash
npm install -g @nestjs/cli
nest new my-nest-api
```


## Tópico 3: Controladores e Rotas
### 3.1 Criando Controladores

```bash
nest generate controller app
```


### 3.2 Definindo Rotas

```typescript
// app.controller.ts
import { Controller, Get } from '@nestjs/common';

@Controller('app')
export class AppController {
  @Get()
  getAppInfo() {
    return 'Bem-vindo à sua API Nest.js com TypeScript!';
  }
}
```


## Tópico 7: Serviços e Lógica de Negócios
### 7.1 Criando Serviços

```typescript
// app.service.ts
import { Injectable } from '@nestjs/common';

@Injectable()
export class AppService {
  getAppInfo(): string {
    return 'Bem-vindo à sua API Nest.js com TypeScript!';
  }
}
```


### 7.2 Conexão a Bancos de Dados

```typescript
// app.service.ts
import { Repository } from 'typeorm';

@Injectable()
export class AppService {
  constructor(
    @InjectRepository(User)
    private readonly userRepository: Repository<User>,
  ) {}

  async findUser(id: number): Promise<User> {
    return this.userRepository.findOne(id);
  }
}
```


## Tópico 11: Documentação da API
### 11.1 Gerando Documentação

```typescript
// main.ts
import { NestFactory } from '@nestjs/core';
import { SwaggerModule, DocumentBuilder } from '@nestjs/swagger';

async function bootstrap() {
  const app = await NestFactory.create(AppModule);
  const options = new DocumentBuilder()
    .setTitle('Minha API Nest.js')
    .setDescription('API RESTful com Swagger')
    .setVersion('1.0')
    .addTag('api')
    .build();
  const document = SwaggerModule.createDocument(app, options);
  SwaggerModule.setup('api', app, document);
  await app.listen(3000);
}
bootstrap();
```
