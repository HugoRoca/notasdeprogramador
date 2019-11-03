---
date: 2019-10-31
title: Backoff
weight: 25
---

Para crear un backoff en javascript iniciaremos con el retorno de una promesa que contiene un `setTimeout`, para poder ejecutar tenemos que anteponer el `await` para "esperar".

Esto es util cuando queremos realizar reintentos, podemos iniciar con 1/2 segundo, luego ir multiplicando para que el tiempo de espera sea más.

```js
const backoff = (delay) => new Promise(res => setTimeout(res, delay));

// ejemplo de ejecución
(async() => {
    await backoff(500); // 500 => milisegundos
    console.log("test");
})();
```