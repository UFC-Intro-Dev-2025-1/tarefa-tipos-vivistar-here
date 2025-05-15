# Variáveis

<!-- toc -->

-   [Estrutura de dados](#estrutura-de-dados)
    -   [Tipagem dinâmica e fraca em JavaScript](#tipagem-dinâmica-e-fraca-em-javascript)
    -   [Tipagem forte em TypeScript](#tipagem-forte-em-typescript)
-   [Tipos de dados em TS](#tipos-de-dados-em-ts)
    -   [Tipos primitivos mais comuns](#tipos-primitivos-mais-comuns)
        -   [`number`](#number)
        -   [`string`](#string)
        -   [`boolean`](#boolean)
    -   [Tipos primitivos para representar o vazio](#tipos-primitivos-para-representar-o-vazio)
        -   [`null`](#null)
        -   [`undefined`](#undefined)
    -   [Tipos primitivos menos usados](#tipos-primitivos-menos-usados)
        -   [`bigint`](#bigint)
        -   [`symbol`](#symbol)
    -   [O famoso tipo `any`](#o-famoso-tipo-any)
    -   [Tipos de dados combinados](#tipos-de-dados-combinados)
        -   [`array`](#array)
        -   [`tupla`](#tupla)
        -   [`object`](#object)
        -   [`enum`](#enum)
    -   [União de Tipos](#união-de-tipos)
    -   [Conversão de tipos](#conversão-de-tipos)
-   [Referências](#referências)

<!-- toc -->

## Estrutura de dados

Todas as linguagens de programação têm estruturas de dados embutidas, mas geralmente diferem de uma linguagem para outra. Aqui vamos listar as estruturas de dados internas disponíveis em TypeScript e JavaScript.

### Tipagem dinâmica e fraca em JavaScript

JavaScript é uma linguagem dinâmica com tipos dinâmicos. As variáveis em JavaScript não estão diretamente associadas a nenhum tipo de valor específico, e qualquer variável pode receber (e reatribuir) valores de todos os tipos:

```js
let minhaVariavel = 42; // minhaVariavel agora é um número
minhaVariavel = 'oi'; // minhaVariavel agora é uma string
minhaVariavel = true; // minhaVariavel agora é um booleano
```

JavaScript também é uma linguagem de tipagem fraca, o que significa que permite a conversão implícita de tipo quando uma operação envolve tipos incompatíveis, em vez de gerar erros de tipo.

```js
const minhaVariavel = 42; //minhaVariavel é um número
const result = minhaVariavel + '1'; // JavaScript coage minhaVariavel para uma string, então ela pode ser concatenada com o outro operando
console.log(resultado); // 421
```

Coerções implícitas (quando ele tenta resolver essa diferença de tipos) são muito convenientes, mas podem ser uma arma em potencial se os desenvolvedores não pretendem fazer a conversão ou pretendem converter na outra direção (por exemplo, string para número em vez de número para string). No exemplo acima, alguém poderia esperar `43` em vez de `421`.

### Tipagem forte em TypeScript

Em TypeScript, você pode usar tipos para definir o formato esperado das variáveis. Isso ajuda a melhorar a verificação de tipos durante a compilação e fornece informações úteis sobre o que é esperado de uma variável em seu código. Aqui estão algumas maneiras de usar tipos em variáveis do TypeScript:

1. **Tipo Explícito:**
   Você pode declarar o tipo de uma variável explicitamente ao mesmo tempo em que a declara. Por exemplo:

```typescript
let idade: number = 25;
let nome: string = 'João';
```

2. **Inferência de Tipo:**
   O TypeScript é capaz de inferir o tipo da variável com base no valor que você atribui a ela. Isso é chamado de inferência de tipo. Por exemplo:

```typescript
let idade = 25; // TypeScript inferirá que "idade" é do tipo number
let nome = 'João'; // TypeScript inferirá que "nome" é do tipo string
```

Essas são apenas algumas das maneiras pelas quais você pode usar tipos em variáveis no TypeScript. A vantagem de usar tipos é que eles ajudam a capturar erros de tipo em tempo de compilação, tornando seu código mais robusto e legível.

## Tipos de dados em TS

O TypeScript fornece vários tipos de dados que você pode usar para declarar variáveis e especificar o tipo de valores que essas variáveis podem conter. Aqui estão alguns dos principais tipos de dados em TypeScript:

### Tipos primitivos mais comuns

#### `number`

Representa números como `42`, tanto inteiros quanto números de ponto flutuante. Em JavaScript, e consequentemente em TypeScript, não temos `int` e `float`, apenas `number`.

```typescript
// Como só usamos o number, para transformar um `float` em `int`, usamos o Math.floor
const numero: number = 7.83;
const parteInteira: number = Math.floor(numero);
console.log(parteInteira); // 7
```

> `NaN` ("Not a Number") é encontrado quando o resultado de uma operação aritmética não pode ser expresso como um número, apesar de ele ser do tipo `number`.

```ts
const minhaVariavel = 0 / 0;
console.log(minhaVariavel); /NaN
```

#### `string`

Representa sequências de caracteres, como `"Olá, mundo!"`. Você pode usar aspas simples (`'`), aspas duplas (`"`) ou crase (`` ` ``) para definir strings. Padronize o uso das aspas. Use a crase para fazer interpolação.

Não existe `char` em JS ou TS. O tipo principal para representar caracteres individuais é o tipo `string`, que representa sequências de caracteres.

```typescript
// Para acessar o primeiro caractere de uma string,
// você pode usar a notação de colchetes com o índice dentro :
// OBS: o índice começa em 0 😬
const palavra: string = 'Hello';
const primeiroCaractere: string = palavra[0]; // "H"
```

### `boolean`

Representa valores booleanos, que podem ser `true` ou `false`. Esse tipo é útil para controle de fluxo e condições.

### Tipos primitivos para representar o vazio

#### `null`

Representa a ausência intencional de valor. É um tipo primitivo que indica que uma variável não tem valor: o vazio.

```typescript
let valorNulo: null = null; // valorNulo é do tipo null
```

#### `undefined`

Representa uma variável que foi declarada, mas não inicializada. É o valor padrão de variáveis não atribuídas.

```typescript
let valorDesconhecido;
console.log(valorDesconhecido); // undefined
```

### Tipos primitivos menos usados

#### `bigint`

Representa números inteiros grandes que podem exceder o limite do tipo `number`. Você pode usar o sufixo `n` para indicar um valor `bigint`.

```typescript
const numeroGrande: bigint = 1234567890123456789012345678901234567890n;
console.log(numeroGrande); // 1234567890123456789012345678901234567890n
```

#### `symbol`

Representa um valor único e imutável, usado como identificador de propriedades de objetos.

```typescript
const simbolo1 = Symbol('descricao');
const simbolo2 = Symbol('descricao');
console.log(simbolo1 === simbolo2); // false, cada símbolo é único
```

### O famoso tipo `any`

O TypeScript tem um tipo especial, `any`, que você pode usar sempre que não quiser erros de verificação de tipo. Basicamente é voltar para o JavaScript puro, onde tudo é `any`. Isso pode ser útil em situações em que você não tem certeza do tipo de um valor ou quando está lidando com bibliotecas de terceiros que não têm definições de tipo. **Use com cautela!**

```typescript
let variavel: any;

variavel = 10;
console.log(variavel);
variavel = 'oie';
console.log(variavel);
variavel = true;
console.log(variavel);
```

> **Nota**: Quando você não especifica um tipo e o TypeScript não consegue inferi-lo a partir do contexto, o compilador normalmente usará `any`.

### Tipos de dados combinados

#### `array`

Em TypeScript, você pode usar colchetes (`[]`) para declarar um array de um tipo específico. Por exemplo, `number[]` representa um array de números.

```typescript
// TypeScript
let numeros: number[] = [1, 2, 3, 4, 5];
let nomes: string[] = ['Alice', 'Bob', 'Charlie'];
```

```js
// JavaScript
let numeros[] = [1, 2, 3, 4, 5];
let nomes[] = ['Alice', 'Bob', 'Charlie'];
let tudoMisturado[] = [1, 'Alice', true, null];
```

#### `tupla`

Uma tupla é um array com um número fixo de elementos, onde cada elemento pode ter um tipo diferente. Você pode declarar uma tupla usando colchetes (`[]`) e especificando os tipos dos elementos.

```typescript
let coordenada: [number, number] = [-4.97811, -39.063631];
console.log('latitude: ' + coordenada[0]);
console.log('longitude: ' + coordenada[1]);
```

#### `object`

O tipo `object` é um tipo genérico. Tudo o que não é primitivo (como `number`, `string`, `boolean`, etc.) é um objeto. Inclusive Array e Funções.

```typescript
et pessoa = {
    nome: 'Alice',
    idade: 30,
};
console.log(pessoa.nome); // Alice
console.log(pessoa['nome']) // Alice
console.log(pessoa.idade); // 30
console.log(pessoa['idade']) // 30
```

Em TypeScript, é possível criar tipos personalizados de objetos usando interfaces.

```typescript
interface Pessoa {
    nome: string;
    idade: number;
}

let pessoa: Pessoa = {
    nome: 'Maria',
    idade: 30,
};
```

#### `enum`

O tipo `enum` é uma maneira de definir um conjunto nomeado de valores. Ele pode ser usado para representar um conjunto fixo de opções, como dias da semana, meses do ano, etc.

```typescript
enum DiaDaSemana {
    Domingo,
    Segunda,
    Terça,
    Quarta,
    Quinta,
    Sexta,
    Sábado,
}
let dia: DiaDaSemana = DiaDaSemana.Segunda;
console.log(dia); // 1 (o valor associado a Segunda)
```

## União de Tipos

A união de tipos em TypeScript permite que uma variável tenha mais de um tipo possível, usando o operador `|`. Exemplo:

```typescript
let valor: number | string;
valor = 42; // válido
valor = 'foo'; // válido
```

Só é possível acessar propriedades ou métodos comuns a todos os tipos da união. Para acessar algo específico, faça uma verificação de tipo:

```typescript
function imprimirTamanho(texto: number | string) {
    if (typeof texto === 'string') {
        console.log(texto.length);
    }
}
```

Você pode permitir que uma variável seja de um tipo ou `null`:

```typescript
let valor: number | null;
valor = 42;
valor = null;
```

## Conversão de tipos

Em TypeScript, você pode realizar conversões entre tipos usando várias abordagens, dependendo da situação. Aqui estão algumas das maneiras mais comuns de realizar conversões de tipos:

**Construtores de Tipo:**
Muitos tipos primitivos, como `Number`, `String`, `Boolean`, `Array`, etc., também têm funções construtoras que podem ser usadas para realizar conversões explícitas.

```typescript
let valor: string = '123';
let numero: number = Number(valor); // Conversão para número
let texto: string = String(numero); // Conversão para string
```

**Operações Aritméticas e Lógicas:**

```typescript
let numero: number = +'5';
let texto = '' + 5;
```

## Referências

[qxcodefup/arcade](https://github.com/qxcodefup/arcade)  
[Estrutura de dados (mdn web docs)](https://developer.mozilla.org/pt-BR/docs/Web/JavaScript/Guide/Data_structures)  
[Everyday Types (TypeScript Handbook)](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html)
