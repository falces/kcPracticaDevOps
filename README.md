# DESPLIEGUE
Se ha desplegado la aplicación en una instancia Ubuntu 18.04. Se usa Nginx como servidor web y proxy inverso. Se ha instalado MongoDB y PM2 para mantener el proceso de la aplicación funcionando en todo momento.

Para acceder a la aplicación he configurado el dominio ozonea.com (que redireccionará a www.ozonea.com).

Los archivos estáticos de tipo imagen y hojas de estilos se sirven directamente sin pasar por Node, se puede ver en: http://www.ozonea.com/anuncios y en el inspector de cualquier hoja de estilo o imagen se puede ver la cabecera X-Owner: falces.

La dirección IP de la instancia es 3.126.88.226. Si accedemos a esta dirección desde un navegador web accedemos a una plantilla Bootstrap de ejemplo.

# NodePop

[Demo](/anuncios) of the methods (this link works only if you run the project)

Api for the iOS/Android apps.

## Deploy

### Install dependencies

    npm install

### Configure

Review lib/connectMongoose.js to set database configuration

### Init database

    npm run installDB

## Start

To start a single instance:

    npm start

To start in development mode:

    npm run dev (including nodemon & debug log)

## Test

    npm test (pending to create, the client specified not to do now)

## JSHint & JSCS

    npm run hints

## API v1 info

### Base Path

The API can be used with the path:
[API V1](/apiv1/anuncios)

### Error example

    {
      "ok": false,
      "error": {
        "code": 401,
        "message": "This is the error message."
      }
    }

### GET /anuncios

**Input Query**:

start: {int} skip records
limit: {int} limit to records
sort: {string} field name to sort by
includeTotal: {bool} whether to include the count of total records without filters
tag: {string} tag name to filter
venta: {bool} filter by venta or not
precio: {range} filter by price range, examples 10-90, -90, 10-
nombre: {string} filter names beginning with the string

Input query example: ?start=0&limit=2&sort=precio&includeTotal=true&tag=mobile&venta=true&precio=-90&nombre=bi

**Result:**

    {
      "ok": true,
      "result": {
        "rows": [
          {
            "_id": "55fd9abda8cd1d9a240c8230",
            "nombre": "iPhone 3GS",
            "venta": false,
            "precio": 50,
            "foto": "/images/anuncios/iphone.png",
            "__v": 0,
            "tags": [
              "lifestyle",
              "mobile"
            ]
          }
        ],
        "total": 1
      }
    }

### GET /anuncios/tags

Return the list of available tags for the resource anuncios.

**Result:**

    {
      "ok": true,
      "allowed_tags": [
        "work",
        "lifestyle",
        "motor",
        "mobile"
      ]
    }
