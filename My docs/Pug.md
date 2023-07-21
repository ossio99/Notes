## full page
**include**   
incluye todo el archivo  
no es necesario alguna declaracion especial, solo cuando quieras incluir un archivo completo en otro solo usa include
estructura:  
```
include <nombre del archivo (sin extensión)>
include <ruta del archivo (sin extensión)>
```
nota: al parecerla segunda sintaxis es cuando el archivo a incluir no esta en la misma carpeta  
nota: checar cuando usar la ruta del archivo en include

## partial
**block**  
solo es un bloque de código  
solo se renderiza en los archivos donde se llama el block  
el contenido del block es dinámico  
el contenido del block será el contenido que se le ponga al block en el archivo donde se llama
que en donde este el block x en el layout ira un contenido dinámico que será el que se defina en donde se llame  
esta palabra reservada va de la mano con extends ya que con extends se conexta el otro archivo con el block  
esta palabra va en donde se declara el block y donde se llama despues de extends
estructura:  
```
block <nombre del bloque>
```

**extends**  
palabra reservada para indicar que una vista extiende de otro archivo, por lo regular un layout  
estructura:
```
extends <ruta del archivo del cual extender>
```

## notas  
para poner clases con hover se tiene que usar la sintaxis:
```pug
a(href="/propiedades/crear" class="hover:700") Publicar propiedad
```
ya que no se pueden poner pseudo clases con la sintaxis tradicional de pug
```pug
h1.text-4xl.my-10.font-extrabold.text-center Bienes
```

## como hacerlo en pug

**bucles**  
```
option(value='') - Seleccione -
- var n = 1
while n < 5
    option(value=n) #{n++}
```

**agregar media queries con tailwind** 
se debe usar la sintaxis de clase entre parentessi 
```
div(class='md:flex md:gap-4 space-y-5 md:space-y-0')

```

**checar**
- include solo se llama y es para archivo completo???
- extense es para extender de otro archivo, igual se fucionan el archivo completo del que se extiende y donde se esta extendiendo completo