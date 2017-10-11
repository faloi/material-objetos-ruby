# Guía rápida de Ruby on Rails

## Archivos y carpetas del proyecto

```
.
├── app                # Controladores, vistas, modelos, CSS.
├── bin            
├── config             # Rutas HTTP, configuración de la conexión a la base de datos.
├── config.ru
├── db                 # Esquema de la base de datos, migraciones.
├── Gemfile            # Dependencias (código de otras personas que nuestra aplicación usa).
├── Gemfile.lock
├── lib
├── log
├── public
├── Rakefile
├── README.md
├── test
├── tmp
└── vendor
```

|Carpeta|Objetivo|
|-------|--------|
|_app/assets/images_        |Contiene las imágenes.|
|_app/assets/stylesheets_   |Contiene una hoja de estilos CSS por cada modelo.|
|_app/controllers_          |Contiene un archivo por cada controlador. En él se especificarán las acciones que pueden realizarse, y que corresponden a los distintos verbos HTTP.|
|_app/models_               |Contiene una clase de Ruby por cada modelo. Los atributos se toman del esquema de la base de datos, en esta clase solo pondremos los métodos que queremos que tengan nuestros objetos.|
|_app/views_                |Contiene una carpeta por cada modelo, y dentro de ella un archivo HTML ERB por cada vista.|
|_config/routes.rb_         |Aquí se especifican las rutas, típicamente mediante `resources`, o recursos.|
|_db/schema.rb_             |Es el esquema de datos, que creará tanto las tablas en la base de datos como los atributos, getters y setters de los objetos del modelo.|


## Rutas y acciones habituales

Rails está preparado para manejar por defecto ciertas rutas, que nos permitirán realizar las acciones habituales: crear, ver, modificar, borrar; o _CRUD_ (del inglés create, read, update, delete). 

Suponiendo que agregamos un recurso llamado `personajes`, las rutas y acciones que Rails puede manejar por defecto serían las siguientes:

|Verbo HTTP|Ruta|Método|Vista|Se usa para...|
|----------|----|------|-----|--------------|
|GET        |`/personajes`            |index       |`index.html.erb` |Muestra un HTML con todos los personajes.|
|GET        |`/personajes/new`        |new         |`new.html.erb`   |Muestra un HTML para crear un nuevo personaje.|
|POST       |`/personajes`            |create      |(no tiene)       |Crea un nuevo personaje.|
|GET        |`/personajes/:id`        |show        |`show.html.erb`  |Muestra un HTML con los datos del personaje con el `id` elegido.|
|GET        |`/personajes/:id/edit`   |edit        |`edit.html.erb`  |Muestra un HTML para editar el personaje con el `id` elegido.|
|PATCH/PUT  |`/personajes/:id`        |update      |(no tiene)       |Actualiza el personaje con el `id` elegido.|
|DELETE     |`/personajes/:id`        |destroy     |(no tiene)       |Borra el personaje con el `id` elegido.|

## Creando un modelo

Podemos crear nuevos modelos desde la consola, ejecutando un comando que trae Rails. Si quisieramos, por ejemplo, crear un Personaje con los atributos nombre, biografia, edad, fecha_nacimiento y usa_capa, correríamos el siguiente comando:

```bash
rails g model Personaje nombre:string biografia:text edad:integer fecha_nacimiento:date usa_capa:boolean
```

Al correr ese comando se generan varios archivos, pero solo nos centraremos en dos:

Una **clase**, como las que veníamos trabajando pero con un poco más de magia. Van a ver que no están los atributos y que hay varios métodos que "aparecen" y nos sirven para interactuar con la base de datos. Este archivo se crea en la carpeta `app/models`, con el nombre que hayamos puesto, en este caso `personaje.rb`.

Una **migración** para la base de datos, que se encargará de correr los comandos necesarios para modificar el esquema, agregando las tablas y columnas que sean necesarias. Este archivo se crea en la carpeta `db/migrate`, con un nombre que incluye la fecha y hora del momento en que se creó, seguido de la acción que realizará cuando se ejecute. Por ejemplo: `20170927183702_create_personajes.rb`, si lo hubieramos creado el 27/09/2017 a las 18:37:02hs.

Para que este cambio se haga efectivo, debemos correr las migraciones con el siguiente comando:

```bash
rake db:migrate
```

Como se ve en el ejemplo, el comando `rails g model` toma varios parámetros:

* El nombre del modelo, en este caso `Personaje`. Debe comenzar con mayúscula y estar en singular.
* Cada uno de los atributos que va a tener este modelo, por ejemplo `edad:integer`. Se escribe primero el nombre del atributo, en este caso `edad` y luego el tipo de datos, `integer` en este caso. En la tabla de abajo se ven los tipos de datos existentes.

|Tipo|Explicación|
|----------|----|
|`string`      |Texto corto, como un nombre o un título.|
|`text`        |Texto largo, como una biografía o el contenido de una publicación.|
|`integer`     |Números enteros (sin coma).|
|`float`       |Números con decimales (con coma).|
|`boolean`     |Verdadero o falso.|
|`datetime`    |Fecha y hora.|
|`date`        |Solo fecha.|
|`time`        |Solo hora.|

<center>
<small>
<p>
![](https://i.creativecommons.org/l/by-sa/4.0/88x31.png)    
Material elaborado por Federico Aloi, distribuido bajo los términos de la [Licencia Creative Commons Atribución-CompartirIgual 4.0 Internacional](http://creativecommons.org/licenses/by-sa/4.0/), basado parcialmente en la versión en español de las guías del sitio RailsGuides, distribuidas bajo la misma licencia y disponibles en http://www.guiasrails.es/getting_started.html.
</p>
</small>
</center>