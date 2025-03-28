# Implementar una aplicación Django en Digital Ocean como APP

***
***
Deploy a Django web app to Digital Ocean\
https://www.youtube.com/watch?v=gKlsuUhfSpo

How To Deploy a Django App on App Platform\
https://www.digitalocean.com/community/tutorials/how-to-deploy-django-to-app-platform

# Índice

* [1 Preparando el proyecto](#1-Preparando-el-proyecto)
  * [1.1 Nuestro proyecto en local](#11-Nuestro-proyecto-en-local)
* [2 Configurando el proyecto](#2-Configurando-el-proyecto)
* [3 Configuración en DigitalOcean](#3-Configuración-en-DigitalOcean)
* [4 Cargando los archivos estáticos](#4-Cargando-los-archivos-estáticos)
* [5 Creación de y conexión a la base de datos Postgres](#5-Creación-de-y-conexión-a-la-base-de-datos-Postgres)




# 1 Preparando el proyecto

## 1.1 Nuestro proyecto en local

Tenemos un proyecto django listo llamado **empleado** conectado a postgres en local en `C:\GitHub\django\emp3\empleado` que arrancamos con:

```bash
C:\Users\chris> cd /
C:\> cd mis_entornos/entorno_3/Scripts
C:\mis_entornos\entorno_3\Scripts> activate
(entorno_3) C:\mis_entornos\entorno_3\Scripts> cd \GitHub\django\emp3\empleado
(entorno_3) C:\GitHub\django\emp3\empleado> python manage.py runserver
```

<br>
<br>

<p align="center">
  <img src="https://github.com/user-attachments/assets/5cfed8aa-2168-4a66-8c62-07fad3823aeb" alt="image" width="60%">
</p>

2 Creamos un nuevo repositorio **emp3** en GitHub y los clonamos en la carpeta local **emp3** localizada en `GitHub/`

1 Ejecutamos `Open Git Bash Here` en la carpeta **GitHub**

2 Ejecutamos `git clone https://github.com/sociologo/emp3.git`

![image](https://github.com/user-attachments/assets/35b683ac-44ef-413a-b969-54ff4b9836b6)

3 Copiamos el proyecto en un nuevo repositorio local, lo subimos a GitHub y lo ejecutamos desde la carpeta  local para cerciorarnos de que el proyecto ejecute correctamente.

<p align="center">
  <img src="https://github.com/user-attachments/assets/802bfe61-0a42-40e4-9095-1ced14c2279b" alt="image" width="60%">
</p>

```bash
C:\Users\chris> cd /
C:\> cd mis_entornos/entorno_3/Scripts
C:\mis_entornos\entorno_3\Scripts> activate
(entorno_3) C:\mis_entornos\entorno_3\Scripts> cd \GitHub\emp3\emp3\empleado
(entorno_3) C:\GitHub\emp3\empleado> python manage.py runserver
```

# 2 Configurando el proyecto

21 Instalamos Gunicorn

Es necesario para incluir Gunicorn dentro del archivo requirements.txt

Lo hacemos para asegurarnos de que nuestra aplicacion Django sea capaz de comunicarse con los servidores que trabajan tras bambalinas en DigitalOcean.

```
(entorno_3) C:\GitHub\emp3\emp3\empleado>pip install gunicorn
Requirement already satisfied: gunicorn in c:\mis_entornos\entorno_3\lib\site-packages (23.0.0)
Requirement already satisfied: packaging in c:\mis_entornos\entorno_3\lib\site-packages (from gunicorn) (24.2)
```

22 En nuestra aplicación creamos un archivo requirements.txt

Es necesario incluir un archivo requirements.txt en tu proyecto Django antes de subirlo a DigitalOcean App Platform. Este archivo le indica a la plataforma qué dependencias necesita instalar para ejecutar tu proyecto.

```
(entorno_3) C:\GitHub\emp3\emp3\empleado>pip freeze > requirements.txt
```

![image](https://github.com/user-attachments/assets/5e7955ca-2920-46ef-838f-4156cf5d5bb5)

23 Preparamos nuestros archivos estaticos.

Para ello vamos al archivo **local.py** de **settings**

debemos agregar STATIC_ROOT importando os, cambiar DEBUG a False y agregar un ALLOWED_HOST '*'

STATIC_URL: Define el prefijo de URL para acceder a tus archivos estáticos.

STATIC_ROOT: Es el directorio donde Django recopila todos los archivos estáticos al ejecutar collectstatic. **Definirlo es esencial para entornos de producción**.

STATICFILES_DIRS: Especifica directorios adicionales para tus archivos estáticos durante el desarrollo. 

`STATIC_ROOT = os.path.join(BASE_DIR, 'staticfiles')` define que todos los archivos estáticos se recopilarán y almacenarán en la carpeta staticfiles ubicada dentro del directorio raíz del proyecto. Es útil para manejar archivos estáticos en producción, cuando necesitas tenerlos organizados y listos para ser servidos por el servidor web.


```
import os

from .base import *

DEBUG = False
ALLOWED_HOSTS = ['*']

DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.postgresql_psycopg2',
        'NAME': 'dbempleado101',
        'USER': 'chris101',
        'PASSWORD': 'nueva123456',
        'HOST': 'localhost',
        'PORT': '5432'
    }
}

STATIC_URL = '/static/'

STATIC_ROOT = BASE_DIR / "staticfiles"

STATICFILES_DIRS = [
   BASE_DIR / "static",
]

MEDIA_URL = '/media/'
MEDIA_ROOT = BASE_DIR / 'media'
```

Ejecuta el comando collectstatic

Antes de desplegar la aplicación, asegúrate de ejecutar este comando en tu entorno local para recopilar los archivos estáticos:

```bash
python manage.py collectstatic --no-input
```

Este comando moverá todos los archivos estáticos al directorio definido en STATIC_ROOT.

Actualiza tu repositorio en GitHub

24 SECRET_KEY

Debemos sacar el valor en duro de SECRET_KEY, valor que vamos a ingresar como variable de entorno en nuestro servidor.

Vamos a nuestro archivo **base.py** de **settings**

en **base.py** copiemos SECRET_KEY y la guardamos y hacemos el siguiente reemplazo en el archivo **base.py**:

SECRET_KEY = 'django-insecure-9xh%=ob5sj*g*r5&ii^r$mu9bs0w*t09ni*vko67=*z402som8'

```
import os

# some code

SECRET_KEY = os.environ.get('SECRET_KEY')

# some code
```

# 3 Configuración en DigitalOcean

31 Vamos a la página `https://cloud.digitalocean.com/apps`

<p align="center">
  <img src="https://github.com/user-attachments/assets/7d4ffa5a-f6dd-4c1e-a6c3-0690666a3094" alt="image" width="60%">
</p>

32 Damos click a Create App con proveedor de código fuente GitHub

33 Conectamos con el repositorio GitHub y seleccionamos **autodeploy** para que cada cambio en el repositorio se actualice automáticamente en el servidor

<p align="center">
  <img src="https://github.com/user-attachments/assets/a4f4417d-2c3e-4944-9825-aef3fc98f9d6" alt="image" width="60%">
</p>


34 Renombramos al aplicación y seleccionamos los recursos mas baratos

<p align="center">
  <img src="https://github.com/user-attachments/assets/ef720672-ef3a-4a14-9789-d215b411879b" alt="image" width="60%">
</p>

35 Observemos el Run Command que se carga en forma automática:

![image](https://github.com/user-attachments/assets/3354cc89-ef8d-441f-9194-00c630503d82)

36 Configuramos como variables de entorno Secret Key sin comillas y la encriptamos   el archivo desde el cual queremos que arranque la aplicación:

<p align="center">
  <img src="https://github.com/user-attachments/assets/d4739be0-411a-4b5f-8bbc-38ff7013f8b5" alt="image" width="60%">
</p>

`DJANGO_SETTINGS_MODULE = empleado.settings.local`

37 Le damos un nombre a la app y creamos la aplicacion con `Create App`

<p align="center">
  <img src="https://github.com/user-attachments/assets/ce891684-f698-4fec-a833-d9a7652c075f" alt="image" width="60%">
</p>

Y llegamos a 

<p align="center">
  <img src="https://github.com/user-attachments/assets/8a6b6edb-6edf-44f4-8c8c-ada510de02be" alt="image" width="60%">
</p>

# 4 Cargando los archivos estáticos

1 Agregamos un recurso desde el código fuente
<p align="center">
  <img src="https://github.com/user-attachments/assets/62b1258f-7e45-4d84-b078-6f9b43eec357" alt="image" width="60%">
</p>


2 Apuntamos al mismo repositorio con autorun y le damos a `Next`

3 Le cambiamos nombre y lo definimos como un recurso del tipo sitio estático:
<p align="center">
  <img src="https://github.com/user-attachments/assets/12ed65e4-afa2-484c-afae-f840fe110433" alt="image" width="60%">
</p>


4 Debemos establecer como directorio de salida `staticfiles` y como ruta requerida http `/static` y le damos a `Add resources`
<p align="center">
  <img src="https://github.com/user-attachments/assets/71b6e627-edf2-41a5-bc20-5cd672c4daea" alt="image" width="60%">
</p>

y nos queda:

![image](https://github.com/user-attachments/assets/f74e5364-3bca-41d9-9d48-b62ad6797321)
![image](https://github.com/user-attachments/assets/42150751-39e8-4b47-adc5-82782e10b26d)

# 5 Creación de y conexión a la base de datos Postgres

51 Agregamos a nuestra aplicación empleado-app una base de datos. DigitalOcean automáticamente nos dirigirá a la creación de una base de datos Postgres:

![image](https://github.com/user-attachments/assets/f41c3878-e487-404c-8d2c-9790c131fb56)

![image](https://github.com/user-attachments/assets/f22c274d-3707-407a-8c7a-a6c0e568f2dd)

52 Copiamos el string de conexión

![image](https://github.com/user-attachments/assets/a63c4e0d-ece7-44cb-b51d-f60fad7f889d)

53 Añadimos el string de conexión como una nueva variable de entorno encriptada de nuestra aplicación:

![image](https://github.com/user-attachments/assets/99474450-74cb-4b13-9740-cfc4ee96886c)

![image](https://github.com/user-attachments/assets/75523dfa-8f87-4b66-8c03-a0386a54adc5)

54 Modificamos el archivo **local.py** de **settings** como se indica:

```python
import os
from .base import *
from urllib.parse import urlparse

DEBUG = True
ALLOWED_HOSTS = ['*']

DATABASE_URL = os.environ.get('DATABASE_URL')

db_info = urlparse(DATABASE_URL)

DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.postgresql_psycopg2',
        'NAME': db_info.path[1:],  # Extrae el nombre de la base de datos desde la URL
        'USER': db_info.username,  # Extrae el nombre de usuario desde la URL
        'PASSWORD': db_info.password,  # Extrae la contraseña desde la URL
        'HOST': db_info.hostname,  # Extrae el host desde la URL
        'PORT': db_info.port,  # Extrae el puerto desde la URL
        'OPTIONS': {
            'sslmode': 'require',  # Asegura la conexión SSL
        },
    }
}

STATIC_URL = 'static/'

STATIC_ROOT = BASE_DIR / "staticfiles"

STATICFILES_DIRS = [
   BASE_DIR / "static",
]

MEDIA_URL = '/media/'
MEDIA_ROOT = BASE_DIR / 'media'
```

55 Actualizamos nuestro proyecto en GitHub.

logre la coneccion. lo que debo hacer ahora es en la consola de digital ocean un make migrate

56 En la consola de DigitalOcean hacemos las migraciones para construir la estructura de nuestra base de datos

python manage.py migrate

57 En la consola de DigitalOcean creamos un superusuario

python manage.py createsuperuser

y ya está.

















