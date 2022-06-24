# Creacion de un aplicacion web con Symfony y XMAPP
#
## TECNOLOGIAS

<br>

[![Symfony](https://img.shields.io/badge/Symfony-000000?style=for-the-badge&logo=Symfony&logoColor=white)](https://symfony.com/doc/current/index.html)
[![XMAPP](https://img.shields.io/badge/Xampp-F37623?style=for-the-badge&logo=xampp&logoColor=white)](https://www.apachefriends.org/es/index.html)

#
Symfony es un framework de php que resulta de gran utilidad pues agiliza todo el proceso de la creacion de la raiz de una aplicacion web. Implementado junto a XMAPP ahorra mucho tiempo y aumenta la eficiencia.
<br>
Para instalar Symfony, son necesarios unos pasos previos

1. Instalar PHP 8.1 o posterior. Para ello:
    - [Descargar PHP](https://www.php.net/downloads) --> _Windows Download_ --> (Ultima Version) --> _Zip_
    - Descomprimir el Archivo
    - Cambiar el nombre al directorio a _php_
    - Mover el directorio _php_ a la ubicacion: __C:__ ó a __C:\Program Files__ 
    - Incluir la carpeta php en las variables de entorno
    - Nota: XAMPP incluye PHP, pero es recomendable instalarlo aparte pues sera del segundo el php.ini que editaremos para los drivers una vez queramos crear la base de datos

2. Instalar Composer
    - [Descargar Composer](https://getcomposer.org/download/) --> Descargar el ejecutable o hacerlo mediante linea de comandos

3. [Instalar Scoop](https://scoop.sh)
    - OJO: Ha de hacerse desde la PoweShell (que no es lo mismo que la CMD)

    > `Set-ExecutionPolicy RemoteSigned -Scope CurrentUser`

    > `irm get.scoop.sh | iex`

4. [Instalar Symfony CLI](https://symfony.com/download)

    > `scoop install symfony-cli`

5. Instalar XMAPP
    - [Descargar XMAPP](https://www.apachefriends.org/es/index.html) --> Instalacion normal --> next. Instalar en: __C:/__    
    - Errores que pueden darse:
        1. Error al cerrar XMAPP
            - Abrir la ubicacion del ejecutable > click derecho > Propiedades > Compatibilidad > marcar "Ejecutar este programa como Administrador"
        2. Ejecutar MySQL y Apache para poder ver este:
            - MySQL > Config > editar **my.ini**
            - Cambiar port=3306 por port=3307 --> aparece 2 veces
            - Apache > Config > editar **php.ini**
            - Cambiar port=3306 por port=3307 --> aparece 2 veces
            - Cerrar y volver a abrir XAMPP

6. Comprobacion de que todo lo que hemos instalado funciona correctamente
```
    > php -v

    > composer -v

    > scoop -v

    > symfony -v

    > Ejecutar XAMPP y abrir los servicios de 'MySQL' y 'APACHE'
```

# 

Una vez esten instaladas las tecnologias, vamos a crear el proyecto como tal.

## Pasos

[Documentacion Oficial](https://symfony.com/doc/current/doctrine.html)

1. Crear el proyecto. Tener en cuenta que ejecutar este comando creará una carpeta del nombre indicado con todos los archivos necesarios para el framework, y para la aplicacion, en su interior:

    > `symfony new project_name`

2. Para poder realizar una aplicacion web, es necesario instalar una serie de librerias. Nos dirigimos al interior del directorio del proyecto y ejecutamnos en la cmd:

    > `composer require symfony/orm-pack`

    > `composer require --dev symfony/maker-bundle`

3. El archivo **-env** habrá sido modificado. De modo que se han añadido una serie de lineas. Modificar la parte de _###> doctrine/doctrine-bundle ###_ del siguiente modo:

    - Vista Inicial:
        ````
        ###> doctrine/doctrine-bundle ###
        # Format described at https://www.doctrine-project.org/projects/doctrine-dbal/en/latest/reference/configuration.html#connecting-using-a-url
        # IMPORTANT: You MUST configure your server version, either here or in config/packages/doctrine.yaml
        #
        # DATABASE_URL="sqlite:///%kernel.project_dir%/var/data.db"
        # DATABASE_URL="mysql://db_user:db_password@127.0.0.1:3306/db_name?serverVersion=5.7&charset=utf8mb4"
        DATABASE_URL="postgresql://symfony:ChangeMe@127.0.0.1:5432/app?serverVersion=13&charset=utf8"
        ###< doctrine/doctrine-bundle ###
        ````
    - Vista Editada (Linea 8) --> # (Sustituir en linea 9) / root / 3307 / NOMBREBASEDATOS
        ````
        ###> doctrine/doctrine-bundle ###
        # Format described at https://www.doctrine-project.org/projects/doctrine-dbal/en/latest/reference/configuration.html#connecting-using-a-url
        # IMPORTANT: You MUST configure your server version, either here or in config/packages/doctrine.yaml
        #
        # DATABASE_URL="sqlite:///%kernel.project_dir%/var/data.db"
        DATABASE_URL="mysql://root@127.0.0.1:3307/NOMBREBASEDATOS?serverVersion=5.7&charset=utf8mb4"
        # DATABASE_URL="postgresql://symfony:ChangeMe@127.0.0.1:5432/app?serverVersion=13&charset=utf8"
        ###< doctrine/doctrine-bundle ###
        ````

        > El 'NOMBREBASEDATOS' será el nombre que recibira la base que crearemos a continuación
#

4. Ahora, tendriamos que crear la Base de Datos. Para ello, utilizaremos MySQL, pero la gestionaremos con PHPMyAdmin. Para la creacion de la misma base de datos: 

> `php bin/console doctrine:database:create`

y de las distintas *Entidades* y *Atributos*:

> `php bin/console make:entity`

5. Para guardar todas las novedades que hayamos hecho:

> `php bin/console make:migration`

6. Una vez hayamos creado la entidad, deberemos crear un controlador:

> `php bin/console make:controller ControllerName`


