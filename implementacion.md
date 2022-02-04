# Implementación del CMS en un proyecto nuevo de Laravel

Paquete para ambiente de trabajo _Laravel_ que separa la responsabilidad de mantenimiento del _CMS_ en sitios web hechos en casa por Marival Group.

Copyright 2021 Marival Group, todos los derechos reservados.

Este proyecto no contiene licencia y, por tanto, no está permitido su uso en proyectos web externos o ajenos a Marival Group sin consentimiento expreso de los autores y/o titulares de derechos de autor.

Requisitos necesarios:
- _Laravel_ ^7.0
- _PHP_ >= 7.2.5

## Tabla de contenido

- [Instalación](#instalacin)
- [Uso](#uso)
- [Desarrollo](#desarrollo)

## Instalación

Crea un nuevo proyecto de _Laravel_ (o salta este paso si ya tienes un proyecto establecido)

```sh
composer create-project laravel/laravel <nombre del proyecto> 7.*
```

O también:

```sh
composer global require laravel/installer

laravel new <nombre del proyecto>
```

Navega al directorio creado y edita el archivo `.env` para establecer el nombre de la base de datos. El nombre de base de datos establecerá también el nombre de la conexión automáticamente:

```env
DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=<nombre de la base de datos>
DB_USERNAME=homestead
DB_PASSWORD=secret
```

Edita el archivo `composer.json` y añade las siguientes llaves (puedes omitir las que ya existan):

```javascript
"minimum-stability": "dev",
"prefer-stable" : true,
"repositories": [
    {
        "type": "vcs",
        "url":  "https://gitlab.com/marival-group/mgcms2021.git"
    }
]
```

Descarga el paquete de _CMS_:

```sh
composer require marival-group/mgcms2021
```

Es posible que, si es la primera vez que requieres una dependencia, la terminal requiera tus credenciales o un token de acceso (especialmente si en lugar de usar `HTTPS` usas `SSH`). Si el sistema solicita las credenciales, escríbelas; si ya habías generado un token anteriormente, cópialo de tu cuenta en [GitLab](https://gitlab.com/-/profile/personal_access_tokens) y pégalo en la terminal; de lo contrario, puedes seguir las instrucciones que aparecen en pantalla o entrar (con tu cuenta de Marival Group) a [GitLab](https://gitlab.com/-/profile/personal_access_tokens) y crea un nuevo token con configuración similar a esta:

![Configuración de nuevo token](./token_git.png)

Establece los valores de configuración en la caché:

```sh
php artisan config:cache
```

Ejecuta las migraciones para establecer la información necesaria en la base de datos:

```sh
php artisan MGCms2021:migrate
```

Ejecuta los semilleros para establecer la información esqueleto en la base se datos, junto con los elementos _dummy_ para creación de sitios:

```sh
php artisan MGCms2021:seed
```

Puedes ejecutar estos dos últimos pasos *juntos* con el siguiente comando:

```sh
php artisan MGCms2021:migrate-and-seed
```

En caso de requerir acceder a la información provista por los _endpoints_ desde servicios externos, será necesario crear las llaves de acceso requeridas por _Passport_ corriendo el comando:

```sh
php artisan passport:keys
```

Seguido de esto, deben darse de alta los clientes que podrán acceder. Dependiendo de la naturaleza de cada usuario (persona, máquina o intermediario), el cliente será diferente; sin embargo, como regla general, pueden clasificarse en partes:

- Primera parte: Sitios o servicios desarrollados en _Marival Group_ que consumen datos sin intervención humana y que tu departamento administra. El cliente [Client Credentials Grant](https://laravel.com/docs/5.8/passport#client-credentials-grant-tokens) es lo recomendado.
- Segunda parte: Sitios o servicios desarrollados en _Marival Group_ que consumen datos sin intervención humana y que otro departamento administra. El cliente [Password Grant](https://laravel.com/docs/5.8/passport#creating-a-password-grant-client) es lo recomendado.
- Tercera parte: Sitios o servicios desarrollados fuera de _Marival Group_ que potencialmente pueden consumir datos bajo petición humana. El cliente [Authorization Code Grant](https://laravel.com/docs/5.8/passport#issuing-access-tokens) es lo recomendado.

Para información acerca de la creación de clientes, refiérase a la documentación de [Passport](https://laravel.com/docs/5.8/passport)

¡Está listo!, ahora puedes acceder al _CMS_ (Accediendo a `<dominio>/admin/`).

### Errores conocidos

- _GenericUser::hasRole_: El archivo `config/auth.php` del proyecto *puede ser eliminado* o, en su defecto, modificar los índices `guards`, `providers` y `passwords`  de la siguiente manera:

```php
'guards' => [
    'web' => [
        'driver' => 'session',
        'provider' => 'users',
    ],
    'api' => [
        'driver' => 'passport',
        'provider' => 'api_consumers',
        'hash' => false,
    ],
    ...
],
...
'providers' => [
    'users' => [
        'driver' => 'eloquent',
        'model' => AvengersMG\MGCms2021\app\Cms\Users\User::class,
    ],
    'api_consumers' => [
        'driver' => 'eloquent',
        'model' => AvengersMG\MGCms2021\app\Cms\ApiConsumers\ApiConsumer::class,
    ],
    ...
],
...
'passwords' => [
    'users' => [
        'provider' => 'users',
        'table' => 'password_resets',
        'expire' => 60,
    ],
    'api_consumers' => [
        'provider' => 'api_consumers',
        'table' => 'password_resets',
        'expire' => 60,
    ],
    ...
],
```

Recuerde que, después de cualquier modificación a archivos en el directorio `config`, el siguiente comando debe ser ejecutado:

```sh
php artisan config:cache
```

## Uso

### Configuraciones personalizadas

Cada proyecto deberá tener sus propias configuraciones (especialmente credenciales de servicios como _PriceTravel_ o direcciones de blogs), por lo que es necesario ejecutar el siguiente comando para publicar el archivo de constantes al proyecto (`config/constants.php`):

```sh
php artisan vendor:publish --tag=constants
```

Adicionalmente, dentro del archivo `.env` del proyecto, será necesario crear nuevas entradas para _Google reCAPTCHA_: `GOOGLE_RECAPTCHA_SITE_KEY`, que contenga la llave pública, y `GOOGLE_RECAPTCHA_SITE_KEY`, que contenga la llave privada para verificación.

Cada vez que los archivos `constants.php` o `.env` sean modificados, el siguiente comando debe ser ejecutado para guardar la información en la caché:

```sh
php artisan config:cache
```

### Imágenes para reseñas
Las imágenes que se quieran usar para seleccionar el logo de la empresa de donde proviene la reseña debe colocarse en el directorio `public/images/reviews` del proyecto de _Laravel_. 

![Configuración de nuevo token](./reviews_folder.png)![Configuración de nuevo token](./reviewsform.png)

Los archivos colocados en el directorio `reviews` aparecerán en el listado de selección de _avatar_.

### Recursos públicos

Ya no es necesaria la recompilación de los recursos del _CMS_, por lo que el archivo `webpack.min.js` en la raíz del proyecto sólo deberá compilar recursos del sitio creado.

Los recursos para compilar (_resources_) que cada sitio deberá usar (_scripts_ y estilos) deberán ser ubicados en el directorio `resources`, siguiendo el estándar siguiente: `resources/assets/<nombre del proyecto>/`.

*NOTA:* _2019-04-17_ - Debido a la naturaleza de desarrollo continuo, la carpeta `lang` sigue siendo utilizada en todos los proyectos que el sistema posea.

### Estilos o scripts personalizados

En caso de requerir añadir funciones, estilos, imágenes u otros recursos especiales para el proyecto, los cuales no serán compartidos por otros, es posible publicar los recursos del _CMS_ utilizando el siguiente comando:

```sh
php artisan vendor:publish --tag=public
```

Al ejecutar, los recursos serán copiados al directorio `public/cms`. Estos recursos tomarán prioridad a los recursos usados por el paquete.

Adicionalmente, la bandera `--tag` puede ser cambiada para publicar archivos de configuración, que serán copiados al directorio apropiado del proyecto. Lo siguientes valores son válidos:

- `public`: Recursos públicos del _CMS_ (`public/cms/`)
- `frontend`: Archivos dummy de _layouts_ y _templates_ para el frente (directorios `emails`, `templates`, `partials` y `layouts` en `resources/views/`)
- `auth`: Configuración de guardias y motores de autenticación (`config/auth.php`)
- `constants`: Configuración de constantes internas de proyecto (`config/constants.php`)
- `database`: Configuración de conexiones y bases de datos (`config/database.php`)
- `services`: Configuración de servicios generales (`config/services.php`)
- `translatable`: Configuración del servicio _Translatable_ (`config/translatable.php`)
- `breadcrumbs`: Configuración del servicio _Breadcrumbs_ (`config/breadcrumbs.php`)
- `filesystems`: Configuración de sistema de archivos (`config/filesystems.php`)

Es recomendado que, después de publicar recursos de configuración, sea ejecutado el siguiente comando para recargar la caché:

```sh
php artisan config:cache
```

### Configuración de itinerario

Algunas funciones del sistema están configuradas para correr de forma desatendida. Para poder habilitar estas características, es necesario establecer en el servidor un archivo de itinerario (típicamente un _Cron Job_) para que ejecute de acuerdo con la fecha y hora.

En el servidor de despliegue, incluya una configuración que ejecute *cada minuto* el comando de navegación al directorio donde reside el archivo `artisan`, seguido del comando de ejecución de itinerarios:

Un _Cron Job_ puede ser establecido con la siguiente configuración:

```sh
* * * * * cd <ruta absoluta al directorio donde reside `artisan`> && php artisan schedule:run >> /dev/null 2>&1
```

Este _Cron Job_ representa una ejecución de cada minuto del comando de navegación, seguido del comando de itinerario (dependiente del de navegación) donde la salida es desechada y no son generados mensajes de correo electrónico para el usuario solicitante (típicamente `root`).

### API para consumidores

Los recursos del proyecto pueden ser consumidos por aplicaciones terceras con el uso del paquete `laravel/passport`, del cual este paquete depende.

El paquete viene configurado con _endpoints_ por defecto, los cuales son protegidos por autenticación por token usando el flujo _Client Credentials Grant_ de _OAuth2.0_:

- `GET:find-rooms-price`: Solicitud de precio de habitación.
  - `<string:language>`: Identificador de lenguaje (Ej.: "es", "en"...)
- `GET:total-blackout-dates`: Fechas en que el hotel no tiene habitaciones disponibles.
  - `<string:language>`: Identificador de lenguaje (Ej.: "es", "en"...)
- `GET:specials`: Especiales activos en el hotel.
  - `<string:language>`: Identificador de lenguaje (Ej.: "es", "en"...)
- `GET:special`: Especial específico activo en el hotel.
  - `<string:language>`: Identificador de lenguaje (Ej.: "es", "en"...)
  - `<string:slug>`: Identificador del especial (Ej.: "up-to-3-kids-for-free")
- `GET:restaurants`: Restaurantes publicados en el hotel.
  - `<string:language>`: Identificador de lenguaje (Ej.: "es", "en"...)
- `GET:rooms`: Habitaciones publicadas en el hotel.
  - `<string:language>`: Identificador de lenguaje (Ej.: "es", "en"...)
- `GET:pages/multiple`: Páginas publicadas en el hotel, las cuales coincidan con un arreglo de permalinks.
  - `<string:language>`: Identificador de lenguaje (Ej.: "es", "en"...)
  - `<string[]:permalinks>`: Arreglo de permalinks (Ej.: \["/es/especiales"\]...)

Para mayor información sobre el uso de API y _OAuth2.0_, refiérase al repositorio de [Passport](https://github.com/laravel/passport)

### Uso avanzado

El paquete incluye comandos adicionales para realizar otras funciones. Ejecuta el siguiente comando para listarlos (estarán bajo el encabezado `MGCms2021`):

```sh
php artisan list
```

## Desarrollo

### Clonado

Clona el repositorio a una ubicación en tu computadora:

```sh
git clone git@gitlab.com:marival-group/mgcms2021.git
```

En terminal, navega al directorio del repositorio y descarga las dependencias necesarias:

```sh
composer install
npm install
```

Para compilar los nuevos cambios en el paquete, ejecuta el siguiente comando en el directorio del repositorio:

```sh
npm run dev
```
### Ambiente de Desarrollo

Puedes usar instalaciones existentes y nuevas de _Laravel_ para desarrollar, pero deberás eliminar la dependencia, si es que está instalada, con el siguiente comando:

```sh
composer remove avengersmg/mgcms_2021
```

Edita el archivo `composer.json` y añade las siguientes llaves (puedes omitir las que ya existan):

```javascript
"minimum-stability": "dev",
"prefer-stable" : true,
"repositories": [
        {
                "type": "path",
                "url": "<dirección al repositorio clonado>",
                "options": {
                        "symlink": true
                }
        }
]
```

Actualiza las dependencias y elimina la caché con el siguiente comando:

```sh
composer clear-cache
composer require avengersmg/mgcms_2021
php artisan MGCms2021:flush
```

De esta forma, ya será posible editar desde el repositorio o desde el directorio `vendor` de la instalación de _Laravel_.

*NOTA:* Si la consola arroja errores sobre configuraciones o repositorios faltantes, elimina todos los archivos dentro de la carpeta `bootstrap/cache` y vuelve a correr los comandos anteriores.
