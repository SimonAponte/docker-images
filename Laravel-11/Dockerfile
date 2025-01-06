FROM php:8.3-apache

# Actualizar e instalar dependencias
RUN apt-get update && apt-get install -y \
    libicu-dev libzip-dev unzip git curl zip nano \
    libonig-dev  # Dependencia para mbstring

# Instalar las extensiones de PHP una por una para identificar el error
RUN docker-php-ext-install pdo_mysql
RUN docker-php-ext-install mbstring
RUN docker-php-ext-install intl
RUN docker-php-ext-install opcache
RUN docker-php-ext-install zip
RUN docker-php-ext-install bcmath

# Limpiar la caché
RUN apt-get clean && rm -rf /var/lib/apt/lists/*

# Habilitar mod_rewrite
RUN a2enmod rewrite

# Instalar Composer
COPY --from=composer:2.6 /usr/bin/composer /usr/bin/composer

# Configuración de permisos y directorio de trabajo
WORKDIR /var/www/html
