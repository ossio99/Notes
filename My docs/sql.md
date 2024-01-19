## Insertar datos en una tabla (multiples registros a la vez)
El orden de los campos es arbitrario, sin embargo, en el orden que se definen los campos sera el orden que deben ir los valores
```sql
INSERT INTO Transacciones (FechaTransaccion, Monto, TipoTransaccionId, UsuarioId, Nota)
VALUES
('2022-11-07', 5000, 1, 'lalo', 'Prueba'),
('2022-11-07', 1000, 2, 'lalo', 'Prueba 2');
```

## Ordenando ciertos campos por un campo de manera descendente
```sql
SELECT Id, UsuarioId, Monto, Nota
FROM Transacciones
ORDER BY Monto DESC
```
Cabe recalcar que para ordenar de manera ascendente no es nesesario poner `ASC` a menos que se quiera ser explicito

## Ordenando en base a varios campos
`DESC` solo aplicara a `Monto`
```sql
SELECT Id, UsuarioId, Monto, Nota
FROM Transacciones
ORDER BY UsuarioId, Monto DESC
```

# Filtros
```sql
/*seleccionamos los campos de transacciones cuando Id sea menor a 1*/
SELECT Id, UsuarioId, Monto, Nota
FROM Transacciones
WHERE Id <> 1

SELECT Id, UsuarioId, Monto, Nota
FROM Transacciones
WHERE Id != 1

SELECT Id, UsuarioId, Monto, Nota
FROM Transacciones
WHERE Nota is not null
```

# Actualizando campos
```sql
UPDATE Transacciones
SET Nota = 'nota actualizada', Monto = 4780
WHERE Id = 1
```

# Borrando registros
Borrando todos los registros de la tabla
```sql
DELETE Transacciones 
```

### Borrando registros con condicion
```sql
DELETE Transacciones
WHERE Id = 9
```

# Haciendo SELECT una lista de valores en el WHERE
Se traera todos los registros de Transacciones donde Monto no sea ninguno de los 2 valores
```sql
SELECT *
FROM Transacciones
WHERE Monto NOT in (350, 499.99)
```

## Traer registros donde un campo tenga un cierto valor
para esto usamos el operador `like`
```sql
SELECT *
FROM Transacciones
WHERE UsuarioId like '%f%'
```
en este query, decimos que se traiga todos los registros de `Transacciones` donde `UsuarioId` contenga `f`, ya sea al antes o despues  
combinando operadores logicos
```sql
SELECT *
FROM Transacciones
WHERE UsuarioId like '%pe' AND Nota is not null AND FechaTransaccion = '2021-10-03'
```

## Validando con operador `OR`
```sql
SELECT *
FROM Transacciones
WHERE (UsuarioId = 'felipe' AND Monto = 501) OR UsuarioId = 'abc'
```

## Validando fecha con funcion `YEAR`
usamos la funcion `YEAR` para validar el año
```sql
SELECT *
FROM Transacciones
WHERE YEAR(FechaTransaccion) = 2020

SELECT *
FROM Transacciones
WHERE MONTH(FechaTransaccion) = 5
```

## Operador `BETWEEN`
```sql
SELECT *
FROM Transacciones
WHERE FechaTransaccion >= '2021-11-01' AND FechaTransaccion <= '2021-11-30'

SELECT *
FROM Transacciones
WHERE FechaTransaccion BETWEEN '2021-11-01' AND '2021-11-30'

SELECT *
FROM Transacciones
WHERE Monto NOT BETWEEN 350 AND 501
```

## Operador `TOP`
para traer los primeros n elementos
```sql
SELECT TOP 3 *
FROM Transacciones
WHERE Monto <= 501

SELECT TOP 50 PERCENT *
FROM Transacciones
```


## Suma
sumar los registros de un resultado
```sql
SELECT SUM(Monto) as Suma
FROM Transacciones
```
`as` permite asignarle un nombre al resultado de la operacion

```sql
SELECT SUM(Monto) as Suma, UsuarioId
FROM Transacciones
GROUP BY UsuarioId
```


# Notas
- Si seleccionas algo en sql server y ejecutas el query se va a ejecutar solo lo que este seleccionado

- `<>` significa menor

- `%` significa que lo que sea que este ya sea antes o despues

# Documentar
- Falta documentar desde GROUP BY Y SUM

# Relaciones
## 1 a muchos
En SQL Server, una relación de uno a muchos se define estableciendo una conexión entre dos tablas a través de una clave primaria en una tabla y una clave foránea en la otra tabla. Esta relación permite que una fila en la tabla principal esté relacionada con varias filas en la tabla secundaria.

Aquí hay un ejemplo de cómo se podría definir una relación de uno a muchos en SQL Server:

Supongamos que tienes dos tablas: "Clientes" y "Pedidos". Quieres establecer una relación de uno a muchos entre los clientes y sus pedidos, lo que significa que un cliente puede tener varios pedidos asociados.

1. Crear la tabla "Clientes":

```sql
CREATE TABLE Clientes (
    ClienteID INT PRIMARY KEY,
    Nombre VARCHAR(50),
    -- Otros campos de cliente
);
```

2. Crear la tabla "Pedidos":

```sql
CREATE TABLE Pedidos (
    PedidoID INT PRIMARY KEY,
    ClienteID INT,
    FechaPedido DATE,
    -- Otros campos de pedido
    FOREIGN KEY (ClienteID) REFERENCES Clientes(ClienteID)
);
```

En este ejemplo, la tabla "Clientes" tiene una columna llamada "ClienteID", que es su clave primaria. La tabla "Pedidos" tiene una columna "PedidoID" como clave primaria y una columna "ClienteID" como clave foránea que se relaciona con la columna "ClienteID" en la tabla "Clientes".

La declaración `FOREIGN KEY (ClienteID) REFERENCES Clientes(ClienteID)` en la definición de la tabla "Pedidos" establece la relación de clave foránea con la tabla "Clientes", lo que garantiza que los valores en la columna "ClienteID" en la tabla "Pedidos" deben coincidir con valores existentes en la columna "ClienteID" de la tabla "Clientes".

Con esta configuración, puedes vincular los pedidos a los clientes mediante el campo "ClienteID", lo que representa una relación de uno a muchos, ya que un cliente puede tener varios registros en la tabla "Pedidos".

## 1 a 1
En SQL Server, una relación uno a uno se establece de manera similar a una relación uno a muchos, pero en este caso, la diferencia es que cada registro en la tabla principal (uno) se relaciona con solo un registro en la tabla secundaria (uno). Aquí te muestro cómo definir una relación uno a uno:

Supongamos que tienes dos tablas: "Empleados" y "DetallesEmpleados". Quieres establecer una relación uno a uno entre los empleados y sus detalles personales.

1. Crear la tabla "Empleados":

```sql
CREATE TABLE Empleados (
    EmpleadoID INT PRIMARY KEY,
    Nombre VARCHAR(50),
    -- Otros campos de empleado
);
```

2. Crear la tabla "DetallesEmpleados":

```sql
CREATE TABLE DetallesEmpleados (
    EmpleadoID INT PRIMARY KEY,
    FechaNacimiento DATE,
    Direccion VARCHAR(100),
    -- Otros campos de detalles
    FOREIGN KEY (EmpleadoID) REFERENCES Empleados(EmpleadoID)
);
```

En este ejemplo, la tabla "Empleados" tiene una columna "EmpleadoID" como clave primaria. La tabla "DetallesEmpleados" también tiene una columna "EmpleadoID" como clave primaria y una columna "FechaNacimiento", "Direccion", etc., para almacenar los detalles personales.

La declaración `FOREIGN KEY (EmpleadoID) REFERENCES Empleados(EmpleadoID)` en la definición de la tabla "DetallesEmpleados" establece la relación de clave foránea con la tabla "Empleados", lo que garantiza que los valores en la columna "EmpleadoID" en la tabla "DetallesEmpleados" deben coincidir con valores existentes en la columna "EmpleadoID" de la tabla "Empleados".

Esta configuración asegura que cada empleado tenga un único registro en la tabla "DetallesEmpleados", y viceversa, lo que representa una relación uno a uno entre las dos tablas.

## muchos a muchos
En SQL Server, para establecer una relación muchos a muchos entre dos tablas, generalmente se necesita una tercera tabla intermediaria que actúa como un puente entre las dos tablas principales. Esta tercera tabla contiene las claves primarias de ambas tablas principales y se utiliza para registrar las relaciones entre ellas. Aquí te muestro cómo definir una relación muchos a muchos:

Supongamos que tienes dos tablas: "Estudiantes" y "Cursos". Quieres establecer una relación muchos a muchos entre los estudiantes y los cursos, ya que un estudiante puede estar inscrito en varios cursos y un curso puede tener varios estudiantes.

1. Crear la tabla "Estudiantes":

```sql
CREATE TABLE Estudiantes (
    EstudianteID INT PRIMARY KEY,
    Nombre VARCHAR(50),
    -- Otros campos de estudiante
);
```

2. Crear la tabla "Cursos":

```sql
CREATE TABLE Cursos (
    CursoID INT PRIMARY KEY,
    NombreCurso VARCHAR(50),
    -- Otros campos de curso
);
```

3. Crear la tabla intermedia "EstudiantesCursos":

```sql
CREATE TABLE EstudiantesCursos (
    EstudianteID INT,
    CursoID INT,
    PRIMARY KEY (EstudianteID, CursoID),
    FOREIGN KEY (EstudianteID) REFERENCES Estudiantes(EstudianteID),
    FOREIGN KEY (CursoID) REFERENCES Cursos(CursoID)
);
```

En este ejemplo, la tabla "EstudiantesCursos" actúa como la tabla intermedia que establece la relación muchos a muchos. Tiene dos columnas, "EstudianteID" y "CursoID", que son claves foráneas que hacen referencia a las tablas "Estudiantes" y "Cursos", respectivamente. La declaración `PRIMARY KEY (EstudianteID, CursoID)` establece una clave primaria compuesta para evitar duplicados.

De esta manera, puedes registrar qué estudiantes están inscritos en qué cursos. Cada fila en "EstudiantesCursos" representa una relación entre un estudiante y un curso.

Esta configuración permite manejar una relación muchos a muchos de manera eficiente y estructurada.