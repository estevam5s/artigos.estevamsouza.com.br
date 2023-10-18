---
description: Como usar debug em NodeJS com Docker
public: true
layout: ../../layouts/BlogPost.astro
title: NodeJS
createdAt: 1663138425977
updatedAt: 1663138445359
tags:
  - Backend
heroImage: /posts/1_nZg-TpYNtTLu3bFhpnho0g.webp
slug: Backend
---


# Como Usar Debug em Node.js com Docker

Neste guia, vamos explorar como configurar e usar a depuração (debug) em aplicativos Node.js executados em contêineres Docker. A depuração é uma ferramenta essencial para identificar e solucionar problemas em seu aplicativo Node.js, e quando combinada com contêineres Docker, ela oferece flexibilidade e eficiência no desenvolvimento e depuração.
## Tópico 1: Configurando a Depuração no Aplicativo Node.js

Para habilitar a depuração em seu aplicativo Node.js, siga estas etapas:
### 1.1. Adicione um Ponto de Parada (Breakpoint)

No código de seu aplicativo, adicione um ponto de parada usando a palavra-chave `debugger`. Por exemplo:

```javascript
// Seu código Node.js
const valor = 42;
debugger; // Adicione um ponto de parada aqui
console.log('Valor:', valor);
```


### 1.2. Configurando o Executável Node.js

Para permitir a depuração, seu aplicativo Node.js deve ser executado em modo de depuração. Isso pode ser alcançado configurando o executável `node` para usar a opção `--inspect` ou `--inspect-brk`. Por exemplo:

```bash
node --inspect=0.0.0.0:9229 seu_app.js
```

 
- `--inspect`: Permite a depuração, e o aplicativo inicia imediatamente. 
- `--inspect-brk`: Permite a depuração, e o aplicativo inicia e aguarda uma conexão de depuração.
## Tópico 2: Configurando o Contêiner Docker para Depuração

Agora que seu aplicativo Node.js está configurado para depuração, você deve garantir que seu contêiner Docker seja configurado para permitir a conexão de depuração.
### 2.1. Expondo a Porta de Depuração

No Dockerfile de seu aplicativo, você deve expor a porta de depuração para que seja acessível de fora do contêiner. Adicione o seguinte comando ao Dockerfile:

```Dockerfile
EXPOSE 9229
```



Isso permitirá que a porta de depuração seja acessível no host.
### 2.2. Criando o Contêiner

Certifique-se de que o Dockerfile de seu aplicativo inclui a configuração necessária para a depuração e, em seguida, crie o contêiner:

```bash
docker build -t seu_app .
docker run -p 9229:9229 -d seu_app
```

 
- `-p 9229:9229`: Mapeia a porta de depuração do contêiner para a mesma porta no host.
## Tópico 3: Depurando com VSCode

Para depurar seu aplicativo Node.js em um contêiner Docker com o Visual Studio Code (VSCode), siga estas etapas:
### 3.1. Instalando Extensões

Certifique-se de ter as seguintes extensões do VSCode instaladas: 
- [Docker](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-docker) 
- [Node.js](https://marketplace.visualstudio.com/items?itemName=ms-vscode.node-debug2)
### 3.2. Criando uma Configuração de Depuração

No VSCode, abra a guia de depuração (F5) e clique em "create a launch.json file". Selecione "Node.js" como ambiente de execução e edite a configuração:

```json
{
  "type": "node",
  "request": "attach",
  "name": "Docker: Attach",
  "port": 9229,
  "address": "localhost",
  "localRoot": "${workspaceFolder}",
  "remoteRoot": "/usr/src/app"  // Caminho no contêiner onde o código está localizado
}
```


### 3.3. Iniciando a Depuração
- Execute seu aplicativo Node.js com o Docker.
- No VSCode, selecione a configuração de depuração "Docker: Attach".
- Clique em "Start Debugging" (F5).

Agora você pode depurar seu aplicativo Node.js em um contêiner Docker usando o VSCode. O VSCode se conectará ao processo de depuração em execução no contêiner.
## Tópico 4: Conclusão

A combinação de Node.js e Docker oferece uma maneira eficaz de desenvolver e depurar aplicativos Node.js. Usar a depuração com Docker permite que você isole ambientes, simule cenários de produção e identifique problemas com facilidade. Certifique-se de seguir as melhores práticas de segurança e manter os contêineres atualizados para um desenvolvimento mais seguro e eficiente.
