FROM php:5.6.40-apache

LABEL org.opencontainers.image.authors="alvifsandana@gmail.com"

# update & upgrade
RUN apt-get update
RUN apt-get upgrade -y

# install git curl vim zip unzip
RUN apt-get install --fix-missing -y zip unzip
RUN apt-get install --fix-missing -y git curl vim 

# install composer
COPY --from=composer:latest /usr/bin/composer /usr/bin/composer
RUN composer self-update --2

# install install-php-extensions 
ADD https://github.com/mlocati/docker-php-extension-installer/releases/latest/download/install-php-extensions /usr/local/bin/

# add execute permission
RUN chmod +x /usr/local/bin/install-php-extensions

# install docker php extensions
RUN install-php-extensions \
    bz2 calendar gd intl json \
    ldap mbstring mcrypt mysql \
    mysqli mysqlnd pdo phar posix \
    pdo_mysql pdo_sqlite \
    shmop sqlite3 sysvmsg sysvsem sysvshm \ 
    tidy tokenizer wddx xml xmlrpc xmlwriter \
    xsl zip

# edit the 'apache.conf' before copy it into image
# copy apache .conf file 
ADD conf/apache.conf /etc/apache2/sites-available/000-default.conf

RUN apt-get clean \
    && rm -r /var/lib/apt/lists/*
    
# expose port 86
EXPOSE 86

# create volume
VOLUME ["/var/www/html", "/var/log/apache2", "/etc/apache2"]


