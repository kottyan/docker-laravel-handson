# ベースイメージを指定
FROM php:7.3.7-fpm-alpine
# 作者を指定
LABEL maintainer "your-name"

# docker-compose.ymlの引数を受け取る
ARG TZ
ENV COMPOSER_ALLOW_SUPERUSER 1
ENV COMPOSER_HOME /composer

# RUNで必要なライブラリをインストール(追加ライブラリはここへ)
# RUNコマンドの数だけレイヤーができてしまう
# e 異常ステータスは即座に終了　u 未割り当ての変数はエラー　x コマンドを実行したときコマンドと引数を表示

RUN set -eux && \
  apk add --update-cache --no-cache --virtual=.build-dependencies tzdata && \
  cp /usr/share/zoneinfo/${TZ} /etc/localtime && \
  apk del .build-dependencies && \
  docker-php-ext-install bcmath pdo_mysql && \
  curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/bin --filename=composer && \
  composer config -g repos.packagist composer https://packagist.jp && \
  composer global require hirak/prestissimo