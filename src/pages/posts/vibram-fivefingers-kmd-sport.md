---
description: Projeto Nest.js com Docker na Digital Ocean
public: true
layout: ../../layouts/BlogPost.astro
title: Nestjs
createdAt: 1663138582918
updatedAt: 1663138612308
tags:
  - Backend
heroImage: /posts/5238364_828a.jpg
slug: Backend
---


# Criando e Implantando um Projeto Nest.js com Docker na Digital Ocean
## Tópico 1: Configuração Inicial
### 1.1 Criação de um Projeto Nest.js

Comece criando um projeto Nest.js usando o CLI:

```bash
npm install -g @nestjs/cli
nest new meu-projeto-nestjs
```


### 1.2 Dockerização do Projeto

Crie um arquivo `Dockerfile` na raiz do seu projeto Nest.js para definir a configuração do contêiner Docker:

```Dockerfile
# Use a imagem oficial do Node.js como base
FROM node:14

# Diretório de trabalho dentro do contêiner
WORKDIR /app

# Copie o arquivo package.json e o arquivo package-lock.json
COPY package*.json ./

# Instale as dependências
RUN npm install

# Copie o restante dos arquivos do projeto
COPY . .

# Porta que a aplicação irá ouvir
EXPOSE 3000

# Comando para iniciar a aplicação
CMD ["npm", "start"]
```


## Tópico 2: Dockerização e Teste Local
### 2.1 Construção da Imagem Docker

Construa a imagem Docker do seu projeto executando o seguinte comando no diretório do projeto:

```bash
docker build -t meu-projeto-nestjs .
```


### 2.2 Execução Local do Contêiner

Execute o contêiner Docker localmente:

```bash
docker run -p 3000:3000 meu-projeto-nestjs
```



Acesse `http://localhost:3000` para testar a aplicação Nest.js em execução no contêiner.
## Tópico 3: Configuração na Digital Ocean
### 3.1 Criação de uma Conta Digital Ocean

Se você ainda não tiver uma conta Digital Ocean, crie uma em [https://www.digitalocean.com/](https://www.digitalocean.com/) .
### 3.2 Criação de um Droplet
- No painel Digital Ocean, crie um Droplet (servidor virtual) com a distribuição Linux de sua escolha.
- Copie o endereço IP do Droplet para uso posterior.
## Tópico 4: Implantação na Digital Ocean
### 4.1 Conexão SSH

Conecte-se ao seu Droplet via SSH usando o endereço IP:

```bash
ssh root@seu-endereco-ip
```


### 4.2 Instalação do Docker no Droplet

No Droplet, instale o Docker:

```bash
curl -fsSL https://get.docker.com -o get-docker.sh
sh get-docker.sh
```


### 4.3 Implantação da Imagem Docker

Transfira a imagem Docker do seu projeto para o Droplet:

```bash
docker save -o meu-projeto-nestjs.tar meu-projeto-nestjs
```



No Droplet, carregue a imagem:

```bash
docker load -i meu-projeto-nestjs.tar
```


### 4.4 Execução da Aplicação no Droplet

Execute a aplicação no Droplet:

```bash
docker run -d -p 80:3000 meu-projeto-nestjs
```



A aplicação Nest.js agora deve estar acessível em `http://seu-endereco-ip`.
## Tópico 5: Configuração do Proxy Reverso
### 5.1 Configuração do Nginx

Instale o Nginx no seu Droplet e configure-o como um proxy reverso para encaminhar as solicitações para a aplicação Nest.js:

```bash
apt update
apt install nginx
```


### 5.2 Criação de um Bloco de Servidor

Crie um arquivo de bloco de servidor Nginx para sua aplicação:

```bash
nano /etc/nginx/sites-available/meu-projeto-nestjs
```



Cole o seguinte conteúdo e ajuste os valores conforme necessário:

```nginx
server {
    listen 80;
    server_name seu-dominio.com;

    location / {
        proxy_pass http://seu-endereco-ip:3000;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection 'upgrade';
        proxy_set_header Host $host;
        proxy_cache_bypass $http_upgrade;
    }
}
```


### 5.3 Ativação do Bloco de Servidor

Ative o bloco de servidor:

```bash
ln -s /etc/nginx/sites-available/meu-projeto-nestjs /etc/nginx/sites-enabled
```


### 5.4 Reinício do Nginx

Reinicie o Nginx:

```bash
systemctl restart nginx
```



Sua aplicação Nest.js agora deve ser acessível em seu domínio.

Lembre-se de ajustar as configurações de segurança, firewall e monitoramento do seu servidor Digital Ocean conforme necessário.