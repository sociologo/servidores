# Implementar una aplicación web Django en Digital Ocean

***
***
Deploy a Django web app to Digital Ocean
https://www.youtube.com/watch?v=gKlsuUhfSpo

# Índice

* [1 La vista ListView](#1-La-vista-ListView)
  * [a Listar todos los empleados](#a-Listar-todos-los-empleados)

# 1 Preparamos nuestro proyecto

1 Tenemos ya listo un proyecto django conectado a postgres en local el cual arrancamos con:

```
C:\Users\chris> cd /
C:\> cd mis_entornos/entorno_3/Scripts
C:\mis_entornos\entorno_3\Scripts> activate
(entorno_3) C:\mis_proyectos\emp3\empleado>cd \Users\chris\Documentos\GitHub\django\emp3\empleado
(entorno_3) C:\Users\chris\Documentos\GitHub\django\emp3\empleado>python manage.py runserver
```

2 Instalamos Gunicorn

```
(entorno_3) C:\mis_proyectos\emp3\empleado>pip install gunicorn
```

3 En nuestra aplicacion creamos un archivo requirements.txt

El cual automaticamente nos carga todos los paquetes y dependencias que tenemos asociados a nuestro proyecto:

```
(entorno_3) C:\Users\chris\Documentos\GitHub\django\emp3\empleado>pip freeze > requirements.txt
```

```
asgiref==3.8.1
Django==5.1.6
django-ckeditor==6.7.2
django-js-asset==3.0.1
gunicorn==23.0.0
packaging==24.2
pillow==11.1.0
psycopg2==2.9.10
psycopg2-binary==2.9.10
sqlparse==0.5.3
tzdata==2025.1
```

4 Preparamos nuestros archivos estaticos.

Para ello vamos al archivo **local.py** de **settings**

El original es:
```
from .base import *

DEBUG = True

ALLOWED_HOSTS = []

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

STATIC_URL = 'static/'

STATICFILES_DIRS = [
   BASE_DIR / "static",
]

MEDIA_URL = '/media/'
MEDIA_ROOT = BASE_DIR / 'media'
```

debemos agregar STATIC_ROOT importando os, cambiar DEBUG a False, agregar un ALLOWED_HOST '*'

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

STATIC_URL = 'static/'

STATIC_ROOT = os.path.join(BASE_DIR, 'staticfiles')

STATICFILES_DIRS = [
   BASE_DIR / "static",
]

MEDIA_URL = '/media/'
MEDIA_ROOT = BASE_DIR / 'media'
```

5 SECRET_KEY

Vamos a nuestro archivo **base.py** de **settings**

Copiemos SECRET_KEY y la guardamos y hacemos el siguiente reemplazo en el archivo **base.py**:
SECRET_KEY = 'django-insecure-9xh%=ob5sj*g*r5&ii^r$mu9bs0w*t09ni*vko67=*z402som8'

```
import os

# some code

SECRET_KEY = os.environ.get('SECRET_KEY')

# some code
```

# 2 Lo subimos a Github

# 3 Configuramos DigitalOcean

Vamos a https://cloud.digitalocean.com/apps

Donde iremos a App platform y no a droplet

![image](https://github.com/user-attachments/assets/9e4f2efa-c840-4261-a7c5-99401295d09d)


Vamos a crear app y conectamos nuestro repositorio Github

Resulta clave indicar la ruta en la estructura del directorio:

![image](https://github.com/user-attachments/assets/8397e822-0638-4beb-a49e-43256e209b4e)

![image](https://github.com/user-attachments/assets/89a821f3-4662-49b8-a367-cbcc49aa74b0)
















## a Listar todos los empleados






