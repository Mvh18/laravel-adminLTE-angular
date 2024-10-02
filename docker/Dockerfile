FROM php:7.4-apache

# Instalamos las extensiones necesarias para Laravel
RUN apt-get update && apt-get install -y \
    libzip-dev \
    zip \
    unzip \
    git \
    && docker-php-ext-install pdo_mysql zip
 

RUN curl -fsSL https://deb.nodesource.com/setup_20.x | bash - \
    && apt-get install -y nodejs \
    && npm install -g npm@latest  # optional: to install the latest npm version

# Instalamos Composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# Configurar el directorio de trabajo
WORKDIR /var/www/html

# Activar el módulo de reescritura de Apache para Laravel
RUN a2enmod rewrite

# Establecer el virtual host apuntando a public
COPY ./000-default.conf /etc/apache2/sites-available/000-default.conf

# Exponemos el puerto 80
EXPOSE 80

# Iniciar Apache en primer plano
CMD ["apache2-foreground"]


