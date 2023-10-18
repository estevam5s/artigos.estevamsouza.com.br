---
description: Desenvolvendo uma Aplicação Full Stack
slug: FullStack
public: true
layout: ../../layouts/BlogPost.astro
title: NestJS + NextJS
createdAt: 1663134489800
updatedAt: 1663635618067
tags:
  - FullStack
heroImage: /posts/1_ymfz_KKMuGJpIPyvdlGnHA.png
---


# Desenvolvendo uma Aplicação Full Stack Profissional com Nest.js e Next.js

**Passo 1: Configuração do Back-end com Nest.js** 

Vamos começar criando o back-end com Nest.js, configurando um servidor RESTful básico. Certifique-se de ter o Node.js e o npm instalados em seu sistema. 
1. **Crie um novo projeto Nest.js** :
Abra seu terminal e execute os seguintes comandos para criar um novo projeto Nest.js:

```bash
npm install -g @nestjs/cli
nest new backend-project
cd backend-project
``` 
2. **Instale as Dependências** :
Instale as dependências necessárias, como o TypeORM para trabalhar com o banco de dados:

```bash
npm install @nestjs/typeorm typeorm pg
``` 
3. **Crie um Módulo, Entidade e Controlador** :
Crie um módulo, uma entidade e um controlador para gerenciar recursos. Por exemplo, vamos criar um módulo chamado `items`:

```bash
nest generate module items
nest generate controller items
``` 
4. **Defina a Entidade** :
Crie uma entidade `Item` usando o TypeORM no arquivo `items.entity.ts`:

```typescript
// src/items/items.entity.ts

import { Entity, PrimaryGeneratedColumn, Column } from 'typeorm';

@Entity('items')
export class Item {
  @PrimaryGeneratedColumn()
  id: number;

  @Column()
  name: string;

  @Column()
  description: string;
}
``` 
5. **Configure o Controlador** :
Implemente as operações CRUD no controlador `items.controller.ts`.

```typescript
// src/items/items.controller.ts

@Get()
findAll(): Promise<Item[]> {
  return this.itemsService.findAll();
}

@Get(':id')
findOne(@Param('id') id: string): Promise<Item> {
  return this.itemsService.findOne(+id);
}

@Post()
create(@Body() createItemDto: CreateItemDto): Promise<Item> {
  return this.itemsService.create(createItemDto);
}

@Delete(':id')
remove(@Param('id') id: string): Promise<void> {
  return this.itemsService.remove(+id);
}
``` 
6. **Configure a Rota** :
Configure a rota no arquivo `items.module.ts`:

```typescript
// src/items/items.module.ts

import { Module } from '@nestjs/common';
import { TypeOrmModule } from '@nestjs/typeorm';
import { Item } from './items.entity';
import { ItemsController } from './items.controller';
import { ItemsService } from './items.service';

@Module({
  imports: [TypeOrmModule.forFeature([Item])],
  controllers: [ItemsController],
  providers: [ItemsService],
})
export class ItemsModule {}
``` 
7. **Execute o Servidor** :
Inicie o servidor Nest.js:

```bash
npm run start:dev
```

**Passo 2: Configuração do Front-end com Next.js** 

Agora, vamos criar o front-end com Next.js para se comunicar com o back-end. Certifique-se de ter o Node.js e o npm instalados. 
1. **Crie um Novo Projeto Next.js** :
Abra um novo terminal e execute os seguintes comandos:

```bash
npx create-next-app frontend-project
cd frontend-project
``` 
2. **Instale as Dependências** :
Instale as dependências necessárias, como Axios para fazer solicitações HTTP ao servidor:

```bash
npm install axios
``` 
3. **Configure a Conexão com o Back-end** :
Defina a URL do servidor Nest.js no arquivo de configuração, por exemplo, em `frontend-project/utils/api.js`:

```javascript
// frontend-project/utils/api.js

import axios from 'axios';

const api = axios.create({
  baseURL: 'http://localhost:3000', // Ajuste conforme a porta do servidor Nest.js
});

export default api;
``` 
4. **Crie Páginas e Componentes** :
Crie páginas e componentes React para construir a interface do usuário. 
5. **Recupere Dados do Back-end** :
Use o Axios para fazer solicitações ao servidor e exibir os dados na interface. 
6. **Configure o Roteamento** :
Configure o roteamento no lado do cliente usando o Next.js, criando páginas e arquivos de rota no diretório `pages`. 
7. **Estilize com CSS** :
Estilize a interface do usuário com CSS ou bibliotecas de estilo, como Styled-components ou SCSS. 
8. **Inicie o Aplicativo Next.js** :
Inicie o aplicativo Next.js:

```bash
npm run dev
```

**Passo 3: Recursos Avançados e Implantação** 

Para recursos avançados, como autenticação, controle de acesso, gerenciamento de estado, SEO, segurança, testes e hospedagem, você precisará expandir seu projeto e personalizá-lo de acordo com suas necessidades específicas. Além disso, a implantação em produção pode ser realizada em plataformas como Vercel, Netlify, Heroku ou AWS, seguindo as práticas recomendadas.

Este guia fornece os passos iniciais para criar uma aplicação full-stack com Nest.js e Next.js, mas aprofundar-se em cada área é essencial para desenvolver um aplicativo mais robusto e profissional.