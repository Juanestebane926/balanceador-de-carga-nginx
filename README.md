# Balanceador de Carga con NGINX

Este proyecto configura un balanceador de carga simple usando NGINX y Docker Compose para gestionar múltiples servicios detrás del balanceador.

## Requisitos

- [Docker](https://www.docker.com/get-started)
- [Docker Compose](https://docs.docker.com/compose/install/)

## Iniciar el Proyecto

Sigue estos pasos para clonar el repositorio e iniciar el proyecto en tu máquina local:

1. **Clona el repositorio**:

   ```bash
   git clone https://github.com/Juanestebane926/balanceador-de-carga-nginx
   ```

2. **Ingresa al directorio del proyecto**:

   ```bash
   cd balanceador-de-carga-nginx
   ```

3. **Inicia los contenedores con Docker Compose**:

   ```bash
   
   docker-compose up
   ```

   Esto descargará las imágenes necesarias y levantará los contenedores en segundo plano.

4. **Accede al balanceador de carga**:

   Abre tu navegador y dirígete a [http://localhost/api/listarProductos](http://localhost/api/listarProductos) para verificar que el balanceador de carga esté funcionando.


## Frontend

El proyecto incluye un servicio de frontend accesible en el puerto `6969`. Este servicio está configurado para consumir las APIs expuestas por los servicios de backend (`app`) a través del balanceador de carga de NGINX.

- **Acceso al Frontend**: [http://localhost:6969](http://localhost:6969)

si estás usando un entorno aislado de pruebas, debes configurar la maquina virtual que esté hosteando los contenedores para que tenga la ip `196.169.60.3` para que funcione correctamente y usar el servicio de front servido en el puerto `9696` en vez del normal.

- **Acceso al Frontend con VM**: [http://192.168.60.3:9696](http://192.168.60.3:9696)

## Configurar la Cantidad de Servidores

Para ajustar la cantidad de servidores que el balanceador de carga NGINX usará, edita el archivo `nginx.conf` y comenta o descomenta las líneas correspondientes a los servidores según sea necesario.

1. Abre el archivo `nginx.conf`

   ```bash
   nginx/nginx.conf
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
   docker-compose up
   ```


## Apagar el Proyecto

Para detener y eliminar los contenedores, ejecuta:

```bash
docker-compose down
```

## Ambiente de pruebas en vagrant

Para mayor facilidad a la hora de correr el proyecto y sus pruebas hemos creado una vagrant box con todo lo necesario, no olvidar la creacion de una carpeta "Sync" en la ubicacion del vagrantfile para su correcta ejecución.
```bash
Vagrant.configure("2") do |config|
  config.vm.box = "serviciostele/test"
  config.vm.box_version = "1.0"
  config.vm.network :private_network, ip: "192.168.60.3"    
  config.vm.synced_folder "Sync/", "/home/vagrant/Sync"
end
```

