# Express validator  
## Instalación  
```sh
npm install express-validator
```
## Agregar un validator  
En el siguiente ejemplo se muestra como agregar un validator que verifica que el query string ``person`` no pueda estar vacía, con el validador nombrado intuitivamente ``notEmpty()``:
```js
const express = require('express');
const { query } = require('express-validator');
const app = express();

app.use(express.json());
app.get('/hello', query('person').notEmpty(), (req, res) => {
  res.send(`Hello, ${req.query.person}!`);
});

app.listen(3000);
```
Checar la documentación para ver todos los validators  
## Manejando los errores de validación  
express-validator no reporta los errores de validación a los usuarios automáticamente, por lo que tenemos que verificar el resultado de las validaciones con la función `validationResult()`
```js
const express = require('express');
const { query } = require('express-validator');
const app = express();

app.use(express.json());
app.get('/hello', query('person').notEmpty(), (req, res) => {
  res.send(`Hello, ${req.query.person}!`);
});

app.listen(3000);
```
``validationResult()``  
Devuelve un objeto con una función y el arreglo de errores  
<img width="395" alt="Untitled" src="https://github.com/ossio99/Libraries/assets/108959960/107a2ed0-3eb3-4fc2-93c5-f64932b561d7">  
Si le aplicamos el método `array()` a la respuesta, como se observa en el ejemplo anterior, obtenemos solamente el array de errores.  
Ejemplo del resultado:
```js
{
  "errors": [
    {
      "location": "query",
      "msg": "Invalid value",
      "path": "person",
      "type": "field"
    }
  ]
}
```
Por lo que, para validar los errores lo que se hace es validar si lo que devolvió este método  `validationResult()` , como se muestra en ilustración 2, donde se usa un condicional que evalúa con un validator.

## Mensajes de error  
Hay varias formas de customizar el msg de error

### Validator-level message  
Un validator-level message aplica soo cuando el campo falla en un validador especifico. Este se puede usar con el metodo `withMessage()`
```js
body('email').isEmail().withMessage('Not a valid e-mail address');
```

## Código del proyecto Bienes Raices Node  
Hasta ahora se ha explicado en palabras propias lo de la documentación pero ahora analicemos el código que se realizo en el proyecto:
```jsx
await check('nombre').notEmpty().withMessage('El nombre no puede ir vacio').run(req)
```
`check()`  
según lo que entendí después de leer la doc, express validator  automáticamente toma los campos por su name provenientes de la localización donde se hizo la petición ya que en la doc dice que de no proporcionar el nombre de los campos, tomara la ubicación completa de la petición
