# Set base image
FROM php:8.2-fpm

# Set timezone argument
ARG TIMEZONE

# Copy php configuration file
COPY php.ini /usr/local/etc/php/conf.d/docker-php-config.ini

# Install necessary packages
RUN apt-get update && apt-get install -y \
    gnupg \
    g++ \
    procps \
    openssl \
    git \
    unzip \
    zlib1g-dev \
    libzip-dev \
    libfreetype6-dev \
    libpng-dev \
    libjpeg-dev \
    libicu-dev  \
    libonig-dev \
    libxslt1-dev \
    acl

# Configure and install php extensions
RUN docker-php-ext-configure gd --with-jpeg --with-freetype \
    && docker-php-ext-install \
        pdo pdo_mysql zip xsl gd intl opcache exif mbstring

# Configure and install pcntl extension
RUN docker-php-ext-configure pcntl --enable-pcntl \
    && docker-php-ext-install pcntl

# Install the Imagick extension
RUN apt-get install -y libmagickwand-dev; \
    pecl install imagick; \
    docker-php-ext-enable imagick;

# Set timezone
RUN ln -snf /usr/share/zoneinfo/${TIMEZONE} /etc/localtime && echo ${TIMEZONE} > /etc/timezone \
    && printf '[PHP]\ndate.timezone = "%s"\n', ${TIMEZONE} > /usr/local/etc/php/conf.d/tzone.ini \
    && "date"

# Install Composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# Install npm and set configurations
# https://nodejs.org/en/download - Linux Binaries (x64)	
RUN curl https://nodejs.org/dist/v18.16.0/node-v18.16.0-linux-x64.tar.xz --output node.tar.xz \
    && tar -xf node.tar.xz \
    && mv node-v18.16.0-linux-x64/bin/* /usr/local/bin/ \
    && mv node-v18.16.0-linux-x64/lib/node_modules/ /usr/local/lib/ \
    && rm node.tar.xz && rm -r node-v18.16.0-linux-x64 \
    && npm install -g npm@latest \
    && npm config set fund false --location=global


# Set the working directory
WORKDIR /var/www