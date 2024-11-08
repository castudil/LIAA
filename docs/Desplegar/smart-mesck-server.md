# Smart Mesck Server

A continuación, se detallarán los pasos necesarios para llevar a cabo la construcción y configuración de Smart-Mesck-Server, así como también se proporcionarán los pasos para su despliegue. Sigue las instrucciones cuidadosamente para asegurarte de tener una implementación exitosa del servidor y garantizar una experiencia óptima para los usuarios.

## Descargar e Instalar Python

- Visita el [sitio web oficial de Python](https://www.python.org/).
- Haz clic en el botón de descarga correspondiente a tu sistema operativo (Windows, macOS o Linux).
- Sigue las instrucciones de instalación proporcionadas por el instalador de Python.
- Verifica que Python se haya instalado correctamente abriendo una ventana de terminal y ejecutando el siguiente comando:

```bash
python --version
```

Deberías ver la versión instalada de Python.

## Instalar las dependencias del proyecto

- Abre una ventana de terminal.
- Navega hasta el directorio raíz de tu proyecto.
- Ejecuta el siguiente comando para instalar las dependencias del proyecto:

```bash
pip install -r requirements.txt
```

Esto descargará e instalará todas las dependencias listadas en el archivo `requirements.txt`. Por lo que es necesario tener una conexión a internet para poder realizar toda la descarga.

## Configurar las variables de entorno

Este proyecto requiere el uso de variables de entorno. Como primer paso, verifica que el fichero .env exista en el directorio raíz del proyecto y contenga la información necesaria. Por ejemplo:

```bash
SECRET_KEY = "###"
ALGORITHM = "HS256"
ACCESS_TOKEN_EXPIRE_MINUTES = 30
DB_URL = "postgresql://user:password@host/database"
MAIL_NAME="CTTN"
MAIL_USER="no-reply@cttn.cl"
MAIL_PASS="###"
MAIL_HOST="mail.cttn.cl"
MAIL_PORT=465
BASE_URL = "http://localhost:8000"
SMART_MESCK_URL = "http://localhost:5173"
HAPI_FHIR_URL = "https://castudillo-hapi.darknacho.xyz/fhir"
```

- `SECRET_KEY`: Esta variable almacena la clave secreta utilizada para validar los tokens JWT (JSON Web Tokens) en la aplicación. Esta clave se utiliza para verificar la autenticidad y la integridad de los tokens, y es importante mantenerla en secreto para garantizar la seguridad del sistema.

- `ALGORITHM`: Esta variable especifica el algoritmo de cifrado que se utilizará para generar y verificar tokens de acceso. En este caso, se utiliza el algoritmo HS256, que es un algoritmo de cifrado basado en una clave secreta.

- `ACCESS_TOKEN_EXPIRE_MINUTES`: Esta variable define el tiempo de expiración de los tokens de acceso generados por la aplicación. En este caso, los tokens de acceso expirarán después de 30 minutos.

- `DB_URL`: Esta variable almacena el connection string para la base de datos utilizada por la aplicación. Asegúrate de tener instalado un adaptador que soporte SQLAlchemy para tu base de datos específica. En este ejemplo, se utiliza una base de datos PostgreSQL y se proporciona el connection string, incluyendo el nombre de usuario, contraseña, host y nombre de la base de datos.

- `MAIL_NAME`, `MAIL_USER`, `MAIL_PASS`, `MAIL_HOST`, `MAIL_PORT`: Estas variables almacenan la información de configuración del servidor de correo electrónico utilizado por la aplicación para enviar correos electrónicos. Incluyen el nombre del remitente, la dirección de correo electrónico del remitente, la contraseña del remitente, el host del servidor de correo y el puerto utilizado para la conexión.

`BASE_URL`: Esta variable almacena la URL base de la aplicación. Es la URL principal a la que los usuarios accederán para interactuar con la aplicación.

`SMART_MESCK_URL`: Esta variable almacena la URL del servicio Smart Mesck al que la aplicación se conectará. Es la dirección del servidor que proporciona funcionalidades específicas para la aplicación.

`HAPI_FHIR_URL`: Esta variable almacena la URL del servicio HAPI FHIR al que la aplicación se conectará. HAPI FHIR es una implementación de la especificación FHIR (Fast Healthcare Interoperability Resources) y se utiliza para el intercambio de datos de salud.

Estas variables de entorno son configuradas en un archivo .env en el directorio raíz del proyecto y se utilizan en la aplicación para acceder a la información necesaria para su funcionamiento.

