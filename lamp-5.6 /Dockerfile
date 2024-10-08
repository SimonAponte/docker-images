FROM php:5.6-apache

# Eliminar cualquier configuración de fuentes de paquetes anteriores
RUN rm -f /etc/apt/sources.list.d/* \
    && rm -f /etc/apt/sources.list \
    && echo "deb http://archive.debian.org/debian stretch main" > /etc/apt/sources.list

# Instalar dependencias necesarias (incluyendo ZLIB, ICU y unzip)
RUN apt-get update \
    && apt-get install -y \
    ca-certificates \
    apt-transport-https \
    wget \
    gnupg2 \
    libzip-dev \
    zlib1g-dev \
    libicu-dev \
    unzip \
    --allow-unauthenticated \
    || true \
    && apt-get clean

# Configurar la extensión zip para que encuentre ZLIB, y luego instalar extensiones
RUN docker-php-ext-configure zip --with-zlib-dir=/usr \
    && docker-php-ext-install zip \
    && docker-php-ext-install mysqli \
    && docker-php-ext-install mbstring \
    && docker-php-ext-configure intl \
    && docker-php-ext-install intl

# Instalar Composer 1.x (compatible con PHP 5.6)
RUN curl -sS https://getcomposer.org/download/1.10.22/composer.phar -o /usr/local/bin/composer \
    && chmod +x /usr/local/bin/composer

# Exponer el puerto 80
EXPOSE 80

# Ejecutar Apache en primer plano
CMD ["apache2-foreground"]
