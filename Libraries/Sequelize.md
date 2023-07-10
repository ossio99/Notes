# Sequelize

Es un ORM (Object relational maping)

## Instalación

```bash
npm install --save sequelize
npm install --save mysql2
```

Dependiendo de la base de datos a ocupar se debe instalar un motor extra, en este ejemplo se muestra para mysql

Al crear una nueva instancia de Sequelize debemos pasarle los siguientes parámetros:

### **DB**

### Usuario

### **Password**

### Objeto de configuración

Este objeto de configuración lleva la siguiente estructura:

### **host**

### **port**

El puerto por defecto de mysql es 3306

### dialect

Motor de db

### timestamps

Cuando un usuario se registra agrega 2 columnas extras a la tabla de usuario cuando fue creado y cuando fue actualizado

### pool

Abrir y cerrar conexiones de base de datos (i.e. conexiones de sockets tcp o similares) toma algún tiempo. Especialmente en aplicaciones Web, en las que no es para nada bueno tener que abrir un nueva conexión para cada acción del usuario, lo que suele hacerse es tener un pequeño `pool` de conexiones que siempre están abiertas y son compartidas entre los usuarios. Un pool de conexiones *mantiene un número de conexiones a la base datos abiertas* y este número puede variar dependiendo de la carga del servicio. De forma en lugar de abrir tu mismo una nueva conexión simplemente solicitas alguna de las disponibles, *mejorando de esta forma el desempeño de tu aplicación*. El no cerrar tus conexiones y abrir nuevas cada que las necesitas es un desperdicio de recursos y conducirá a un mal desempeño de la misma.

Parametros del pool:

**max y min**

maximo y minimo de conexiones a mantener (por usuario)

**acquire**

el tiempo que va a pasar tratando de elaborar una conexion antes de marcar un error

**idle**

tiempo que debe transcurrir para finalizar una conexion a la db para liberar recursos

### operatorAliases

Era algo que existia hace tiempo

Example of data base instance:

```jsx
import Sequelize from 'sequelize'

const db = new Sequelize('bienesraices_node_mvc', 'root', '', {
    host: 'localhost',
    port: 3306,
    dialect: 'mysql',
    define: {
        timestamps: true
    },
    pool: {
        max: 5,
        min: 0,
        acquire: 3000,
        idle: 10000
    },
    operatorAliases: false
})

export default db;
```

## Modelo

Un modelo es una abstracción que representa una tabla en su base de datos. En Sequelize, es una clase que extiende [Model](https://sequelize.org/api/v6/class/src/model.js~Model.html) .

El modelo le dice a Sequelize varias cosas sobre la entidad que representa, como el nombre de la tabla en la base de datos y qué columnas tiene (y sus tipos de datos).

Un modelo en Sequelize tiene un nombre. Este nombre no tiene que ser el mismo nombre de la tabla que representa en la base de datos. Por lo general, los modelos tienen nombres en singular (como `User`) mientras que las tablas tienen nombres en plural (como `Users`), aunque esto es totalmente configurable.

### Definición del modelo

Example:

```jsx
const { Sequelize, DataTypes } = require('sequelize');
const sequelize = new Sequelize('sqlite::memory:');

const User = sequelize.define('User', {
  // Model attributes are defined here
  firstName: {
    type: DataTypes.STRING,
    allowNull: false
  },
  lastName: {
    type: DataTypes.STRING
    // allowNull defaults to true
  }
}, {
  // Other model options go here
});

//Codigo con juan example
const Usuario  = db.define('usuarios', {
    nombre: {
        type: DataTypes.STRING,
        allowNull: false
    },
    email: {
        type: DataTypes.STRING,
        allowNull: false
    },
    password: {
        type: DataTypes.STRING,
        allowNull: false
    },
    token: DataTypes.STRING,
    confirmado: DataTypes.BOOLEAN
})

// `sequelize.define` also returns the model
console.log(User === sequelize.models.User); // true
```

### METODOS DE MODELO

`define()`

Método para crear un nuevo modelo, se aplica a una instancia de la db.

Parámetros:

Recibe como primer parámetro la tabla.

Como segundo parámetro recibe un objeto con todos los campos, cada campo puede tener como valor el tipo de dato u otro objeto en caso de que se definan más parámetros.

`create()`

crear un nuevo registro extendiendo de un modelo

```jsx
const registrar = async (req, res) => {
    console.log(req.body);
    const usuario = await Usuario.create(req.body)
    res.json(usuario)
}
```

`findOne()`

Devuelve una promesa de un objeto con la data del primer registro en la db que coincida con consulta, recibe un objeto con la info con la que buscara en la db.

Example:

```jsx
await Usuario.findOne( {where: { email: req.body.email }} )
```

### No métodos de modelo

`sync()`

Crear una tabla en caso de que no exista, se debe extender de una instancia de la db

```jsx
// Conexion a la base de datos
try {
    await db.authenticate()
    db.sync()
    console.log('Conexion correcta a la base de datos');
} catch (error) {
    console.log(error);
}
```

Hooks

Los hooks (también conocidos como eventos del ciclo de vida) son funciones que se llaman antes y después de que se ejecuten las llamadas en Sequelize. Por ejemplo, si desea establecer siempre un valor en un modelo antes de guardarlo, puede agregar un `beforeUpdate`enlace.

**Declaración de Hooks**

Los argumentos a los hooks se pasan por referencia. Esto significa que puede cambiar los valores, y esto se reflejará en la declaración de inserción/actualización. Un hook puede contener acciones asíncronas; en este caso, la función de hook debería devolver una promesa.

A continuación una de las formas de declarar hooks (checar doc para ver las demás)

```jsx
const Usuario  = db.define('usuarios', {
    nombre: {
        type: DataTypes.STRING,
        allowNull: false
    },
    email: {
        type: DataTypes.STRING,
        allowNull: false
    },
    password: {
        type: DataTypes.STRING,
        allowNull: false
    }
}, {
    hooks: {
        beforeCreate: async function(usuario) {
            const salt = await bcrypt.genSalt(10)
            usuario.password = await bcrypt.hash(usuario.password, salt)
        }
    }
})
```

El hook tiene una propiedad que es una función la cual recibe la ¿instancia del modelo?, y dentro de esta función podemos hacer lo que sea
