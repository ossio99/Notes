# Javascript

### Optional chaining operator (?)
Es una característica introducida en ECMAScript 2020 (también conocido como ES11) y se utiliza para acceder a propiedades de un objeto de forma segura cuando alguna de las propiedades en la cadena de acceso puede ser null o undefined.

Antes de que existiera este operador, al intentar acceder a una propiedad de un objeto que era null o undefined, se producía un error que podía detener la ejecución del código. Con el operador ?., si alguna propiedad en la cadena de acceso es null o undefined, la evaluación se detiene y devuelve undefined en lugar de lanzar un error, permitiendo que el código continúe ejecutándose sin interrupciones.

Ejemplo de uso del operador ?.:

```javascript
const person = {
    name: "John",
    age: 30,
    address: {
        city: "New York",
        zipCode: 12345
    }
}

// Acceso seguro a propiedades
const city = person?.address?.city; // "New York"
const country = person?.address?.country; // undefined (no existe la propiedad "country" en el objeto)

// Evita errores si el objeto es nulo o indefinido
const notExistingObject = null;
const result = notExistingObject?.someProperty; // undefined, no se lanza un error
```

El operador ?. es muy útil para evitar errores en situaciones donde no se tiene garantía de que todas las propiedades de un objeto estén presentes.

### Nulish operator (??)
El "nulish coalescing operator" o "nullish operator" en JavaScript es un operador que también se conoce como `??` (doble signo de interrogación). Fue introducido en ECMAScript 2020 (ES11). Este operador se utiliza para proporcionar un valor predeterminado en caso de que el valor de la izquierda sea `null` o `undefined`, pero no cuando el valor es falsy (es decir, `null` o `undefined`, pero no `0`, `false`, `""`, etc.).

La sintaxis del operador es la siguiente:

```javascript
const result = valorIzquierdo ?? valorPredeterminado;
```

Si `valorIzquierdo` es `null` o `undefined`, entonces `valorPredeterminado` se asigna a `result`. En caso contrario, `valorIzquierdo` se asigna a `result`.

Ejemplo:

```javascript
const name = null;
const defaultName = "John Doe";

const displayName = name ?? defaultName;
console.log(displayName); // Output: "John Doe" (name es null, por lo tanto se utiliza defaultName)
```

Comparado con el operador de "coalescencia" o `||`, que también puede proporcionar un valor predeterminado, el operador nulish `??` no considera como falso los valores `0`, `false`, `""` (string vacío), entre otros. Solo considera `null` o `undefined` como valores para los cuales se debe utilizar el valor predeterminado.

### Map
El objeto **`Map`** contiene pares clave-valor y recuerda el orden de inserción original de las claves. Cualquier valor (tanto objetos como [valores primitivos](https://developer.mozilla.org/en-US/docs/Glossary/Primitive) ) puede usarse como clave o como valor.

```jsx
const map1 = new Map();

map1.set('a', 1);
map1.set('b', 2);
map1.set('c', 3);

console.log(map1.get('a'));
// Expected output: 1

map1.set('a', 97);

console.log(map1.get('a'));
// Expected output: 97

console.log(map1.size);
// Expected output: 3

map1.delete('b');

console.log(map1.size);
// Expected output: 2
````
