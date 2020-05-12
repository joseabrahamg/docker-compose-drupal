# Plantilla de Docker Compose para Drupal 8 :whale: :droplet:

Este repositorio contiene una plantilla de **Docker Compose** para desplegar un entorno de desarrollo para instalar drupal

La plantilla de **Docker Compose** tiene definida una red _(net)_ y tres (3) servicios: 
> 1. Contenedor para bases de datos: MySQL
> 2. Contenedor para servidor web: Apache
> 3. Contenedor para pruebas de correos electrónicos: MailHog

## Comenzando 🚀

En la carpeta donde quieras descargarlo, haz un **git clone**, de la siguiente forma: (ssh/https)

```
git clone git@github.com:joseabrahamg/docker-compose-drupal.git
```
o
```
git clone https://github.com/joseabrahamg/docker-compose-drupal.git
```

### Pre-requisitos 📋

1. Git
2. Docker
3. Docker Compose
4. Composer _(Opcional)_

### Instalación 🔧

Luego de clonar el repositorio, duplicamos el fichero ```.env.example``` y lo renombramos a ```.env``` 

Posteriormente editamos el fichero ```.env``` donde vamos a establecer los valores para las variables de entorno de proyecto que vamos a crear, las variables son las siguientes:

| Nº | Variable | Descripción |
| - | - | - |
| 1 | IP | Dirección IP |
| 2 | MYSQL_ROOT_PASSWORD | Contraseña para el usuario root de MySQL |
| 3 | MYSQL_PORT | Puerto del MySQL |
| 4 | VIRTUAL_HOST | Virtual host |
| 5 | APP_PATH | Ruta local de la aplicación mapeada en el contenedor de Docker |
| 6 | APP_PORT | Puerto del contenedor de la aplicación |
| 7 | NAME | Nombre del proyecto |

Finalmente ejecutamos el ```docker-compose``` con la opción ```build``` para desplegar el proyecto, ejemplo:

```
docker-compose up --build
```

### Probando el entorno ⚙️

Para comprobar que se han levantado los tres contenedores ejecutamos ```docker ps``` y se nos mostrará un listado con los contenedores activos.

### Instalando Drupal 8 :droplet:

Para instalar drupal tenemos dos opciones, te las describimos con mas detalles en ```/drupal/readme.md```

## Construido con 🛠️
* :whale: [Docker](https://www.docker.com/) - Build, Ship and Run. Any application, Anywhere.
* :elephant: [PHP](https://www.php.net/) - PHP powers everything from your blog to the most popular websites in the world.
* :droplet: [Drupal](https://www.drupal.org/) - It's used to make many of the websites and applications you use every day.
* :ok_woman: [Composer](https://getcomposer.org/) - A Dependency Manager for PHP.
* :large_orange_diamond: [Git](https://git-scm.com/) - Distributed version control system.
* :octocat: [GitHub](https://github.com/) - The world's leading software development platform.

## Autor ✒️

*  **José Abraham Gómez** - [:link: GitHub](https://github.com/joseabrahamg) - [:link: LinkedIn](https://www.linkedin.com/in/joseabrahamg/)
[![José Abraham Gómez](https://avatars1.githubusercontent.com/u/35762223?s=60&u=40906d85e27026c3586a769e0d036decd1ae36e5&v=4 "LinkedIn @joseabrahamg")](https://www.linkedin.com/in/joseabrahamg/)

## Expresiones de Gratitud 🎁

* Comenta a otros sobre este proyecto 📢
* Invita una cerveza 🍺 o un café ☕ a alguien del equipo. 
* Da las gracias públicamente 🤓.

---
:page_facing_up: ```readme.md``` inspirado en [Andrés Villanueva](https://github.com/Villanuevand)
