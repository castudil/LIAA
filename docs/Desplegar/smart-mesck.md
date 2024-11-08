# Smart Mesck Web

A continuación, se detallarán los pasos necesarios para llevar a cabo la construcción y configuración de Smart-Mesck-UI, así como también se proporcionarán los pasos para su despliegue. Sigue las instrucciones cuidadosamente para asegurarte de tener una implementación exitosa de la interfaz gráfica y garantizar una experiencia óptima para los usuarios.

## Descargar e Instalar Node.js

- Visita el sitio web oficial de [Node.js](https://nodejs.org).
- Haz clic en el botón de descarga correspondiente a tu sistema operativo (Windows, macOS o Linux).
- Sigue las instrucciones de instalación proporcionadas por el instalador de Node.js.
- Verifica que Node.js se haya instalado correctamente abriendo una ventana de terminal y ejecutando el siguiente comando:

```shell
$ node --version
```

Deberías ver la versión instalada de Node.js.

## Construir la aplicación

Abre una ventana de terminal.
Navega hasta el directorio raíz de tu proyecto .
Ejecuta el siguiente comando para instalar las dependencias del proyecto:

```shell
$ npm install
```

Esto descargará e instalará todas las dependencias listadas en el archivo `package.json`. Por lo que es necesario tener una conexión a internet para poder realizar toda la descarga.
   
- Una vez completada la instalación de las dependencias, puedes ejecutar uno de los scripts definidos en el archivo `package.json`. Por ejemplo, para iniciar la aplicación en modo de desarrollo, ejecuta:

```shell
$ npm run dev
```

Esto iniciará la aplicación utilizando el comando `vite --mode development` proporcionado en el script `dev` del archivo `package.json`.
    
- Para construir la aplicación, ejecuta:

```shell
$ npm run build
```

Esto generará los archivos optimizados listos para desplegar en un entorno de producción.

## Ejecutar el proyecto

1. Este proyecto, requiere el uso de variables de entorno, por lo que como primer paso es necesario

Verificar que el fichero `.env` exista ubicada en `src` y contenga la siguiente información:

```shell
VITE_API_URL=https://castudillo-hapi.darknacho.xyz/fhir
VITE_SERVER_URL=https://castudillo-chart-server-sm.darknacho.xyz
VITE_CHART_SERVER_URL=wss://castudillo-chart-server-sm.darknacho.xyz/dashboard_ws
```

Estos argumentos representan los dominios donde se encuentran los servicios los cuales se utilizan.

1. Después de configurar las variables de entorno y haber completado la instalación de las dependencias, ejecuta el siguiente comando para iniciar la aplicación:

```shell
$ npm run dev
    > smart-mesck@0.0.0 dev
    > vite --mode development
        VITE v5.2.10  ready in 3971 ms
        ➜  Local:   http://localhost:5173/
        ➜  Network: use --host to expose
        ➜  press h + enter to show help
```

Estos mensajes proporcionan información útil sobre la aplicación en ejecución:

Este mensaje muestra que la aplicación está escuchando en `http://localhost:5173`, lo cual indica que se ha configurado HTTP para la aplicación.