---
date: 2019-10-30
title: Lógica de reintentos
weight: 25
---

Las promesas son una abstracción invaluable en torno a resultados 'eventuales' dentro de operaciones asincrónicas. Recientemente tuve la necesidad de poder volver a intentar una acción basada en Promesa en caso de falla. Resultó ser muy fácil implementar tal proceso usando construcciones recursivas simples.

Inicialmente solo requería la capacidad de volver a intentar la cantidad deseada de veces, antes de fallar eventualmente si aún no tenía éxito.

El siguiente código lo que realiza es que si una "petición http" falla, entra al catch por defecto, luego valida los `retries`, en caso que es este sea cero retornará el error en si.

```js
const retry = (retries, fn) => fn().catch(err => retries > 1 ? retry(retries - 1, fn) : Promise.reject(err));
```

Sin embargo, lo que eventualmente necesité fue la capacidad de 'retroceder' y proporcionar un período de gracia creciente entre los intentos de operación. Nuevamente, fue muy fácil describir esto dentro de una Promesa como se muestra a continuación.

```js
const pause = (delay) => new Promise(res => setTimeout(res, delay));

const backoff = (retries, fn, delay = 500) =>
  fn().catch(err => retries > 1
    ? pause(delay).then(() => backoff(retries - 1, fn, delay * 2))
    : Promise.reject(err));
```

Como puede ver, ambas implementaciones usan una estructura recursiva con decremento "retries" para llegar al caso base. Lo que encuentro tan impresionante con la abstracción de Promise es lo fácil que es codificar problemas complejos como este con un código mínimo.