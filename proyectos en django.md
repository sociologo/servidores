# Implementar una aplicación Django en Digital Ocean como APP

***
***
Deploy a Django web app to Digital Ocean\
https://www.youtube.com/watch?v=gKlsuUhfSpo

How To Deploy a Django App on App Platform\
https://www.digitalocean.com/community/tutorials/how-to-deploy-django-to-app-platform

# Índice

* [1 Preparando el proyecto](#1-Preparando-el-proyecto)
  * [11 Nuestro proyecto en local](#11-Nuestro-proyecto-en-local)
* [3 Configuración en DigitalOcean](#3-Configuración-en-DigitalOcean)


# 1 Preparando el proyecto

## 11 Nuestro proyecto en local

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

31 Vamos a la pagina `https://cloud.digitalocean.com/apps`

<p align="center">
  <img src="https://github.com/user-attachments/assets/7d4ffa5a-f6dd-4c1e-a6c3-0690666a3094" alt="image" width="60%">
</p>

32 Damos click a Create App con el proveedor de la fuente GitHub

33 Conectamos a GitHub y seleccionamos **autodeploy** para que cada cambio en el repositorio se actualice automaticamente en el servidor, 

<p align="center">
  <img src="https://github.com/user-attachments/assets/a4f4417d-2c3e-4944-9825-aef3fc98f9d6" alt="image" width="60%">
</p>


34 Renombramos al aplicación y seleccionamos los recursos mas baratos

<p align="center">
  <img src="https://github.com/user-attachments/assets/ef720672-ef3a-4a14-9789-d215b411879b" alt="image" width="60%">
</p>

35 Observemos el Run Command que se carga en forma automatica:

![image](https://github.com/user-attachments/assets/3354cc89-ef8d-441f-9194-00c630503d82)

36 Configuramos la variable de entorno que es la secret key sin comillas y la encriptamos:

<p align="center">
  <img src="https://github.com/user-attachments/assets/c17e1956-20cf-42c3-9668-1559b86ccb87" alt="image" width="60%">
</p>

Configuramos como variable de entorno el archivo desde el cual queremos que arranque la aplicacion.

DJANGO_SETTINGS_MODULE=empleado.settings.production


37 Le damos un nombre a la app y cramos la aplicacion

<p align="center">
  <img src="https://github.com/user-attachments/assets/ce891684-f698-4fec-a833-d9a7652c075f" alt="image" width="60%">
</p>





***
***
<br>
<br>
<br>
<br>

aca voy

<br>
<br>
<br>
<br>
***
***








En nuestro proyecto debemos agregar un archivo sin extension llamado Procfile a la altura del **manage.py**

```
C:\Users\chris\Documentos\GitHub\emp3\empleado>echo web: gunicorn empleado.wsgi > Procfile
```

![image](https://github.com/user-attachments/assets/0501f68d-8b8a-479f-a311-28224b613bb2)


Vamos a https://cloud.digitalocean.com/apps

Donde iremos a App platform y no a droplet

![image](https://github.com/user-attachments/assets/9e4f2efa-c840-4261-a7c5-99401295d09d)


Vamos a crear app y conectamos nuestro repositorio Github

Resulta clave indicar la ruta en la estructura del directorio:

![image](https://github.com/user-attachments/assets/8397e822-0638-4beb-a49e-43256e209b4e)

![image](https://github.com/user-attachments/assets/89a821f3-4662-49b8-a367-cbcc49aa74b0)

Y asi se ve:

![image](https://github.com/user-attachments/assets/763bf478-1111-458c-bea8-aaa1daeece4b)

![image](https://github.com/user-attachments/assets/6078a862-d0e5-4e27-b847-2232eb3d4f55)

Configuramos las variables de entorno que es la secret key sin comillas:

![image](https://github.com/user-attachments/assets/23eb1197-1068-4dae-a57c-3e79f3221ede)

![image](https://github.com/user-attachments/assets/74351d19-6c3a-4191-ba72-c4156e1aa482)


# 4 Configuramos los archivos estaticos

# 5 Construimos una base de datos

Constuimos una base de datos en postgres.

Copiamos la cadena de conexion y la asociamos a una variable de entorno que configuramos en Actions Manage env vars de la app en DigitalOcean


DATABASE_URL = postgresql://doadmin:show-password@db-postgresql-sfo3-81712-do-user-18172787-0.m.db.ondigitalocean.com:25060/defaultdb?sslmode=require

![image](https://github.com/user-attachments/assets/c0bca814-1e4a-4658-bb96-44fecea3ef50)

![image](https://github.com/user-attachments/assets/56ba4ab8-925f-4e97-b7fa-948542e69c05)

Establecemos los correctos parametros en la configuracion de nuestra base de datos postgres
```
import os
from .base import *

DEBUG = False
ALLOWED_HOSTS = ['*']

from urllib.parse import urlparse
DATABASE_URL = os.environ.get('DATABASE_URL')
db_info = urlparse(DATABASE_URL)

DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.postgresql_psycopg2',
        'NAME': 'defaultdb',
        'USER': db_info.username,
        'PASSWORD': db_info.password,
        'HOST': db_info.hostname,
        'PORT': db_info.port,
        'OPTIONS': {'sslmode': 'require'},
    }
}

STATIC_URL = 'static/'
STATIC_ROOT = os.path.join(BASE_DIR, 'staticfiles')
STATICFILES_DIRS = [
   BASE_DIR / "static",
]

MEDIA_URL = '/media/'
MEDIA_ROOT = BASE_DIR / 'media'
```


Es fundamental establecer correctamente las variables de entorno incluyendo DJANGO_SETTING_MODULE 

![image](https://github.com/user-attachments/assets/7addac5c-a8ac-427a-aee1-814b94f408c3)







## a Listar todos los empleados






