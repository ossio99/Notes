# Apuntes que me saque del c***
## Comandos
**Ver ramas**
```git
git branch
```
**Crear rama**
```git
git branch <nombre de la rama>
```
**Cambiar de rama**
```git
git switch <rama>
```
## Como hacer ciertas cosas
**Eliminar del repositorio archivos que ya se han confirmado (se ha hecho commit)**  
Si quieres que el archivo permanezca en tu ordenador pero simplemente que se borre del repositorio tienes que hacerlo así:
```
git rm -- cached <nombre del archivo>
```
Si lo que deseas es borrar un directorio y todos sus contenidos, tendrás que hacer algo así:
```
git rm -r -- cached <nombre del archivo>
```
El parámetro "--cached" es el que nos permite mantener los archivos en nuestro directorio de trabajo.
Una vez quitado del repositorio los archivos que no queremos, y ahora sí están ignorados, tenemos que confirmar los cambios.
```
git commit -m 'Eliminados archivos no deseados'
git push
```

# Curso pildoras informaticas
START REPO
```git
git init
```

GLOBAL CONFIG
```git
git config --global user.username ""
git config --global user.email ""
```

### BASIC COMANDS
```git
git --version
git status
git status -s
git add <nombre del archivo>
git add .
git reset <nombre del archivo> = quitar archivos del staging area
git reset . = quitar todo del stagin area
git commit -m ""
git log
git log --oneline
git reset --hard <hash del commit> = restaura, se pierden los commits posteriores
git rm <nombre del archivo> = indicarle a git que deje de hacer el seguimiento de uno o varios archivos cuando ya se hizo commit, este comando borrara el archivo y dejara el stagin area lista para solo hacer commit
git rm --dry-run <> = para ver qué archivos se borrarán sin realizar la operación
git rm --cached <> = lo mismo pero sin que se borre el archivo
git rm -r --cached = borra todos los ficheros de manera recursiva al indicar un directorio osea una carpeta con sus archivos
```

Las diferencias entre git rm y git reset son las siguientes:

`git rm --cached <file>`: remueve el archivo del indice, esto quiere decir, que Git ya no le hará seguimiento. Aunque el archivo seguirá existiendo en tu directorio, tal y como está.  
`git reset HEAD <file>`: devuelve el archivo a su último commit y este sigue en seguimiento por git, es decir podras hacer add, commit, etc. con total normalidad.  
Si realizas git status podrás darte cuenta de que el archivo al que le aplicaste `git rm --cached <file>` ya no se encuentra en seguimiento por Git porque ya no aparece.



REMOTE
```git
git remote -v
git branch -M master
git remote add origin  <url>
git push -u origin main (-u para automatizar el remoto y la rama y la proxima vez solo hacer git push)
git pull = traerme los cambios del remoto
*
```


TAGS
```git
git tag <nombre> -m ""
git push --tags
```


BRANCHES
```git
git branch <nombre de rama>
git branch = ver ramas y en cual estamos
git checkout <nombre de la rama> = moverse de rama
git merge <rama a fucionar> = nota, solo se puede hacer merge desde la rama principal
*una vez que se crea la nueva rama solo se muestran los commits de la nueva rama haciendo git log desde la nueva rama
git branch -d <nombre de rama> = borra la rama
```



```git
git clone <url>
```

# Libro midu
crear una rama y cambiarte a ella
```git
git switch -c <branch_name>
```
eliminar rama
```git
git branch -d <branch_name>
```
forzar eliminacion de rama
```git
git branch -D <branch_name>
```

# añadir y checar
- git restore, que es para restaurar un archivo modificado a su commit inmediatamente anterior sin haber vuelto a commitear
- git reset, que es para regresar al commit anterior borrando el commit actual
- investigar si se puede uno mover a un commit anterior sin necesariamente borrar los posteriores al que se regreso
- documentar lo de las pull request
- checar bien lo del head


# Dudas que tuve
## ¿Que pasa si cambio el nombre de una carpta que tengo localmente y esta vinculada a un repositorio remoto en github?
Si solo cambias el nombre de la carpeta en tu máquina local y luego haces un git push al repositorio remoto en GitHub, lo que sucederá es que el repositorio remoto creará una nueva carpeta con el nuevo nombre en lugar de actualizar el nombre de la carpeta existente.  
Esto significa que tendrás dos carpetas en el repositorio remoto: la carpeta original con el nombre antiguo y la nueva carpeta con el nombre actualizado. Además, todos los archivos y el historial de cambios dentro de la carpeta original no se transferirán automáticamente a la nueva carpeta.  
Para evitar esta situación, es recomendable realizar los siguientes pasos adicionales:  
1. Abre una terminal o línea de comandos en tu máquina y navega hasta el directorio raíz de tu repositorio local.
1. Ejecuta el comando git mv viejo_nombre nuevo_nombre para cambiar el nombre de la carpeta en el repositorio local. Asegúrate de reemplazar "viejo_nombre" con el nombre original de la carpeta y "nuevo_nombre" con el nuevo nombre que deseas asignarle.
1. Luego, realiza un commit para registrar los cambios ejecutando los comandos git add . para agregar los cambios al área de preparación y git commit -m "Cambio de nombre de carpeta" para realizar el commit.
1. Finalmente, utiliza el comando git push para enviar los cambios al repositorio remoto en GitHub.

Después de completar estos pasos, el repositorio remoto en GitHub reflejará el cambio de nombre de la carpeta. Sin embargo, ten en cuenta que si otros colaboradores tienen una copia del repositorio antes de que realices el cambio, es posible que deban actualizar su repositorio local para reflejar el cambio de nombre utilizando el comando git pull.

fuente: chat-gpt

## el repositorio remoto tiene algunos commits que no están en tu repositorio local, pero también tienes commits en tu repositorio local que aún no has subido al remoto

1. Guardar los cambios locales:  
Si tienes cambios no comprometidos (es decir, modificaciones en los archivos que aún no has hecho "git add" y "git commit"), asegúrate de comprometerlos o guardarlos en un "stash" temporal antes de continuar. De esta manera, puedes asegurarte de que no perderás esos cambios durante el proceso.
1. Actualizar el repositorio local:  
Antes de hacer cualquier otra cosa, asegúrate de tener la última versión del repositorio remoto en tu repositorio local. Ejecuta los siguientes comandos:
```git
git fetch origin
git pull origin <nombre-de-tu-rama>
```

Esto traerá los cambios del repositorio remoto a tu rama local sin fusionarlos automáticamente con tus cambios locales.

Resolver conflictos (si los hay):  
Es posible que al hacer "git pull", se generen conflictos si tus cambios locales y los cambios remotos afectan las mismas líneas de código. Git te informará sobre estos conflictos y tendrás que resolverlos manualmente. Utiliza un editor de código o una herramienta de resolución de conflictos para corregir los archivos con conflictos. Una vez que hayas resuelto todos los conflictos, realiza un nuevo "git add" y "git commit" para registrar los cambios.

Actualizar el repositorio remoto:  
Después de haber resuelto los conflictos y haber hecho un commit con los cambios, ahora puedes actualizar el repositorio remoto con tus commits locales. Ejecuta:
```git
git push origin <nombre-de-tu-rama>
```
Si estás trabajando en una rama diferente a la principal, asegúrate de cambiar <nombre-de-tu-rama> por el nombre correcto de tu rama.

Con estos pasos, deberías haber sincronizado correctamente tus cambios locales con los cambios remotos sin perder ningún trabajo. Sin embargo, siempre es una buena práctica tener cuidado y comprender las acciones que estás realizando, ya que las operaciones de git pueden afectar tu código y el de tus colaboradores.

fuente: chat-gpt

## al clonar un repositorio te traes todas las ramas del repo remoto???
Cuando clonas un repositorio remoto, por defecto, se copiarán todas las ramas del repositorio remoto en tu repositorio local. Esto incluirá la rama predeterminada (generalmente "master" o "main") y todas las demás ramas que puedan estar presentes en el repositorio remoto.  
Al clonar el repositorio, toda la historia del proyecto, incluidos todos los commits y las diferentes ramas, se copiará en tu sistema local. Esto te permitirá trabajar con el repositorio de manera completa, incluyendo la posibilidad de alternar entre las diferentes ramas y realizar modificaciones en ellas.  
fuente: chat-gpt


## cuando le hago un pull a un repositorio remoto me traigo a mi repo local solo los cambios que tiene esa misma rama o se trae cambios de todas las ramas?
Cuando haces un "pull" desde un repositorio remoto a tu repositorio local, solo te traerás los cambios que se encuentran en la rama específica que estás extrayendo. No afectará a otras ramas en tu repositorio local.

El comando "git pull" se utiliza para obtener los cambios más recientes del repositorio remoto y fusionarlos con la rama actual en la que te encuentras en tu repositorio local. Si no especificas una rama en particular en el comando "git pull", se utilizará la rama actual por defecto.

Por ejemplo, si estás en la rama "main" de tu repositorio local y ejecutas el comando:
```git
git pull origin main
```
Esto traerá los cambios que se han realizado en la rama "main" del repositorio remoto llamado "origin" y los fusionará con la rama "main" en tu repositorio local. No se verán afectadas otras ramas que puedas tener en tu repositorio local.

Si deseas traer cambios de otras ramas del repositorio remoto, tendrás que hacer un "pull" explícito de esas ramas utilizando el comando:
```git
git pull origin nombre_de_otra_rama
```
Esto solo afectará a la rama local que estés trabajando en ese momento y no interferirá con las demás ramas en tu repositorio. Recuerda que siempre es importante verificar en qué rama te encuentras antes de ejecutar el comando "git pull" para evitar fusiones no deseadas o conflictos.

##  traer los cambios de todas las ramas a tu repositorio local
1. **Asegúrate de estar en la rama principal (por lo general, "master" o "main")**  
Antes de realizar cualquier actualización, es recomendable que te encuentres en la rama principal de tu repositorio local. Puedes verificar la rama actual utilizando el comando:
    ```git
    git status
    ```
    Si no estás en la rama principal, cámbiate a ella usando:
    ```git
    git checkout nombre_de_la_rama_principal
    ```
2. **Actualiza tu rama principal local**  
Antes de traer los cambios de todas las ramas, asegúrate de tener la versión más actualizada de la rama principal. Esto se hace mediante el comando git pull:
    ```git
    git pull origin nombre_de_la_rama_principal
    ```
3. **Trae los cambios de todas las ramas**  
    Para traer los cambios de todas las ramas, primero debes obtener una lista de todas las ramas remotas disponibles. Para ello, utiliza el siguiente comando:
    ```git
    git fetch --all
    ```
    Esto descargará todas las referencias de las ramas remotas, pero no realizará cambios en tu repositorio local.

4. **Mezcla las ramas con la rama principal**  
Ahora que tienes los cambios de todas las ramas en tu repositorio local, puedes mezclarlas con la rama principal. Asegúrate de estar en la rama principal antes de ejecutar la mezcla:
    ```git
    git checkout nombre_de_la_rama_principal
    ```
    Una vez en la rama principal, utiliza el siguiente comando para mezclar los cambios de todas las ramas:
    ```git
    git merge --no-ff origin/otra_rama
    ```

    Este comando realizará una mezcla no rápida (no fast-forward) para asegurarse de que se cree un commit de mezcla, incluso si no hay conflictos.

    Repite el paso anterior para todas las demás ramas que desees mezclar con la rama principal.

5. **Resuelve conflictos (si los hay)**  
En caso de que haya conflictos al mezclar las ramas, Git te mostrará los archivos con conflictos y te pedirá que los resuelvas manualmente. Una vez resueltos los conflictos, deberás hacer git add a los archivos modificados y luego hacer un commit para aplicar los cambios.

6. **Sube los cambios**  
Finalmente, después de haber mezclado todas las ramas y resuelto los conflictos, puedes subir los cambios a tu repositorio remoto:

    ```git
    git push origin nombre_de_la_rama_principal
    ```
Con estos pasos, habrás traído los cambios de todas las ramas a tu repositorio local y los habrás mezclado en la rama principal. Recuerda que, en ocasiones, mezclar muchas ramas puede generar conflictos complejos, así que es importante revisar los cambios con detenimiento antes de realizar la mezcla.

## al borrar una rama en local y hacer push no se borra solita del remoto
si creas o eliminas una rama localmente y luego haces un push, eso no afectará directamente la rama en el repositorio remoto.

Al hacer un push, estás enviando los cambios de las ramas locales al repositorio remoto, pero solo afectará a las ramas que hayas especificado explícitamente en el comando push. Por lo tanto, si has eliminado una rama local y luego realizas un push, la rama eliminada no se eliminará automáticamente del repositorio remoto.

Para eliminar una rama en el repositorio remoto, debes usar el comando específico para eliminar ramas remotas. El comando puede variar según el sistema de control de versiones que estés utilizando, pero en Git, el comando generalmente es:
```git
git push <nombre_remoto> --delete <nombre_rama>
```

## traer una nueva rama creada en el repositorio remoto a tu repositorio local

1. Asegúrate de tener el repositorio remoto configurado:  
Si aún no lo has hecho, agrega el repositorio remoto a tu repositorio local utilizando el siguiente comando (reemplaza "origin" con el nombre que desees para el repositorio remoto y "URL_DEL_REPOSITORIO" con la URL del repositorio remoto):

    ```bash
    git remote add origin URL_DEL_REPOSITORIO
    ```

2. Verifica los repositorios remotos:   
Puedes verificar los repositorios remotos configurados en tu repositorio local usando el siguiente comando:

    ```bash
    git remote -v
    ```

3. Actualiza la lista de ramas remotas:  
Antes de traer la nueva rama, asegúrate de que tu repositorio local esté al tanto de todas las ramas remotas. Para hacerlo, ejecuta el siguiente comando:

    ```bash
    git fetch origin
    ```

4. Trae la nueva rama:  
Ahora, puedes crear una copia local de la nueva rama que se creó en el repositorio remoto usando el siguiente comando (reemplaza "nombre_de_la_rama" con el nombre de la rama que deseas traer):

    ```bash
    git checkout -b nombre_de_la_rama origin/nombre_de_la_rama
    ```

    Este comando creará una nueva rama en tu repositorio local con el mismo nombre que la rama remota y te cambiará automáticamente a esa nueva rama.

    Una vez que hayas seguido estos pasos, deberías tener la nueva rama del repositorio remoto en tu repositorio local y podrás trabajar con ella como lo harías con cualquier otra rama local. Recuerda que después de hacer cambios en la nueva rama local, puedes subirlos al repositorio remoto usando el comando `git push`.

# Dudas
- al borrar una rama local si sigue estando en el remoto como la recupero?
- si al hacer pull desde mi rama, solo me traigo los cambios de esta misma en el remoto, entonces mi rama solo se actualiza hasta que se haga un merge despues de autorizar un pr???
- si creo una rama en el remoto como me la traigo al local???
- preguntar si hay cambios en el remoto para proceder a hacer un pull, creo que esto lo hace git fetch
- ver los cambios entre commits, creo que esto lo hace git diff

# Hacer:
* make sure that the new branch is on the remote

# checar curso mouredev
- git diff
- git fetch
- Checkout
- reset para navegar entre commits, 
- git diff ver cambios en archivos sin tener que hacer commits
- desplazamiento en una rama
- git reset hard
- reintegración de ramas

