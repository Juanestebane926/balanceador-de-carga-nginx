# Balanceador de Carga con NGINX

Este proyecto configura un balanceador de carga simple usando NGINX y Docker Compose para gestionar múltiples servicios detrás del balanceador.

## Requisitos

- [Docker](https://www.docker.com/get-started)
- [Docker Compose](https://docs.docker.com/compose/install/)

## Iniciar el Proyecto

Sigue estos pasos para clonar el repositorio e iniciar el proyecto en tu máquina local:

1. **Clona el repositorio**:

   ```bash
   git clone https://github.com/Juanestebane926/balanceador-de-carga-nginx.git
   ```

2. **Ingresa al directorio del proyecto**:

   ```bash
   cd balanceador-de-carga-nginx
   ```

3. **Inicia los contenedores con Docker Compose**:

   ```bash
   
   docker-compose up -d
   ```

   Esto descargará las imágenes necesarias y levantará los contenedores en segundo plano.

4. **Accede al balanceador de carga**:

   Abre tu navegador y dirígete a [http://localhost/api/listarProductos](http://localhost/api/listarProductos) para verificar que el balanceador de carga esté funcionando.

   Aquí tienes el `README.md` actualizado con la información sobre cómo cambiar la cantidad de servidores en el balanceador de carga:

## Configurar la Cantidad de Servidores

Para ajustar la cantidad de servidores que el balanceador de carga NGINX usará, edita el archivo `nginx.conf` y comenta o descomenta las líneas correspondientes a los servidores según sea necesario.

1. Abre el archivo `nginx.conf` ubicado en el directorio `nginx` (o donde esté en tu proyecto):

   ```bash
   nano nginx/nginx.conf
   ```

2. Comenta (`#`) los servidores que no desees utilizar o descomenta los que quieras activar. Ejemplo:

   ```nginx
   upstream upstream-server {
        least_conn;
        server app1:3000;
        server app2:3001;
        #server app3:3002;
        #server app4:3003;
        #server app5:3004;
    }
   ```

3. Guarda los cambios y reinicia los contenedores para aplicar la configuración:

   ```bash
   docker-compose down
   docker-compose up -d
   ```


## Apagar el Proyecto

Para detener y eliminar los contenedores, ejecuta:

```bash
docker-compose down
```
