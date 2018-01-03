FROM php:7.1.0-fpm


#安装php扩展

RUN pecl install redis-3.1.0 && \
    docker-php-ext-enable redis

#安装composer

RUN curl -sS https://getcomposer.org/installer | php && \
    mv composer.phar /usr/local/bin/composer && \
    chmod -R +x /usr/local/bin/composer && \
    echo "" >> ~/.bashrc && \
    echo 'export PATH="~/.composer/vendor/bin:$PATH"' >> ~/.bashrc

RuN apt-get update && apt-get install -y zlib1g-dev

RUN docker-php-ext-install zip

RUN docker-php-ext-install pdo_mysql
