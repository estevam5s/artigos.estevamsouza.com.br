---
description: Orientação a Objetos com TS
public: true
layout: ../../layouts/BlogPost.astro
title: TypeScript
createdAt: 1663138688416
updatedAt: 1663138745318
tags:
  - Backend
heroImage: /posts/TypeScript_Vantagens_mitos_e_aplicacoes.png
slug: Backend
---


# Programação Orientada a Objetos com TypeScript: Do Básico ao Avançado

A Programação Orientada a Objetos (POO) é um paradigma de programação amplamente utilizado em que o software é modelado como um conjunto de objetos interagindo uns com os outros. Neste guia abrangente, exploraremos a POO com TypeScript, começando com conceitos básicos e avançando para exemplos práticos de código.
## Tópico 1: Introdução à POO
### 1.1 O que é a Programação Orientada a Objetos?

Aprenda os conceitos fundamentais da POO, como objetos, classes, herança e encapsulamento.
### 1.2 Por que a POO é Importante?

Entenda por que a POO é amplamente utilizada e quais são seus benefícios.
## Tópico 2: Classes e Objetos em TypeScript
### 2.1 Definindo Classes em TypeScript

Crie classes em TypeScript para modelar objetos do mundo real.
### 2.2 Instanciando Objetos

Aprenda a criar instâncias de objetos a partir de classes.
### 2.3 Propriedades e Métodos de Classe

Defina propriedades e métodos em suas classes TypeScript.

```typescript
class Pessoa {
  nome: string;
  constructor(nome: string) {
    this.nome = nome;
  }
  cumprimentar() {
    console.log(`Olá, meu nome é ${this.nome}.`);
  }
}

const pessoa1 = new Pessoa('Alice');
pessoa1.cumprimentar();
```


## Tópico 3: Encapsulamento
### 3.1 Modificadores de Acesso

Aprenda sobre os modificadores de acesso, como `public`, `private` e `protected`, para controlar o acesso aos membros da classe.
### 3.2 Getters e Setters

Implemente getters e setters para controlar o acesso e a modificação de propriedades privadas.
## Tópico 4: Herança
### 4.1 Herança de Classes

Crie hierarquias de classes para compartilhar funcionalidades entre objetos relacionados.
### 4.2 Classe Base e Classe Derivada

Explore a relação entre a classe base e a classe derivada.
## Tópico 5: Polimorfismo
### 5.1 Polimorfismo de Métodos

Aprenda a usar o polimorfismo para permitir que objetos de classes diferentes respondam de maneira única a métodos comuns.

```typescript
class Animal {
  fazerSom() {
    console.log('Animal faz som.');
  }
}

class Cachorro extends Animal {
  fazerSom() {
    console.log('Cachorro late.');
  }
}

class Gato extends Animal {
  fazerSom() {
    console.log('Gato mia.');
  }
}
```


## Tópico 6: Interfaces e Abstração
### 6.1 Interfaces em TypeScript

Defina interfaces para descrever contratos de classes e objetos.
### 6.2 Classes Abstratas

Crie classes abstratas para modelar entidades que não podem ser instanciadas diretamente.
## Tópico 7: Sobrecarga de Métodos
### 7.1 Sobrecarga de Métodos

Implemente a sobrecarga de métodos para criar métodos com comportamentos diferentes com base nos argumentos fornecidos.

```typescript
class Calculadora {
  calcular(x: number, y: number): number;
  calcular(x: string, y: string): string;
  calcular(x: any, y: any): any {
    if (typeof x === 'number' && typeof y === 'number') {
      return x + y;
    } else if (typeof x === 'string' && typeof y === 'string') {
      return x + y;
    }
  }
}
```


## Tópico 8: Classes Genéricas
### 8.1 Classes Genéricas

Crie classes genéricas para reutilizar lógica com tipos flexíveis.

```typescript
class Colecao<T> {
  itens: T[] = [];
  adicionar(item: T) {
    this.itens.push(item);
  }
}

const numeros = new Colecao<number>();
numeros.adicionar(1);
numeros.adicionar(2);
```


## Tópico 9: Conclusão
### 9.1 Dominando a POO com TypeScript

A POO é uma poderosa maneira de modelar e organizar seu código. Continue praticando e explorando recursos adicionais do TypeScript para aprimorar suas habilidades.