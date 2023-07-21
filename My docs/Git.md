Ver ramas
```git
git branch
```
Crear rama
```git
git branch <nombre de la rama>
```
Cambiar de rama
```git
git switch <rama>
```

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

# another one
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

# añadir y checar
- git restore, que es para restaurar un archivo modificado a su commit inmediatamente anterior sin haber vuelto a commitear
- git reset, que es para regresar al commit anterior borrando el commit actual
- investigar si se puede uno mover a un commit anterior sin necesariamente borrar los posteriores al que se regreso
- documentar lo de las pull request
- checar bien lo del head
