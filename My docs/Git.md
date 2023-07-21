# Comandos
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

# Dudas que tuve
**¿Que pasa si cambio el nombre de una carpta que tengo localmente y esta vinculada a un repositorio remoto en github?**  
Si solo cambias el nombre de la carpeta en tu máquina local y luego haces un git push al repositorio remoto en GitHub, lo que sucederá es que el repositorio remoto creará una nueva carpeta con el nuevo nombre en lugar de actualizar el nombre de la carpeta existente.  
Esto significa que tendrás dos carpetas en el repositorio remoto: la carpeta original con el nombre antiguo y la nueva carpeta con el nombre actualizado. Además, todos los archivos y el historial de cambios dentro de la carpeta original no se transferirán automáticamente a la nueva carpeta.  
Para evitar esta situación, es recomendable realizar los siguientes pasos adicionales:  
1. Abre una terminal o línea de comandos en tu máquina y navega hasta el directorio raíz de tu repositorio local.
1. Ejecuta el comando git mv viejo_nombre nuevo_nombre para cambiar el nombre de la carpeta en el repositorio local. Asegúrate de reemplazar "viejo_nombre" con el nombre original de la carpeta y "nuevo_nombre" con el nuevo nombre que deseas asignarle.
1. Luego, realiza un commit para registrar los cambios ejecutando los comandos git add . para agregar los cambios al área de preparación y git commit -m "Cambio de nombre de carpeta" para realizar el commit.
1. Finalmente, utiliza el comando git push para enviar los cambios al repositorio remoto en GitHub.

Después de completar estos pasos, el repositorio remoto en GitHub reflejará el cambio de nombre de la carpeta. Sin embargo, ten en cuenta que si otros colaboradores tienen una copia del repositorio antes de que realices el cambio, es posible que deban actualizar su repositorio local para reflejar el cambio de nombre utilizando el comando git pull.