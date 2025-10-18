# Práctica de Docker - Contenedores y Gestión Básica

Este documento recoge todos los comandos y pasos realizados en la práctica de Docker, dividida en dos partes principales.

## Parte A - Ejercicios Básicos de Docker

### Paso 1: Instalación y Configuración de Docker Desktop

1. Descargar Docker Desktop desde https://www.docker.com/products/docker-desktop/
2. Instalar con configuración WSL 2
3. Verificar instalación:

```bash
docker --version
```

### Paso 2: Contenedor Hello-World

Ejecutar y gestionar el contenedor hello-world:

```bash
# Ejecutar contenedor hello-world
docker run hello-world

# Verificar contenedores en ejecución (vacío)
docker ps

# Listar todos los contenedores (incluidos parados)
docker ps -a

# Borrar el contenedor hello-world
docker rm <CONTAINER_ID>

# Verificar que se eliminó
docker ps -a
```

### Paso 3: Contenedor Interactivo con Debian

Crear y trabajar con un contenedor interactivo:

```bash
# Crear contenedor interactivo Debian
docker run -it --name mi_debian debian

# Dentro del contenedor: actualizar paquetes
apt update

# Instalar nano
apt install nano

# Salir del contenedor
exit

# Verificar estado (parado)
docker ps
docker ps -a

# Reiniciar contenedor
docker start mi_debian

# Acceder nuevamente de forma interactiva
docker exec -it mi_debian bash

# Verificar que nano sigue instalado
nano --version

# Salir del contenedor
exit

# Parar y eliminar contenedor
docker stop mi_debian
docker rm mi_debian

# Crear nuevo contenedor desde imagen original
docker run -it debian

# Verificar que nano NO está instalado (imagen limpia)
nano --version
```

**Conclusión:** Los cambios se mantienen en el contenedor específico, no en la imagen base.

### Paso 4: Contenedor Demonio con Nginx

Crear un servidor web con nginx:

```bash
# Crear contenedor nginx en modo demonio
docker run -d --name mi_nginx -p 80:80 nginx

# Verificar que está corriendo
docker ps

# Ver logs del contenedor
docker logs mi_nginx

# Ver logs en tiempo real (opcional)
docker logs -f mi_nginx
```

**Acceso web:** http://localhost

**Nota:** No fue necesario especificar comando porque nginx ya tiene CMD predefinido.

### Paso 5: Contenedor Nextcloud

Crear contenedor Nextcloud con base de datos SQLite personalizada:

```bash
# Crear contenedor Nextcloud con variable de entorno personalizada
docker run -d --name mi_nextcloud -p 8080:80 -e SQLITE_DATABASE=mi_bd_personalizada nextcloud

# Verificar que está corriendo
docker ps

# Ver logs del contenedor
docker logs mi_nextcloud
```

**Acceso web:** http://localhost:8080

## Parte B - Ejercicio Específico: Servidor Web

### Objetivo
Crear un contenedor demonio nginx llamado "servidor_web" accesible por el puerto 8181.

### Comandos Ejecutados

```bash
# Crear contenedor con nombre específico y puerto 8181
docker run -d --name servidor_web -p 8181:80 nginx

# Verificar que está funcionando
docker ps

# Ver imágenes en registro local
docker images

# Parar el contenedor
docker stop servidor_web

# Eliminar el contenedor
docker rm servidor_web

# Verificar eliminación
docker ps -a
```

**Acceso web:** http://localhost:8181

## Conceptos Aprendidos

### Diferencias entre Contenedores e Imágenes
- **Imagen:** Plantilla inmutable para crear contenedores
- **Contenedor:** Instancia ejecutable de una imagen con sus propios cambios

### Tipos de Contenedores
- **Interactivos (`-it`):** Para trabajar directamente en el contenedor
- **Demonio (`-d`):** Para servicios que corren en segundo plano

### Gestión de Contenedores
- `docker run`: Crear y ejecutar contenedor
- `docker ps`: Ver contenedores en ejecución
- `docker ps -a`: Ver todos los contenedores
- `docker start`: Iniciar contenedor parado
- `docker stop`: Parar contenedor
- `docker rm`: Eliminar contenedor
- `docker logs`: Ver logs de contenedor

### Mapeo de Puertos
- `-p host_port:container_port`: Mapea puerto del host al contenedor
- Ejemplo: `-p 8181:80` mapea puerto 8181 del host al puerto 80 del contenedor

### Variables de Entorno
- `-e VARIABLE=valor`: Define variables de entorno en el contenedor
- Útil para configurar aplicaciones sin modificar la imagen

## Autor
SebasRomaguera

## Fecha
2025-10-18