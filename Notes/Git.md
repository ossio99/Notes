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