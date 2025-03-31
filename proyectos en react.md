
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

Creamos un nuevo repositorio **react3** en GitHub y los clonamos en una carpeta local llamada **react3** localizada en `GitHub/`

1 Ejecutamos `Open Git Bash Here` en la carpeta **GitHub**

2 Ejecutamos `git clone https://github.com/sociologo/react3.git`

Copiamos el proyecto en el nuevo repositorio local, lo subimos a GitHub y lo ejecutamos desde la carpeta local para cerciorarnos de que el proyecto ejecute correctamente.

```bash
C:\Users\chris> cd /
C:\> cd \GitHub\react3\proyecto-egator
C:\GitHub\react3\proyecto-egator> npm start
```
<br>
<br>

## Paso 3: Implementación en la plataforma de aplicaciones de DigitalOcean


Inicie sesión en su cuenta de DigitalOcean, presione el botón "Crear" y seleccione "App platform".

A continuación, se le solicitará que vincule su repositorio de GitHub. 

![image](https://github.com/user-attachments/assets/33eac984-5bbc-43b9-917c-4b2ce6e1ce25)








Ahora que ha seleccionado su repositorio, debe configurar la aplicación DigitalOcean. En este ejemplo, el servidor estará ubicado en Norteamérica; para ello, seleccione Nueva York en el campo Región, y la rama de implementación será la principal. Para su aplicación, elija la región más cercana a su ubicación física:

En este tutorial, comprobarás los cambios de código en la implementación automática. Esto reconstruirá tu aplicación automáticamente cada vez que actualices el código.

Pulsa Siguiente para pasar a la pantalla "Configurar tu aplicación".

A continuación, selecciona el tipo de aplicación que ejecutarás. Dado que React compila recursos estáticos, selecciona "Sitio estático" en el menú desplegable del campo "Tipo".

Nota: Create React App no ​​es un generador de sitios estáticos como Gatsby, pero sí utiliza recursos estáticos, ya que el servidor no necesita ejecutar código del lado del servidor, como Ruby o PHP. La aplicación usará Node para ejecutar los pasos de instalación y compilación, pero no ejecutará el código de la aplicación en el nivel gratuito.

También tienes la opción de usar un script de compilación personalizado. En este caso, puedes usar el comando predeterminado "npm run build". Si tienes un script de compilación diferente para un entorno de control de calidad (QA) o de producción, puedes crear un script de compilación personalizado:

Pulsa Siguiente para ir a la página Finalizar e iniciar.

Aquí puedes seleccionar el plan de precios. El plan Starter gratuito está diseñado para sitios web estáticos, así que elige ese:


Presione el botón Iniciar aplicación de inicio y DigitalOcean comenzará a construir su aplicación.

La aplicación ejecutará los scripts de compilación de npm ci y npm en tu repositorio. Esto descargará todas las dependencias y creará el directorio de compilación con una versión compilada y minimizada de todos tus archivos JavaScript, HTML y otros recursos. También puedes crear un script personalizado en tu package.json y actualizar los comandos en la pestaña Componentes de tu aplicación en App Platform.

La compilación tardará unos minutos en ejecutarse, pero una vez finalizada, recibirás un mensaje de éxito y un enlace a tu nuevo sitio. El enlace tendrá un nombre único y será ligeramente diferente:


Pulsa la aplicación en vivo para acceder a tu proyecto en el navegador. Será igual que el proyecto que probaste localmente, pero estará activo en la web con una URL segura:


Ahora que tu proyecto está configurado, cada vez que realices un cambio en el repositorio vinculado, ejecutarás una nueva compilación. En este caso, si envías un cambio a la rama principal, DigitalOcean ejecutará automáticamente una nueva implementación. No es necesario iniciar sesión; se ejecutará en cuanto envíes el cambio:

Nueva implementación

En este paso, creaste una nueva aplicación de DigitalOcean en App Platform. Conectaste tu cuenta de GitHub y configuraste la aplicación para compilar la rama principal. Después de configurar la aplicación, descubriste que esta implementará una nueva compilación después de cada cambio.









