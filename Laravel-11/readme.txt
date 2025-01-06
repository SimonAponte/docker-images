1.-Primero hacer el docker build

2.-Hacer el docker compose 

3.-Si da el mensaje con respecto a que no puede hacer pull al laravel app, contruir la imagen localmente (ya que la esta buscando en dockerhub) usar comando

docker build -t laravel-app .

4.-Hacer el docker compose 

5.-abrir esta terminal docker exec -it laravel-app bash

6.-Crear el proyecto de laravel con el comando

composer create-project --prefer-dist laravel/laravel . "11.*"

7.-Si por algún motivo el volumen de node no muestra los archivos del laravel es decir de la carpeta www, remover todos los contenedores con 

docker-compose down -v 

y luego proceder con docker compose up -d

8.-Para compilar assets y usar node configurar el archivo vite.config.js añadiendo siguiente 

server: {
        host: '0.0.0.0',  // Esto hace que Vite escuche en todas las interfaces
        port: 3000,        // Establece el puerto a 3000
    },
9.-Para que funcione el tailwind configurar en el .env APP_URL=http://localhost:8080 y añadir en vite.config.js

proxy: {
        '/': {
            target: 'http://laravel-app:8080',  // Nombre del servicio de Laravel en Docker
            changeOrigin: true,
            secure: false,
        },
    },
