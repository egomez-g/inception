# Inception

## Descripción
Este proyecto tiene como objetivo mejorar tus conocimientos en administración de sistemas utilizando Docker. Se debe crear una infraestructura virtualizada compuesta por varios contenedores Docker que interactúan entre sí, ejecutándose en una máquina virtual.

## Requisitos

- Necesitamos tener Docker y make instalado.
- Todos los archivos de configuración deben estar en la carpeta `srcs/`.
- Se debe incluir un `Makefile` en la raíz del directorio, el cual debe construir y ejecutar la infraestructura usando `docker-compose.yml`.
- Cada servicio debe ejecutarse en su propio contenedor Docker.
- Se deben crear las imágenes de Docker desde Alpine o Debian (penúltima versión estable).
- No se permite usar imágenes predefinidas de DockerHub (excepto Alpine/Debian).

## Servicios Requeridos

1. **NGINX**: Debe soportar TLSv1.2 o TLSv1.3.
2. **WordPress + PHP-FPM**: Instalado y configurado (sin nginx).
3. **MariaDB**: Base de datos para WordPress (sin nginx).
4. **Volumen para la base de datos** de WordPress.
5. **Volumen para los archivos del sitio web** de WordPress.
6. **Red Docker** para conectar los contenedores.

## Configuraciones Adicionales

- Los contenedores deben reiniciarse en caso de fallo.
- Se debe evitar el uso de comandos como `tail -f`, `sleep infinity`, `while true`, etc.
- Se deben crear dos usuarios en la base de datos, uno de ellos administrador (sin "admin" en el nombre de usuario).
- Se debe configurar un dominio `login.42.fr`, apuntando a la IP local.
- Las credenciales y variables de entorno deben almacenarse en un archivo `.env` (ubicado en `srcs/`) y no deben subirse al repositorio.
- El acceso a la infraestructura debe ser exclusivamente a través de NGINX en el puerto 443 con TLSv1.2 o TLSv1.3.

## Estructura del Proyecto

```bash
$ tree
.
├── Makefile
├── srcs
│   ├── docker-compose.yml
│   ├── .env
│   ├── requirements
│   │   ├── mariadb
│   │   │   ├── Dockerfile
│   │   │   ├── conf/
│   │   │   ├── tools/
│   │   ├── nginx
│   │   │   ├── Dockerfile
│   │   │   ├── conf/
│   │   │   ├── tools/
│   │   ├── wordpress
│   │   │   ├── Dockerfile
│   │   │   ├── conf/
│   │   │   ├── tools/
```

## Bonus

Si la parte obligatoria es completada sin errores, se pueden añadir las siguientes mejoras:

- **Redis Cache** para mejorar el rendimiento de WordPress.
- **Servidor FTP** para acceder a los archivos de WordPress.
- **Sitio web estático** (en cualquier lenguaje excepto PHP).
- **Adminer** para gestionar la base de datos.
- **Otro servicio a elección**, justificando su utilidad.

## Instalación y Uso

1. Clonar el repositorio:
   ```bash
   git clone https://github.com/egomez-g/inception.git
   cd inception
   ```

2. Configurar las variables de entorno en `srcs/.env`.

3. Construir y ejecutar los contenedores:
   ```bash
   make
   ```

4. Acceder a la aplicación desde el navegador:
   ```
   https://localhost:8000
   ```

5. Detener y limpiar los contenedores:
   ```bash
   make clean
   ```

