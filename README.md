## Actividad Integradora - Contenedores (Mikroways)

Este proyecto tiene como objetivo desplegar un entorno compuesto por **Redmine** escalado a múltiples réplicas, detrás de un **balanceador de carga (Traefik)**, junto con servicios adicionales como **Maildev** y **phpMyAdmin**. 

### Objetivos
- Correr Redmine con más de una réplica.
- Resolver el manejo de sesiones al tener múltiples instancias de Redmine.
- Colocar un **load balancer** (Traefik) delante de los servicios.
- Exponer a través de Traefik:
  - Redmine
  - Maildev
  - phpMyAdmin
- Configurar acceso HTTPS con certificados inválidos y diferentes hostnames.
- Utilizar nombres `.localhost` para pruebas locales (ejemplo: `redmine.localhost`, `mail.localhost`, `pma.localhost`).

### Servicios

El `docker-compose.yml` incluye:

- **Redmine**: desplegado con 3 réplicas.  
- **MySQL**: base de datos para Redmine.  
- **Maildev**: para pruebas de correo.  
- **phpMyAdmin**: herramienta de administración de MySQL.  
- **Traefik**: balanceador de carga y proxy inverso, configurado para integrarse con Docker.

### Archivos de importancia

- `docker-compose.yml`: definición de los servicios.
- `Dockerfile`: agrega configuración personalizada a Redmine.
- `traefik.yml`: configuración de Traefik.
- `config/configuration.yml`: configuración de Redmine para manejo de sesiones.

### Uso

1. Clonar este repositorio.
2. Levantar los servicios:

    ```bash
    docker compose up -d --build
    ```

Luego de iniciado los servicios, se pueden acceder a las siguientes URLs:
- Panel de administración de Traefik: `http://localhost:7070`
- Redmine (detras de nginx): `http://integrador-redmine.localhost`
- phpMyAdmin: `http://phpmyadmin-integrador.localhost`
- Maildev: `http://maildev-integrador.localhost`
