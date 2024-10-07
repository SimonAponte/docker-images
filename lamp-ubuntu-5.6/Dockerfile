# Usamos Ubuntu 20.04 como base
FROM ubuntu:20.04

# Evitamos que durante la instalación se presenten preguntas
ENV DEBIAN_FRONTEND=noninteractive

# Instalamos las dependencias necesarias y actualizamos la imagen
RUN apt-get update && apt-get install -y \
    apache2 \
    gnupg2 \
    ca-certificates \
    apt-transport-https \
    lsb-release \
    wget \
    curl \
    unzip \
    software-properties-common \
    && apt-get clean

# Agregamos el repositorio de Ondřej Surý para PHP 5.6
RUN add-apt-repository ppa:ondrej/php -y

# Instalamos PHP 5.6 y las extensiones necesarias
RUN apt-get update && apt-get install -y \
    php5.6 \
    php5.6-mysql \
    php5.6-xml \
    php5.6-mbstring \
    php5.6-curl \
    php5.6-zip \
    php5.6-intl \
    php5.6-gd \
    libapache2-mod-php5.6 \
    && apt-get clean

# Habilitamos mod_rewrite en Apache
RUN a2enmod rewrite

# Copiamos los archivos de la aplicación a /var/www/html
COPY www/ /var/www/html/

# Cambiamos el propietario de los archivos a www-data (usuario de Apache)
RUN chown -R www-data:www-data /var/www/html/

# Exponemos el puerto 80 para el contenedor
EXPOSE 80

# Apache se ejecutará en segundo plano
CMD ["apache2ctl", "-D", "FOREGROUND"]

