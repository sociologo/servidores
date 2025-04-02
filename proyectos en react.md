https://www.csharp.com/article/deploy-reactjs-app-to-azure-app-service-from-vs-code/#:~:text=Open%20Visual%20Studio%20Code%20and,running%20on%20the%203000%20port.

Implementar una aplicación web de Node.js en Azure\
https://learn.microsoft.com/es-mx/azure/app-service/quickstart-nodejs?tabs=windows&pivots=development-environment-vscode

# Índice

* [1 Preparando el proyecto](#1-Preparando-el-proyecto)
  * [1.1 Nuestro proyecto en local](#11-Nuestro-proyecto-en-local)

***
***

1 Una App

Construímos una App React básica y el archivo `build`:

```bash
C:\Users\chris> cd /
C:\> cd \GitHub\
C:\GitHub> npx create-react-app react10
# (no hay que construir la carpeta pues se crea sola)
C:\GitHub> cd react10
C:\GitHub\react10> npm start
C:\GitHub\react10> npm run build
```

2 Subir la App a GitHub

para subir tu repo local a GitHub:

En GitHub desktop damos click a `File` y `Add local repository`. Seleccionamos el local path `C:\GitHub\react10` y damos click en `Add repository`. Hacemos click en `Publish repository`.

Para hacer push desde local:

```bash
$ git add .
$ git commit -m "Tu mensaje aquí"
$ git push origin main
```
***
***

# Intentamos subir nuestra App React en Azure pero es un recurso caro. De todas maneras debe saber como hacerlo. Lo unico importante es crear una App Azure con una Suscripcion y un grupo de recursos creado por usted.

# Creamos un App Platform en DigitalOcean

1 Conectamos el repositorio con Autodeploy

![image](https://github.com/user-attachments/assets/ae00f426-686b-4887-9891-069bcc2d824f)

2 Establecemos como tipo de recurso `Static Site`

![image](https://github.com/user-attachments/assets/669d133c-03cb-4dea-865d-4bdca38d9e8b)

<br>
<br>















