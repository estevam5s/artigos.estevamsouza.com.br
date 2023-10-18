---
description: Como trabalhar com variaveis de ambiente no NestJS?!
public: true
layout: ../../layouts/BlogPost.astro
title: NestJS
createdAt: 1663134814751
updatedAt: 1663635669481
tags:
  - Backend
heroImage: /posts/1_Yq-mdtszOQDyDG_4Z32qhQ.webp
slug: Backend
---


# Guia: Como Trabalhar com Variáveis de Ambiente no NestJS

Neste guia, vamos explorar como trabalhar com variáveis de ambiente no NestJS, um framework Node.js para construir aplicativos escaláveis e modulares. O uso de variáveis de ambiente é essencial para configurar e gerenciar as configurações de seu aplicativo de forma segura e flexível.
## Tópico 1: Variáveis de Ambiente no NestJS

Variáveis de ambiente são valores que podem ser configurados fora de seu aplicativo e são usados para armazenar configurações sensíveis ou valores que podem variar entre ambientes (desenvolvimento, teste, produção).
## Tópico 2: Configurando Variáveis de Ambiente
### 2.1. Uso do pacote `dotenv`

O pacote `dotenv` é uma biblioteca comum para carregar variáveis de ambiente de um arquivo `.env`. Para começar, instale o `dotenv` em seu projeto:

```bash
npm install dotenv
```


### 2.2. Criando um arquivo `.env`

Crie um arquivo `.env` na raiz de seu projeto e adicione variáveis como chave-valor. Por exemplo:

```makefile
DATABASE_URL=mongodb://localhost/meuapp
PORT=3000
SECRET_KEY=minhachave123
```


### 2.3. Carregando Variáveis de Ambiente

No ponto de entrada de seu aplicativo NestJS (geralmente `main.ts`), carregue as variáveis de ambiente usando `dotenv`:

```javascript
import { NestFactory } from '@nestjs/core';
import { AppModule } from './app.module';
import * as dotenv from 'dotenv';

dotenv.config(); // Carregar variáveis de ambiente do arquivo .env

async function bootstrap() {
  const app = await NestFactory.create(AppModule);
  await app.listen(process.env.PORT || 3000); // Usar PORT definida no arquivo .env ou 3000 como valor padrão
}
bootstrap();
```


## Tópico 3: Usando Variáveis de Ambiente

Agora que as variáveis de ambiente estão configuradas, você pode usá-las em seu aplicativo NestJS.

```javascript
import { Injectable } from '@nestjs/common';

@Injectable()
export class MinhaService {
  // Acesse uma variável de ambiente
  private databaseUrl = process.env.DATABASE_URL;

  // Use a variável em sua lógica
  async conectarAoBancoDeDados() {
    // Use this.databaseUrl para se conectar ao banco de dados
  }
}
```


## Tópico 4: Variáveis de Ambiente em Diferentes Ambientes

Você pode ter arquivos `.env` separados para diferentes ambientes, como `.env.dev` para desenvolvimento e `.env.prod` para produção. Carregue o arquivo apropriado com base no ambiente.

```javascript
if (process.env.NODE_ENV === 'development') {
  dotenv.config({ path: '.env.dev' });
} else {
  dotenv.config({ path: '.env.prod' });
}
```


## Tópico 5: Segurança

Mantenha suas variáveis de ambiente seguras. Evite armazenar informações sensíveis diretamente no arquivo `.env` e use soluções de segurança adequadas, como segredos e tokens.
## Tópico 6: Conclusão

O uso de variáveis de ambiente no NestJS é fundamental para configurar seu aplicativo de maneira flexível e segura. Isso permite que você gerencie facilmente as configurações do aplicativo em diferentes ambientes e mantenha informações sensíveis protegidas. Certifique-se de seguir as melhores práticas de segurança ao lidar com variáveis de ambiente em seu projeto NestJS.

