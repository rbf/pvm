ARG BASE_IMAGE_VERSION

FROM php:${BASE_IMAGE_VERSION}

# Needs to be declared after the FROM clause.
# SOURCE: 14sep2021 https://ryandaniels.ca/blog/docker-dockerfile-arg-from-arg-trouble/
ARG MOUNTED_APP_ROOT_DIR_FULL_PATH
ARG CONTAINER_USER
ARG CONTAINER_USER_CONFIG_DIR_FULL_PATH
ARG SECONDARY_VERSION

# SOURCE: 18nov2021 https://getcomposer.org/doc/03-cli.md#composer-home
ENV COMPOSER_HOME="${CONTAINER_USER_CONFIG_DIR_FULL_PATH}/.composer"
ENV PATH="${COMPOSER_HOME}/vendor/bin:${PATH}"

RUN set -xe \
      && adduser --disabled-password --gecos '' ${CONTAINER_USER} \
      && echo "alias la='ls -la'" >> /etc/bash.bashrc \
      && echo 'uname --all' >> /etc/bash.bashrc \
      && echo '(source /etc/os-release; echo ${PRETTY_NAME} - \(cat /etc/os-release for details\))' >> /etc/bash.bashrc \
      && apt-get update -y \
      && apt-get install -y git zip unzip \
      && apt-get clean -y \
      && git config --global init.defaultBranch main

RUN set -xe \
      && apt-get install -y php-zip || true \
      && apt-get clean -y \
      && curl -sSL https://raw.githubusercontent.com/composer/getcomposer.org/main/web/installer | php -- --version="${SECONDARY_VERSION}" \
      && mv composer.phar /usr/local/bin/composer \
      && mkdir -p /home/preinstalled/.composer \
      && composer --working-dir="/home/preinstalled/.composer" global require laravel/installer

WORKDIR ${MOUNTED_APP_ROOT_DIR_FULL_PATH}

CMD ["/bin/bash", "-l"]
