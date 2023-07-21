# Express js

Express es un framework muy minimalista

Express no proporciona un analizador de cuerpo incorporado, por lo que deberás usar un middleware para analizar el cuerpo de la solicitud.

Puedes usar el middleware incorporado express.json() para analizar los datos JSON enviados en el cuerpo de la solicitud.

Anteriormente se usaba el bodyParser pero hoy en día ya disponemos de manera masiva de la función `urlencoded()`.

Example bodyParser:

```jsx
const express = require('express');
const bodyParser = require('body-parser');

const app = express();
app.use(bodyParser.urlencoded({ extended: false }));
app.use(bodyParser.json());

app.post('/ruta', (req, res) => {
const datos = req.body; // Acceder a los datos enviados en el cuerpo de la solicitud
// ...
});
```

### Leer datos enviados por un json

```jsx
app.use(express.json())
```

### Habilitar lectura de datos de formularios

Esto aplica para cuando la petición se hace directamente con las propiedades del formulario

```jsx
app.use(express.urlencoded({extended: true}))
```

`render()`

En Express.js, **`render()`** es un método utilizado para renderizar vistas o plantillas en una aplicación web. Es parte del motor de vistas integrado de Express y se utiliza para generar la respuesta HTML que se enviará al cliente.

El método **`render()`** se utiliza junto con un motor de plantillas.

Cuando se invoca **`render()`**, se especifica el nombre de la plantilla que se desea renderizar y se pasan los datos que se utilizarán en la plantilla. Estos datos pueden ser objetos JavaScript que contienen información específica que se desea mostrar en la vista.

Example:

```jsx
// Configuración inicial del motor de plantillas EJS
app.set('view engine', 'ejs');
app.set('views', path.join(__dirname, 'views'));

// Ruta para renderizar una vista utilizando EJS
app.get('/ruta', (req, res) => {
  // Datos que se utilizarán en la plantilla
  const datos = {
    nombre: 'John Doe',
    edad: 30
  };

  // Renderizar la plantilla 'vista.ejs' con los datos proporcionados
  res.render('vista', datos);
});
```

`res.cokie()`  
Funcion usada para establecer valor al nombre de la cookie, el parametro de valor puede ser un string o un objeto convertido a json  
sintaxis:
```js
res.cookie(name, value [, options])
```
el parametro `name` contiene el nombre de la cookie y el parametro `value` es el valor asignado al nombre de la cookie. El parametro `options` contiene varias propiedades como encode, expires, domain, etc.  

**Otro ejemplo**
```js
return res.cookie('_token', token, {
  httpOnly: true,
  //secure: true
}).redirect('/mis-propiedades')
```
En este otro ejemplo vemos:
- `httpOnly`: evita los ataques cross-site ya que con esta propiedad el cookie no es accesible mediante javascipt
- `secure`: solo permite las cookies en conexiones seguras, es buena opcion en el deployment si el hosting permite tener certificado ssl

Para mas info checar: [info res.cookie()](https://www.geeksforgeeks.org/express-js-res-cookie-function/)