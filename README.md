Hola buen día, espero que todo esté bien.
En este espacio explicaré como fue realizada la API, primero que todo se leyó el requerimiento para poderlo comprender, después de eso pasé a modelar la base de datos (la encontrarán adjunto)
así fue como la comprendí y como realicé todo el maquetado de la api.
Al momento de haber modelado la base de datos, instalé los programas para poder crear la API y los clientes, los programas que usé fueron: XAMPP para PHP, apache y uso de virtualhosts, Visual Studio Code,
NodeJs para usar npm, composer, consola git bash, para el maquetado de la base de datos usé MySQL Workbench y por último Laravel.

Lo siguiente que hice fue crear el proyecto de laravel con el nombre api.rick-morty, mientras se instalaba, modifiqué el archivo hosts que se encuentra en la ruta C:\Windows\System32\drivers\etc\hosts
en este archivo modifiqué el host para poder acceder por medio de una url específica para cada proyecto, las que se requieren para usar esta api, al igual que los clientes son los siguentes:

127.0.0.1       api.rick-morty.test
127.0.0.1       client1.rick-morty.test
127.0.0.1       client2.rick-morty.test

Después de eso nos vamos a la ruta de virtualhost de apache para que la redirección funcione correctamente, el archivo que vamos a modificar es el siguiente C:\xampp\apache\conf\extra\httpd-vhosts.conf
acá se agregaron las siguientes líneas de código
<VirtualHost *>
	DocumentRoot "C:\xampp\htdocs"
	ServerName localhost
</virtualHost>
Nota: si ya tenías creados virtualhosts en xampp, no es necesario escribir nuevamente el anterior código.
<VirtualHost *>
	DocumentRoot "C:\xampp\htdocs\api.rick-morty\public"
	ServerName api.rick-morty.test
	<Directory "C:\xampp\htdocs\api.rick-morty\public ">
		Options All
		AllowOverride All
		Require all granted
	</Directory>
</VirtualHost>

<VirtualHost *>
	DocumentRoot "C:\xampp\htdocs\client1.rick-morty\public"
	ServerName client1.rick-morty.test
	<Directory "C:\xampp\htdocs\client1.rick-morty\public ">
		Options All
		AllowOverride All
		Require all granted
	</Directory>
</VirtualHost>

<VirtualHost *>
	DocumentRoot "C:\xampp\htdocs\client2.rick-morty\public"
	ServerName client2.rick-morty.test
	<Directory "C:\xampp\htdocs\client2.rick-morty\public ">
		Options All
		AllowOverride All
		Require all granted
	</Directory>
</VirtualHost>

Nota: Los tres proyectos se están ejecutando con bases de datos SQLITE

IMPORTANTE: Recuerda que debes descomprimir la base de datos en la carpeta database de cada uno de los proyectos, además el ".env.example" debemos quitarle el nombre ".example" en cada uno de los proyectos para que la aplicación no te genere error. Quizá te pueda a llegar a dar un error de sesión, ese error se soluciona ejecutando la siguente línea de comando php artisan config:cache

Esos son los tres virtualhost que necesitamos para poder ejecutar correctamente la API y sus clientes.
Nota: Es importante que la carpetas llamadas api.rick-morty, client1.rick-morty y client2.rick-morty estén en la carpeta htdocs de xampp

Ahora nos redirigimos a la carpeta de cada uno de los proyectos o a los proyectos que vamos a usar y con la consola de git bash vamos a ejecutar el siguiente comando


npm run dev

Esto debemos hacerlo para que el front de la api y de los clientes se ejecuten correctamente

En el proyecto api.rick-morty se encuentra todo el CRUD para las tablas characters, episodes y locations, con sus respectivas llaves

Nota: para la API se usó Laravel Passport, por ende se crearon dos clientes para facilitarte la vida ¿por qué dos clientes?
porque uno esta accediendo por medio de grant_type authorization_code(client2) y otro por password(client1)

puedes acceder a cualquiera de los dos clientes, en los dos se encuentra el CRUD para las tres tablas.

recuerda antes de ingresar a la url de la aplicación ejecutar el comando npm run dev, si te registraste en api.rick-morty.test no es necesario registrarte en client1.rick-morty.test
ya que client1 hace peticiones de login y register a la API pero si vas a trabajar con client2.rick-morty.test si es necesario que te registres nuevamente ya que client2 trabaja 
con su propia base de datos.

Si accedes a client2 debes solicitar permisos a la api con el botón que te aparece en el dashboard y si quieres usar el CRUD, debes autorizar.

Ya para hacer uso de los CRUD, las aplicaciones son muy intuitivas, cuando ingreses al dashboard de alguno de los dos clientes, en la parte de tu nombre está el menú
y en ese menú se encuentran todos los crud de Ubicaciones, Episodios y personajes, ya solo faltaría que explores el cliente y crees, verifiques, actualices y borres registros a tu gusto.

Para poder acceder al los CRUD, debemos usar las siguientes rutas

Los campos requeridos para la tabla locations son: name, type, dimension, slug

Para acceder a todos los registros de la tabla locations debemos usar la siguiente ruta: Get:http://api.rick-morty.test/v1/locations
Para almacenar un registro en la tabla location debemos usar la siguiente ruta: Post:http://api.rick-morty.test/v1/locations
Para actualizar un registro en la tabla location debemos usar la siguiente ruta: Put:http://api.rick-morty.test/v1/locations/$id
para eliminar un registro en la tabla location debemos usar la siguiente ruta: Delete:http://api.rick-morty.test/v1/locations/$id

Los campos requeridos para la tabla episodes son: name, air_date, episode, slug
Para acceder a todos los registros de la tabla episodes debemos usar la siguiente ruta: Get:http://api.rick-morty.test/v1/episodes
Para almacenar un registro en la tabla episodes debemos usar la siguiente ruta: Post:http://api.rick-morty.test/v1/episodes
Para actualizar un registro en la tabla episodes debemos usar la siguiente ruta: Put:http://api.rick-morty.test/v1/locations/$id
Para eliminar un registro en la tabla episodes debemos usar la siguiente ruta: Delete:http://api.rick-morty.test/v1/locations/$id

Los campos requeridos para la tabla characters son: name, status, species, type, gender, slug, location_id, origin, episodes
Para acceder a todos los registros de la tabla characters debemos usar la siguiente ruta: Get:http://api.rick-morty.test/v1/characters
Para almacenar un registro en la tabla characters debemos usar la siguiente ruta: Post:http://api.rick-morty.test/v1/characters
para actualizar un registro en la tabla characters debemos usar la siguiente ruta: Put:http://api.rick-morty.test/v1/characters/$id
Para eliminar un registro en la tabla characters debemos usar la siguiente ruta: Delete:http://api.rick-morty.test/v1/characters/$id

He de aclarar que aparte de Laravel Passport, también se utilizó Laravel breeze, Blade, Vue, Axios, SweetAlert2 y los estilos de Tailwind

De antemano agradezco la oportunidad brindada para demostrar mis conocimientos en el tema de Laravel, acá demuestro que tengo conocimiento no solo en back, sino en front.

Quedo atento a cualquier comentario.

Saludos.

