FROM php:8.4-apache

# 必要なパッケージとPHP拡張モジュールのインストール
RUN apt-get update && apt-get install -y \
    git \
    zip \
    unzip \
    libpng-dev \
    libonig-dev \
    libxml2-dev \
    libzip-dev \
 && docker-php-ext-install pdo_mysql mbstring gd zip bcmath

# xdebugのインストールと有効化
RUN pecl install xdebug \
 && docker-php-ext-enable xdebug

# Node.js 22 LTSを追加
RUN curl -fsSL https://deb.nodesource.com/setup_22.x | bash - \
    && apt-get install -y nodejs

# Apacheの mod_rewrite モジュールを有効化（Laravelのルーティングに必須）
RUN a2enmod rewrite

# Apacheのドキュメントルート設定を上書き
COPY apache/000-default.conf /etc/apache2/sites-available/000-default.conf

# Composerの導入
COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

WORKDIR /var/www/html