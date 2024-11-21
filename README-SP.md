# Dockerized Oracle SQL Developer

Este proyecto proporciona un contenedor Docker para ejecutar Oracle SQL Developer, una herramienta de gestión de bases de datos Oracle. Los contenedores están configurados para soportar arquitecturas **amd64** y **arm64** mediante `docker-compose`. 

## Características
- Basado en imágenes de ubuntu 22.04.
- Incluye Oracle SQL Developer versión `24.3.0.284.2209`.
- Configuración predefinida para una fácil implementación con soporte para persistencia de datos.

## Requisitos previos
1. [Docker](https://www.docker.com/) instalado.
2. [Docker Compose](https://docs.docker.com/compose/) instalado.
3. Arquitectura de CPU compatible (`amd64` o `arm64`).

# Uso

## Clonar el repositorio
```bash
git clone https://github.com/ozkr0124/dockerized-oracle-sql-developer.git
cd dockerized-oracle-sql-developer
```

## Ejecutar con Docker Compose

### Para arquitecturas ARM64

1.	Usa el archivo ***docker-compose.arm64.yml***:

```bash
docker-compose -f docker-compose.arm64.yml up -d
```
2.	Accede a la aplicación con
```
https://localhost:8444
```

### Para arquitecturas AMD64

1.	Usa el archivo ***docker-compose.amd64.yml***:
```bash
docker-compose -f docker-compose.amd64.yml up -d
```
2.	Accede a la aplicación en 
```
https://localhost:8444
```

## Personalización

### Variables de entorno

Puedes modificar las siguientes variables de entorno en los archivos ***docker-compose.\*.yml*** para personalizar tu entorno:
- `TZ`: Zona horaria (por defecto `America/Bogota`).

### Puertos

El puerto por defecto del contenedor es `8444`. Para exponerlo, el archivo docker-compose asigna el puerto `8444` en el host. Puedes modificar esta configuración según sea necesario.

### Persistencia de datos

Los datos de configuración de Oracle SQL Developer se almacenan en un volumen Docker llamado ***sqldeveloper-data***. Esto asegura que las configuraciones persistan entre reinicios del contenedor.

### Detener y eliminar el contenedor

Para detener y eliminar el contenedor junto con los volúmenes asociados:

```bash
docker-compose -f docker-compose.arm64.yml down -v
# o
docker-compose -f docker-compose.amd64.yml down -v
```

## Detalles técnicos

### Imágenes base

- **ARM64/AMD64**: `ubuntu:22.04`.

### Dockerfile

El Dockerfile instala:
1. JDK 17 (requerido por SQL Developer).
2. Oracle SQL Developer.
3. KasmVNC
4. Openbox GNOME
5. Supervisor
6. Configura el contenedor para exponer el puerto `8444` y usar un supervisor para la ejecucion de varios procesos dentro del contenedor.

### Seguridad

- Se configura ***seccomp:unconfined*** para permitir funcionalidades avanzadas dentro del contenedor. Esto puede ajustarse según las necesidades de seguridad.

# Contribuciones

¡Las contribuciones son bienvenidas! Si encuentras un problema o tienes una mejora, no dudes en abrir un issue o enviar un pull request.

# Licencia

Este proyecto está licenciado bajo los términos de [MIT License](https://opensource.org/license/mit) y [Oracle Free Use Terms and Conditions](https://www.oracle.com/downloads/licenses/oracle-free-license.html)