FROM php:7.3.8-fpm

# Set working directory
WORKDIR /srv/src/project

# Install dependencies
RUN apt-get update && apt-get install -y \
    build-essential \
    libpng-dev \
    libjpeg62-turbo-dev \
    libfreetype6-dev \
    locales \
    zip \
    libzip-dev\
    jpegoptim optipng pngquant gifsicle \
    vim \
    unzip \
    git \
    libxml2-dev \
    curl \
    mc \
    nano

# Install composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# Install extensions
RUN docker-php-ext-install pdo_mysql mbstring zip exif pcntl
RUN docker-php-ext-configure gd --with-gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ --with-png-dir=/usr/include/
RUN docker-php-ext-install gd
RUN docker-php-ext-install soap

RUN /bin/bash pecl install xdebug-2.7.2 && docker-php-ext-enable xdebug

# Add user for laravel application
RUN groupadd -g 1000 www
RUN useradd -u 1000 -ms /bin/bash -g www www

# Add node npm
RUN curl -sL https://deb.nodesource.com/setup_8.x | bash -
RUN apt-get install gcc g++ make -y
# Whatever you did in your PHP Dockerfile
# this was missing for some reason. Didn't require last time.
RUN apt-get install -y gnupg2
# Removing /var/lib/apt/lists worked
RUN rm -rf /var/lib/apt/lists/ && curl -sL https://deb.nodesource.com/setup_10.x | bash -
RUN apt-get install nodejs -y