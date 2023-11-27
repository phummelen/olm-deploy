FROM php:8.1.10-fpm

WORKDIR /app

# Arguments defined in docker-compose.yml
ARG user=laravel
ARG uid=1000

# Install system dependencies
RUN apt-get update && apt-get install -y \
    git \
    curl \
    libpng-dev \
    libonig-dev \
    libxml2-dev \
    libzip-dev \
    libwebp-dev \
    libjpeg62-turbo-dev \
    libxpm-dev \
    libfreetype6-dev \
    zip \
    unzip \
    redis-tools \
    default-mysql-client \
    vim

# Clear cache
RUN apt-get clean && rm -rf /var/lib/apt/lists/*

# Install PHP extensions
RUN docker-php-ext-configure gd --with-jpeg --with-freetype
RUN docker-php-ext-install pdo_mysql mbstring exif pcntl bcmath gd zip

# Get latest Composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# Create system user to run Composer and Artisan Commands
RUN useradd -G www-data,root -u $uid -d /home/$user $user
RUN mkdir -p /home/$user/.composer \
    && chown -R $user:$user /home/$user \
    && chown -R $user:$user /app

COPY --chown=$user olm-web/. /app
COPY --chown=$user olm-web/.env.dockerimage /app/.env

#ENV COMPOSER_ALLOW_SUPERUSER=1

#RUN composer audit && composer suggest
#RUN composer update --no-scripts && composer install --no-dev --no-progress --no-autoloader --audit --prefer-dist --verbose
#RUN composer dump-autoload
RUN composer install --optimize-autoloader --no-dev
RUN php artisan config:clear && php artisan cache:clear
RUN php artisan horizon:publish
RUN php artisan key:generate
#RUN composer update

#USER $user

#EXPOSE 9000
CMD php artisan serve --host=0.0.0.0 --port=9000
