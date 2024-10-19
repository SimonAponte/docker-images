# Usamos la imagen oficial de PHP 8.3 con Apache
FROM php:8.3-apache

# Variables de entorno
ENV APACHE_DOCUMENT_ROOT /var/www/html

# Actualizamos e instalamos dependencias
RUN apt-get update && apt-get install -y \
    libfreetype6-dev \
    libjpeg62-turbo-dev \
    libpng-dev \
    libzip-dev \
    libonig-dev \
    libxml2-dev \
    mariadb-client \
    git \
    unzip \
    curl \
    nano \
    wget \
    nodejs \
    npm \
    && docker-php-ext-configure gd --with-freetype --with-jpeg \
    && docker-php-ext-install pdo pdo_mysql mbstring exif pcntl bcmath gd zip fileinfo 

# Instalamos Composer 2 globalmente
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# Configuración del directorio de trabajo
WORKDIR /var/www/html

# Instalamos Node.js v18 y NPM v10
RUN npm install -g npm@10 && npm install -g vite@5

# Habilitar módulos de Apache necesarios para Laravel
RUN a2enmod rewrite

# Copiamos el archivo de vhost
COPY ./vhost.conf /etc/apache2/sites-available/000-default.conf

# Copiamos php.ini
COPY ./php.ini /usr/local/etc/php/php.ini

# Asignamos permisos a la carpeta www
RUN chown -R www-data:www-data /var/www/html

# Exponemos el puerto 80
EXPOSE 80

# Ejecutamos Apache en modo foreground
CMD ["apache2-foreground"]
