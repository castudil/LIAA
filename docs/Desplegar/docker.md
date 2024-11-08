# Utilizando Docker

## Despliegue del proyecto con Docker Compose

[Docker](https://www.docker.com) es una plataforma de virtualización a nivel de contenedores que permite empaquetar una aplicación y sus dependencias en un contenedor ligero y portátil. Un contenedor Docker incluye todo lo necesario para ejecutar la aplicación de manera eficiente y consistente, como el código, las bibliotecas, las herramientas y las configuraciones.

[Docker Compose](https://docs.docker.com/compose/install/), por otro lado, es una herramienta que facilita la gestión y la orquestación de múltiples contenedores Docker. Permite definir y configurar servicios y sus dependencias en un archivo YAML, lo que simplifica el despliegue y la gestión de aplicaciones que se componen de varios contenedores interconectados.

En el contexto de este proyecto, se ha utilizado [Docker](https://www.docker.com) y [Docker Compose](https://docs.docker.com/compose/install/) para empaquetar y desplegar la aplicación en contenedores Docker. Esto proporciona un entorno aislado y consistente para ejecutar el proyecto, independientemente de las diferencias en los entornos de desarrollo o producción. Al utilizar Docker Compose, se simplifica aún más el proceso de ejecución y gestión de los contenedores que forman parte del proyecto.

A continuación, se presentarán las instrucciones para desplegar el proyecto utilizando Docker y Docker Compose, lo que permitirá ejecutar la aplicación de manera rápida y sencilla en cualquier entorno compatible con Docker.

1. **Descargar Docker Compose**
   Antes de poder ejecutar un archivo `docker-compose.yml`, necesitarás tener Docker Compose instalado en tu sistema. Sigue estos pasos para descargarlo:

   - Visita la página de  [Docker Compose](https://docs.docker.com/compose/install/).
   - Sigue las instrucciones de instalación correspondiente a tu sistema operativo (Windows, macOS o Linux).
   - Verifica que Node.js se haya instalado correctamente abriendo una ventana de terminal y ejecutando el siguiente comando:

     ```shell
     $ docker compose version
     Docker Compose version v2.20.2
     ```

   Ahora deberías tener Docker Compose instalado en tu sistema.
2. **Edición**

   - **Seleción de puertos**

     Aquí tienes una explicación del mapeo de puertos en el archivo `docker-compose.yml` proporcionado:

     ```yaml
     services:
     ui:
         ports:
         - 5001:80
     api:
         ports:
         - 5002:80
     graph:
         ports:
         - 5003:80
     ```
     En este ejemplo, hay tres servicios definidos: `ui`, `api` y `graph`.

     - Para el servicio `ui`, se realiza un mapeo del puerto `5001` del host al puerto `80` del contenedor. Esto significa que puedes acceder al servicio de la interfaz de usuario (UI) desde tu máquina local utilizando `http://localhost:5001`.
     - Para el servicio `api`, se realiza un mapeo del puerto `5002` del host al puerto `80` del contenedor. Esto significa que puedes acceder al servicio de la API desde tu máquina local utilizando `http://localhost:5002`.
     - Para el servicio `graph`, se realiza un mapeo del puerto `5003` del host al puerto `80` del contenedor. Esto significa que puedes acceder al servicio de gráficos desde tu máquina local utilizando `http://localhost:5003`.

     El formato del mapeo de puertos es `<puerto_del_host>:<puerto_del_contenedor>`. Esto permite redirigir las solicitudes que llegan al puerto del host especificado al puerto correspondiente dentro del contenedor.

     Es importante tener en cuenta que si los puertos especificados (`5001`, `5002`, `5003` en este caso) ya están en uso en tu máquina local, deberás elegir puertos diferentes para el mapeo o liberar los puertos en uso antes de ejecutar el archivo `docker-compose.yml`.

     El mapeo de puertos es útil para exponer los servicios de tus contenedores de Docker a través de puertos accesibles en tu máquina local, lo que te permite interactuar con ellos desde tu navegador web u otras herramientas externas.
   - **Asignar variables de entorno**

     1. **Credenciales de la base de datos:**

        - `DATABASE_Host`: Especifica el host o la dirección IP del servidor de la base de datos.
        - `DATABASE_Port`: Indica el puerto en el que se escucha la conexión de la base de datos.
        - `DATABASE_Username`: Representa el nombre de usuario utilizado para autenticarse en la base de datos.
        - `DATABASE_Password`: Es la contraseña asociada al usuario de la base de datos.
        - `DATABASE_Database`: Especifica el nombre de la base de datos a la que se desea conectar.

        2. **Credenciales de correo electrónico (MAIL):**

        - `MAIL_Sender`: Es la dirección de correo electrónico del remitente.
        - `MAIL_DisplayName`: Es el nombre que se mostrará como remitente en los correos electrónicos enviados.
        - `MAIL_Password`: Representa la contraseña o clave de acceso del correo electrónico del remitente.
        - `MAIL_SmtpHost`: Especifica el host del servidor SMTP utilizado para enviar correos electrónicos.
        - `MAIL_Port`: Indica el puerto utilizado para la conexión SMTP.
     2. **Variable secreta (JWT_KEY):**

        - `JWT_KEY`: Es una clave secreta utilizada para firmar y verificar los tokens de autenticación JWT (JSON Web Token). Esta clave debe ser única y mantenerse en secreto para garantizar la seguridad de los tokens generados.
     3. **Direcciones (URL)**

        - `UI_URL`: Especifica la dirección donde se encuentra Smart-Mesck-UI
        - `API_URL`: Especifica la dirección donde se encuentra Smart-Mesck-API
        - `GRAPH_URL`: Especifica la dirección donde se encuentra Smart-Mesck-Graph
3. **Ejecutar Docker Compose**

   Una vez que tengas el archivo `docker-compose.yml` listo, puedes ejecutarlo utilizando el siguiente comando:

   ```shell
   $ docker-compose up
   ```
   Asegúrate de abrir tu terminal y ubicarte en el directorio donde se encuentra el archivo `docker-compose.yml` antes de ejecutar el comando.

   Docker Compose leerá el archivo `docker-compose.yml`, creará los contenedores y configuraciones definidas en él, y los iniciará. Verás los registros de salida de cada contenedor en la terminal.

   Si deseas ejecutar Docker Compose en modo desacoplado (en segundo plano), puedes utilizar la opción `-d`:

   ```shell
   $ docker-compose up -d
   ```
4. **Detener los servicios**: Para detener los servicios y los contenedores en ejecución, puedes utilizar el siguiente comando:

   ```shell
   docker-compose down
   ```
   Esto detendrá y eliminará los contenedores creados a partir del archivo `docker-compose.yml`.


## Ejecución de servicios individuales con Docker

Cada servicio incluye su propio `Dockerfile`, lo que te permite ejecutarlos de forma individual si así lo deseas. A continuación, se muestra cómo puedes hacerlo:

1. **Edición de variables de entorno**
   Antes de construir y ejecutar los servicios individuales, debes editar las variables de entorno en los respectivos archivo de Docker. Estas variables son similares a las que se mencionaron en la sección anterior de Docker Compose.

   - Abre el `Dockerfile` correspondiente al servicio que deseas ejecutar de forma individual, estos se encuentran en la carpeta de cada servicio.
   - Busca las instrucciones `ENV` en el Dockerfile y edita los valores de las variables de entorno según tus necesidades.

2. **Construcción y ejecución del servicio**
   Una vez que hayas editado las variables de entorno, puedes construir y ejecutar el servicio utilizando los siguientes comandos:

   - Navega hasta el directorio que contiene el Dockerfile del servicio que deseas ejecutar.

   - Ejecuta el siguiente comando para construir la imagen del Docker:

     ```shell
     $ docker build -t nombre_imagen .
     ```

     Asegúrate de reemplazar `nombre_imagen` con un nombre significativo para la imagen del servicio.

   - Después de que la imagen se haya construido correctamente, puedes ejecutar el servicio utilizando el siguiente comando:

     ```shell
     $ docker run -p puerto_host:puerto_contenedor nombre_imagen
     ```

     Reemplaza `puerto_host` con el puerto del host en el que deseas mapear el servicio, y `puerto_contenedor` con el puerto en el que el servicio se está ejecutando dentro del contenedor.

     Por ejemplo, si deseas ejecutar el servicio de interfaz de usuario en el puerto 5001 de tu host, y has construido la imagen con el nombre `ui-image`, puedes ejecutar el siguiente comando:

     ```shell
     $ docker run -p 5001:80 ui-image
     ```

     Esto iniciará el contenedor del servicio de interfaz de usuario y lo mapeará al puerto 5001 de tu máquina local.

3. **Edición de variables de entorno para servicios individuales**
   Si deseas editar las variables de entorno para los servicios individuales, puedes hacerlo siguiendo los mismos pasos descritos anteriormente en la sección de Docker Compose. Busca las variables de entorno correspondientes en el Dockerfile del servicio que estás ejecutando de forma individual y modifica sus valores según sea necesario.

Recuerda que al editar las variables de entorno en los Dockerfiles, debes tener en cuenta la configuración específica de cada servicio y asegurarte de proporcionar los valores correctos para un funcionamiento adecuado.
