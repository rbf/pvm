ARG BASE_IMAGE_VERSION

FROM php:${BASE_IMAGE_VERSION}

WORKDIR /home/dev

# SOURCE: 18nov2021 https://getcomposer.org/doc/03-cli.md#composer-home
ENV COMPOSER_HOME=/home/dev/.composer \
    PATH="/home/dev/.composer/vendor/bin:${PATH}"

# Needs to be declared after the FROM clause.
# SOURCE: 14sep2021 https://ryandaniels.ca/blog/docker-dockerfile-arg-from-arg-trouble/
ARG SECONDARY_VERSION

RUN set -xe \
      && echo "alias la='ls -la'" >> /etc/bash.bashrc \
      && apt-get update -y \
      && apt-get install -y git zip unzip \
      && apt-get install -y php-zip || true \
      && curl -sSL https://raw.githubusercontent.com/composer/getcomposer.org/main/web/installer | php -- --version="${SECONDARY_VERSION}" \
      && mv composer.phar /usr/local/bin/composer \
      && mkdir -p /home/preinstalled/.composer \
      && composer --working-dir="/home/preinstalled/.composer" global require laravel/installer

CMD ["/bin/bash", "-l"]
