# Use a imagem PHP como base
FROM php:latest

# Instale algumas extensões e dependências úteis
RUN apt-get update && apt-get install -y --no-install-recommends \
    libzip-dev \
    git \
    zip \
    unzip

RUN docker-php-ext-install zip pdo_mysql

# Copie o Composer da imagem Composer oficial
COPY --from=composer:latest /usr/bin/composer /usr/local/bin/composer

# Instale o Laravel Installer globalmente
RUN composer global require laravel/installer

# Adicione o diretório global do Composer ao PATH
ENV PATH="${PATH}:/root/.composer/vendor/bin"

# Defina um diretório de trabalho
WORKDIR /var/www/html

# Execute o comando 'tail -f /dev/null' para manter o contêiner em execução
CMD ["tail", "-f", "/dev/null"]