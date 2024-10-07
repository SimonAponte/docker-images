FROM php:5.6-apache

# Eliminar cualquier configuración de fuentes de paquetes anteriores
RUN rm -f /etc/apt/sources.list.d/* \
    && rm -f /etc/apt/sources.list \
    && echo "deb http://archive.debian.org/debian stretch main" > /etc/apt/sources.list \
    && echo "deb http://archive.debian.org/debian stretch/updates main" >> /etc/apt/sources.list \
    && echo "deb http://archive.debian.org/debian-security stretch/updates main" >> /etc/apt/sources.list

# Instalamos los paquetes necesarios e ignoramos los errores de repositorios faltantes
RUN apt-get update --allow-releaseinfo-change \
    && apt-get install -y \
    ca-certificates \
    apt-transport-https \
    wget \
    gnupg2 \
    --allow-unauthenticated \
    || true \
    && wget -q https://packages.sury.org/php/apt.gpg -O- | apt-key add - \
    && echo "deb https://packages.sury.org/php/ stretch main" | tee /etc/apt/sources.list.d/php.list \
    && apt-get update --allow-releaseinfo-change \
    && apt-get install -y \
    php5.6 \
    php5.6-mysql \
    php5.6-xml \
    php5.6-mbstring \
    php5.6-curl \
    php5.6-zip \
    php5.6-intl \
    --allow-unauthenticated \
    || true \
    && apt-get clean

# Instalar Composer 1.x (específicamente la última versión compatible con PHP 5.6)
RUN curl -sS https://getcomposer.org/download/1.10.22/composer.phar -o /usr/local/bin/composer \
    && chmod +x /usr/local/bin/composer

# Exponer el puerto 80
EXPOSE 80

# Ejecutamos Apache en primer plano (esto es necesario para que el contenedor siga corriendo)
CMD ["apache2-foreground"]
