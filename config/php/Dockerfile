FROM php:8.1-fpm

# Set working directory
WORKDIR /var/www

# Disable remote database security requirements.
ENV JOOMLA_INSTALLATION_DISABLE_LOCALHOST_CHECK=1

# install the PHP extensions we need.
RUN apt-get update; \
	apt-get install -y --no-install-recommends \
		libbz2-dev \
		nano \
		libjpeg-dev \
		libmagickwand-dev \
		libpq-dev \
		libpng-dev \
		libwebp-dev \
		libzip-dev \
	; \
	\
	docker-php-ext-configure gd \
		--with-jpeg \
		--with-webp \
	; \
	debMultiarch="$(dpkg-architecture --query DEB_BUILD_MULTIARCH)"; \
	docker-php-ext-install -j "$(nproc)" \
		bz2 \
		bcmath \
		exif \
		gd \
		mysqli \
		pdo_mysql \
		zip \
		pcntl \
		mbstring \
		intl \
	; \
	pecl install imagick-3.6.0; \
	docker-php-ext-enable imagick \
	intl; \
	\
# check for output like "PHP Warning:  PHP Startup: Unable to load dynamic library 'foo' (tried: ...)
	err="$(php --version 3>&1 1>&2 2>&3)"; \
	[ -z "$err" ]

RUN apt-get update && apt-get install -y \
    libicu-dev \
    libonig-dev \
    && docker-php-ext-configure intl \
    && docker-php-ext-install intl \
    && docker-php-ext-install mbstring
RUN docker-php-ext-enable intl mbstring

# Install composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# Add user
RUN groupadd -g 1000 www
RUN useradd -u 1000 -ms /bin/bash -g www www

# Copy existing application directory contents
COPY . /var/www

# Copy existing application directory permissions
COPY --chown=www:www . /var/www

# Change current user to www
USER www

# Expose port 9000 and start php-fpm server
EXPOSE 9000
CMD ["php-fpm"]