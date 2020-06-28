# Novidades do ES2020

[Link de Referência](https://www.freecodecamp.org/news/javascript-new-features-es2020/)

## 1 - BigInt

Atualmente, o número máximo que se pode armazenar em um inteiro no JavaScript é ```pow(2, 53) - 1```

Para visualizar esse número basta printar essa variável no console do navegador

```js
Number.MAX_SAFE_INTEGER // 9007199254740991
```

Para criar um BigInt, basta adicionar um ```n``` no final do número

```js
9007199254740991n
```

---

## 2 - Dynamic Import

O Dynamic Import permite que você faça a importação dinâmica de modulos JavaScript nativamente, sem a necessidade do Babel ou Webpack. Ela é muito útil quando se é necessário fazer code-splitting, ou carregar um código com base em uma condição

```js
if (myCondition) {
  const module = await import('./dynamicModule.js')
  module.addNumbers(3, 4, 5)
}
```

---

## 3 - Nullish Coalescing

O Javascript hoje considera muitos valores como ```falsey```, dentre eles ```0```, ```undefined```, ```null```, ```false```, ```NaN```.

Com o Nullish Coalescing ele só trata a variável como ```falsey``` se ela for ```undefined``` ou ```null```.

```js

null || 'hello world' // "hello world"
null ?? 'hello world' // "hello world"

--

false || 'hello world' // "hello world"
false ?? 'hello world' // false

```

---

## 4 - Optional Chaining

O Optional Chaining permite você acessar objetos profundamente sem ficar fazendo verificações se os pais existem. Por exemplo, considerando esse objeto:

```js

const pessoa = {
  nome: 'João',
  idade: 19,
  endereco: {
    cidade: 'Belo Horizonte',
    estado: 'Minas Gerais'
  }
}

```

Para você poder pegar a cidade antes teria que verificar se o parâmetro ```endereco``` existiria. Caso ```endereco``` fosse null e não fosse feita a verificação, ocasionaria em um erro. Exemplo:

```js
const cidade = pessoa && pessoa.endereco && pessoa.endereco.cidade
```

Com o Optional Chaining eu posso fazer simplesmente dessa forma:

```js
const cidade = pessoa?.endereco?.cidade
```

---

## 5 - Promise.allSettled

O método ```Promise.allSettled``` aceita um array de Promises e apenas é resolvida após todas as Promises dentro dela terminarem.

```js
const myPromiseArray = [
  Promise.resolve(100),
  Promise.reject(null),
  Promise.reject(new Error('Oh No'))
]

Promise.allSettled(myPromiseArray).then(results => {
  console.log('All Promises Settled', results)
})
```

---

## 6 - String#matchAll

O método ```matchAll``` foi adicionado ao tipo ```String``` com o objetivo de retornar **todos** os valores coincidentes com base em uma expressão regular. Por exemplo, considerando a seguinte expressão regular:

```js
const regExp = /[a-c]/g
const myString = 'abc'
const iterator = myString.matchAll(regExp)
Array.from(iterator, result => console.log(result))

/*
  ["a", index: 0, input: "abc", groups: undefined]
  ["b", index: 1, input: "abc", groups: undefined]
  ["c", index: 2, input: "abc", groups: undefined]
*/
```

---

## 7 - globalThis

Ao escrever um código JavaScript cross-platform, que rodaria por exemplo no Node, no browser e dentro dos web-workers, você teria que verificar qual seria o objeto global, considerando que no browser é a ```window```, no node é o ```global``` e nos web workers é o ```self```.

O ```globalThis``` foi criado para referenciar todos esses objetos globais, independente da plataforma.

```js
globalThis.setTimeout === window.setTimeout // True
```

---

## 8 - Module Namespace Exports

Atualmente no JavaScript eu posso fazer a exportação de vários módulos dentro de um arquivo, como por exemplo:

```js
// utils.js
function module1 () {...}
function module2 () {...}
function module3 () {...}

export { module1, module2, module3 }
```

ou

```js
// utils.js
export function module1 () {...}
export function module2 () {...}
export function module3 () {...}
```

E se eu quisesse importar tudo de uma vez, bastaria:

```js
import * as utils from 'utils.js'
utils.module1()
utils.module2()
utils.module3()
```

Com o ES2020, eu posso utilizar uma nova sintaxe de exportação

```js
// utils.js
function module1 () {...}
function module2 () {...}
function module3 () {...}

export * as utils from 'utils.js'
```
