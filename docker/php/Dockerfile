FROM php:8.1.6-fpm

# Set working directory
WORKDIR /var/www

# Remove html folder
RUN rm -rf /var/www/html

# Install dependencies
RUN apt-get update && apt-get install -y \
    build-essential \
    libpng-dev \
    libjpeg62-turbo-dev \
    libfreetype6-dev \
    locales \
    zip \
    jpegoptim optipng pngquant gifsicle \
    vim \
    unzip \
    git \
    curl \
    libzip-dev \
    apt-utils \
    libonig-dev

# Clear cache
RUN apt-get clean && rm -rf /var/lib/apt/lists/*

# Install extensions
RUN docker-php-ext-install zip pdo_mysql mbstring exif
RUN docker-php-ext-configure gd --with-freetype=/usr/include/ --with-jpeg=/usr/include/
RUN docker-php-ext-install gd

## Redis Extension
RUN mkdir -p /usr/src/php/ext/redis; \
	curl -fsSL https://pecl.php.net/get/redis --ipv4 | tar xvz -C "/usr/src/php/ext/redis" --strip 1; \
	docker-php-ext-install redis;

# Install composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# Add user for laravel application
RUN groupadd -g 1000 laravelgroup
RUN useradd -u 1000 -ms /bin/bash -g laravelgroup laraveluser

# Copy existing application directory contents
COPY . /var/www

# Copy existing application directory permissions
COPY --chown=laraveluser:laravelgroup . /var/www

# Change current user to laraveluser
USER laraveluser

# Expose port 9000 and start php-fpm server
EXPOSE 9000
CMD ["php-fpm"]