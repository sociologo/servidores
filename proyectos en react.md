https://www.csharp.com/article/deploy-reactjs-app-to-azure-app-service-from-vs-code/#:~:text=Open%20Visual%20Studio%20Code%20and,running%20on%20the%203000%20port.


# Índice

* [1 Preparando el proyecto](#1-Preparando-el-proyecto)
  * [1.1 Nuestro proyecto en local](#11-Nuestro-proyecto-en-local)
 

# 1 Preparando el proyecto

## 1.1 Nuestro proyecto en local

Tenemos un proyecto React listo llamado **proyecto-egator** en local en `\Users\chris\Documentos\GitHub\react\proyecto-egator` que arrancamos con:

```bash
C:\Users\chris> cd /
C:\> cd \Users\chris\Documentos\GitHub\react\proyecto-egator
C:\Users\chris\Documentos\GitHub\react\proyecto-egator>npm start
```
<br>
<br>

## 1.2 Subiendo una copia del proyecto a GitHub

1 Creamos un nuevo repositorio **react5** en GitHub y los clonamos dentro de la carpeta local `C:\GitHub`.

2 Ejecutamos `Open Git Bash Here` en la carpeta **GitHub** y `git clone https://github.com/sociologo/react5.git`

3 Copiamos el proyecto **proyecto-egator** ubicado en `C:\Users\chris\Documentos\GitHub\react\proyecto-egator` en el nuevo repositorio local, lo subimos a GitHub y lo ejecutamos desde la carpeta local para cerciorarnos de que el proyecto ejecute correctamente.

En GitHub desktop damos click a `File` y `Add local repository`. Seleccionamos el local path `C:\GitHub\react5` y damos click en `Add repository`. Hacemos el `Push origin` a GitHub.

```bash
C:\Users\chris> cd /
C:\> cd \GitHub\react5\proyecto-egator
C:\GitHub\react5\proyecto-egator> npm start
```
<br>
<br>

## Un problema

Nos encontramos con la sorpresa al subir e proyecto React completo de que se despliega en Azure solo una página en blanco. Debemos determinar en que momento se produce esto porque hasta cierto punto el despliegue se produce bien.

Construimos de nuevo la aplicacion en C:\GitHub\react6 siguiendo las instrucciones de `proyecto-egator-ejer-1.md` hasta el punto 14 incluyéndolo.

Verifiquemos que despliegue bien:

```bash
C:\Users\chris> cd /
C:\> cd \GitHub\react6\
C:\GitHub\react6> npm start
```
<br>
<br>

![image](https://github.com/user-attachments/assets/f2bcbf6f-f85b-49e7-a930-d59e7196ae9b)

![image](https://github.com/user-attachments/assets/4f779a26-b62b-46bd-8a40-f20dd3ab08e7)

Repetimos el proceso para un repositorio Github **react6**

`git clone https://github.com/sociologo/react6.git`


# 2 


# 3 Configurar un dominio personalizado existente en Azure App Service

Tengo una aplicacion React desplegada en Azure:

https://reactcuatro-d9eydxfmegezehf6.brazilsouth-01.azurewebsites.net/

![image](https://github.com/user-attachments/assets/b8a596f1-7f42-405b-bfea-3d053e875893)

1 Configurar un dominio personalizado

En Azure Portal, dirígete a la página de administración de tu aplicación.

En el menú izquierdo de tu aplicación, selecciona Dominios personalizados.

Selecciona Agregar dominio personalizado.

![image](https://github.com/user-attachments/assets/9e4bc358-7726-4c65-9f67-2bdb6ee68a30)













