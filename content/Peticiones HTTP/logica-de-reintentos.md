---
date: 2019-10-30
title: Lógica de reintentos
weight: 25
---

Las promesas son una abstracción invaluable en torno a resultados 'eventuales' dentro de operaciones asincrónicas. Recientemente tuve la necesidad de poder volver a intentar una acción basada en Promesa en caso de falla. Resultó ser muy fácil implementar tal proceso usando construcciones recursivas simples.

Inicialmente solo requería la capacidad de volver a intentar la cantidad deseada de veces, antes de fallar eventualmente si aún no tenía éxito.

El siguiente código lo que realiza es que si una "petición http" falla, entra al catch por defecto, luego valida los `retries`, en caso que es este sea cero retornará el error en si.

```
const retry = (retries, fn) => fn().catch(err => retries > 1 ? retry(retries - 1, fn) : Promise.reject(err));
```
