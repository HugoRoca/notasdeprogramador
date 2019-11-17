---
date: 2019-11-17
title: Requirements.txt
weight: 25
---

### ¿Cual es el equivalente de package.json en python?

La solución es simple, usaremos `freeze`, este pequeño y poderoso comando nos retornará los paquetes que instalamos en nuestro proyecto, hay que tener en cuenta que esto solo es para los paquetes, no es para ejecutar como se hace en nodejs con `npm run` o `npm start`.

Ejemplos

1. Generando salida para un archivo de requisitos

```
> pip freeze
docutils==0.11
Jinja2==2.7.2
MarkupSafe==0.19
Pygments==1.6
Sphinx==1.2.2
```

2. Generando archivo 

```
> pip freeze > requirements.txt
```

3. Instalando en otro entorno

```
> pip install -r requirements.txt
```