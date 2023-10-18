---
description: Construindo uma REST API
public: true
layout: ../../layouts/BlogPost.astro
title: Hasura
createdAt: 1663635760350
updatedAt: 1663635788618
tags:
  - Hasura
heroImage: /posts/hasura_deno.webp
slug: Hasura
---


# Construindo uma REST API com Hasura, Deno e GraphQL

Neste blog completo, você aprenderá a criar uma REST API usando três tecnologias emocionantes: Hasura, Deno e GraphQL. Vamos explorar cada um dos tópicos a seguir:
## Tópico 1: Introdução ao Hasura
### O que é o Hasura?

Hasura é uma plataforma de código aberto que simplifica o desenvolvimento de APIs GraphQL e REST. Ela se conecta diretamente a um banco de dados PostgreSQL, fornecendo recursos de autorização, autenticação e lógica de negócios personalizada.

```markdown
Hasura é uma escolha popular para desenvolvedores que desejam acelerar o processo de criação de serviços REST e GraphQL.
```


## Tópico 2: Configurando o Ambiente
### Instalando o Hasura e o Deno

Antes de começarmos, você precisa configurar seu ambiente de desenvolvimento. Vamos começar instalando o Hasura e o Deno.

```bash
# Instalando o Hasura
docker-compose up -d

# Instalando o Deno
curl -fsSL https://deno.land/x/install/install.sh | sh
```


## Tópico 3: Criando um Banco de Dados
### PostgreSQL como Banco de Dados

Vamos usar o PostgreSQL como nosso banco de dados para esta REST API.

```markdown
O PostgreSQL é uma escolha sólida para um banco de dados relacional que oferece confiabilidade e suporte a recursos avançados.
```



```bash
# Criando um banco de dados no PostgreSQL
createdb mydb -U user
```


## Tópico 4: Configurando o Hasura
### Conectando o Hasura ao Banco de Dados

Para configurar o Hasura, você precisa fornecer as informações de conexão com o PostgreSQL.

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



Certifique-se de substituir `user`, `password`, `mydb` e `myadminsecret` pelas informações apropriadas.
## Tópico 5: Definindo Tabelas e Relações
### Configurando Tabelas no Hasura

O Hasura oferece uma interface gráfica para definir tabelas no banco de dados e estabelecer relações entre elas.

![Hasura Table Configuration](https://chat.openai.com/c/image-hasura-table-configuration.png) 

## Tópico 6: Configurando Permissões
### Gerenciando Permissões

Com o Hasura, você pode definir permissões detalhadas para controlar quem pode acessar e modificar os dados.

```markdown
A definição de permissões é essencial para garantir a segurança e a integridade dos dados em sua API.
```


## Tópico 7: Gerando um Schema GraphQL
### Geração Automática de Schema

O Hasura gera automaticamente um schema GraphQL com base nas configurações do banco de dados.

```markdown
A geração automática de um schema GraphQL economiza tempo e esforço no desenvolvimento da API.
```


## Tópico 8: Testando a API GraphQL
### Utilizando o Playground do Hasura

O Playground do Hasura permite testar consultas e mutações na API GraphQL.

![Hasura Playground](https://chat.openai.com/c/image-hasura-playground.png) 

## Tópico 9: Expondo a API GraphQL como REST API
### Usando o Hasura para Expor como REST

O Hasura permite que você exponha sua API GraphQL como uma REST API com facilidade.

```markdown
Isso oferece flexibilidade aos desenvolvedores que preferem usar REST para interagir com a API.
```



```bash
# Expor a API GraphQL como REST
hasura metadata apply
```


## Tópico 10: Introdução ao Deno
### O que é o Deno?

Deno é uma plataforma JavaScript/TypeScript segura e moderna para construir aplicativos server-side. Ela se destaca por sua segurança, desempenho e facilidade de uso.

```markdown
O Deno oferece uma alternativa empolgante ao Node.js para criar aplicativos server-side.
```



```bash
# Instalando o Deno
curl -fsSL https://deno.land/x/install/install.sh | sh
```


## Tópico 11: Configurando o Ambiente Deno
### Configurando o Ambiente de Desenvolvimento Deno

Configure o ambiente Deno e crie um arquivo `deps.ts` para gerenciar as dependências.

```markdown
Gerenciar dependências em um arquivo separado torna a manutenção de seu aplicativo mais organizada.
```



```typescript
// deps.ts
export { Application, Router } from "https://deno.land/x/oak/mod.ts";
export { Client } from "https://deno.land/x/postgres/mod.ts";
```


## Tópico 12: Criando um Servidor Deno
### Criando um Servidor Deno Simples

Vamos criar um servidor Deno simples que ouvirá as solicitações da REST API.

```typescript
// server.ts
import { Application } from "./deps.ts";

const app = new Application();
const port = 8000;

app.use((ctx) => {
  ctx.response.body = "Hello, Deno!";
});

await app.listen({ port });
```



```bash
# Executando o servidor Deno
deno run --allow-net server.ts
```


## Tópico 13: Manipulando Rotas em Deno
### Definindo Rotas em Deno

Vamos aprender a criar rotas em Deno para lidar com diferentes solicitações HTTP.

```typescript
// routes.ts
import { Router } from "./deps.ts";

const router = new Router();

router.get("/", (ctx) => {
  ctx.response.body = "Rota GET";
});

router.post("/data", async (ctx) => {
  // Manipular solicitação POST
});

export default router;
```


## Tópico 14: Conectando-se à REST API
### Fazendo Solicitações à API Hasura

Iremos explorar como fazer solicitações à REST API que expusemos usando o Hasura.

```typescript
// connect-to-hasura.ts
import { fetch } from "https://deno.land/x/node_fetch/mod.ts";

const response = await fetch("http://localhost:8080/rest/data");
const data = await response.json();
console.log(data);
```


## Tópico 15: Criando Rotas REST
### Definindo Rotas REST em Deno

Vamos definir rotas REST para recuperar, criar, atualizar e excluir dados usando Deno.

```typescript
// rest-routes.ts
import { Router } from "./deps.ts";

const restRouter = new Router();

restRouter.get("/data", async (ctx) => {
  // Recuperar dados da API Hasura
});

restRouter.post("/data", async (ctx) => {
  // Criar um novo registro na API Hasura
});

restRouter.put("/data/:id", async (ctx) => {
  // Atualizar um registro existente na API Hasura
});

restRouter.delete("/data/:id", async (ctx) => {
  // Excluir um registro na API Hasura
});

export default restRouter;
```


## Tópico 16: Validação de Dados
### Validando Dados de Solicitação

Aprenderemos como validar os dados recebidos nas solicitações REST para garantir a integridade dos dados.

```typescript
// validation.ts
export function validateData(data) {
  // Implementar validação de dados
}
```


## Tópico 17: Autenticação e Autorização
### Estratégias de Autenticação e Autorização

Exploraremos opções para autenticação e autorização na nossa REST API.

```markdown
A autenticação e a autorização são componentes críticos de qualquer API para proteger os dados e garantir que apenas usuários autorizados acessem recursos específicos.
```


## Tópico 18: Logging e Tratamento de Erros
### Registrando Eventos e Tratando Erros

Aprenderemos a registrar eventos e lidar com erros em nosso servidor Deno.

```typescript
// logging.ts
export function logEvent(event) {
  // Registra eventos no servidor
}
```


## Tópico 19: Adicionando Lógica de Negócios
### Lógica de Negócios Personalizada

Vamos adicionar lógica de negócios personalizada à nossa REST API usando Deno.

```typescript
// business-logic.ts
export function processData(data) {
  // Implementa a lógica de negócios
}
```


## Tópico 20: Testando a REST API
### Testes Unitários e de Integração

Iremos abordar como criar testes unitários e de integração para garantir a qualidade da nossa API.

```markdown
Testes são cruciais para garantir que sua API funcione corretamente e não introduza regressões.
```



```bash
# Executando testes
deno test
```


## Tópico 21: Documentação da API
### Criando Documentação da API

Aprenderemos a criar documentação da nossa API REST para facilitar o uso por outros desenvolvedores.

```markdown
Uma documentação clara e abrangente é essencial para facilitar o uso de sua API por outros desenvolvedores.
```



```markdown
## Tópico 22: Implantação

### Implantação da API
Exploraremos opções para implantar nossa REST API e torná-la acessível para o público.

```markdown
Implantar sua API é um passo importante para disponibilizá-la para os usuários finais.
```



```bash
# Implantação com Docker
docker build -t my-api .
docker run -p 8000:8000 my-api
```


## Tópico 23: Monitoramento e Métricas
### Monitorando o Desempenho

Iremos configurar ferramentas de monitoramento e coleta de métricas para acompanhar o desempenho da API.

```markdown
O monitoramento é essencial para identificar e resolver problemas de desempenho em tempo hábil.
```


## Tópico 24: Gerenciamento de Versões
### Versionamento da API

Vamos discutir práticas recomendadas para gerenciar versões de nossa REST API.

```markdown
O versionamento é importante para garantir que as alterações na API não quebrem os aplicativos existentes dos usuários.
```


## Tópico 25: Escalabilidade
### Estratégias de Escalabilidade

Discutiremos estratégias de escalabilidade para lidar com um grande número de solicitações.

```markdown
A escalabilidade é crucial para garantir que sua API possa crescer à medida que a demanda aumenta.
```


## Tópico 26: Segurança
### Práticas Recomendadas de Segurança

Exploraremos práticas recomendadas de segurança para proteger nossa API contra ameaças.

```markdown
A segurança é uma consideração crítica ao criar uma API pública para proteger dados confidenciais e a privacidade dos usuários.
```


## Tópico 27: Manutenção e Atualizações
### Manutenção Contínua

Aprenderemos sobre como manter e atualizar nossa REST API de maneira eficaz.

```markdown
A manutenção regular é necessária para corrigir bugs, adicionar recursos e manter a API atualizada.
```


## Tópico 28: Desafios Comuns
### Lidando com Desafios

Discutiremos desafios comuns encontrados ao criar uma REST API com Hasura, Deno e GraphQL.

```markdown
A criação de uma API envolve desafios que variam desde questões técnicas até a adoção da API pelos desenvolvedores e usuários.
```


## Tópico 29: Recursos e Ferramentas
### Recursos Úteis

Apresentaremos recursos e ferramentas úteis para a criação e o gerenciamento de REST APIs.

```markdown
Existem inúmeras ferramentas, bibliotecas e recursos disponíveis para facilitar o desenvolvimento e a manutenção de APIs REST.
```


## Tópico 30: Conclusão
### Finalizando

Finalizaremos nosso blog resumindo o que aprendemos e destacando a importância de construir REST APIs com Hasura, Deno e GraphQL.

```markdown
Parabéns por completar esta jornada de criação de uma REST API com Hasura, Deno e GraphQL. Esperamos que você tenha adquirido as habilidades e o conhecimento necessários para construir APIs eficazes, seguras e de alto desempenho.
```