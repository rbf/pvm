ARG BASE_IMAGE_VERSION

FROM ruby:${BASE_IMAGE_VERSION}

# Needs to be declared after the FROM clause.
# SOURCE: 14sep2021 https://ryandaniels.ca/blog/docker-dockerfile-arg-from-arg-trouble/
ARG MOUNTED_APP_ROOT_DIR_FULL_PATH
ARG CONTAINER_USER
ARG CONTAINER_USER_CONFIG_DIR_FULL_PATH
ARG SECONDARY_VERSION

# SOURCE: 15nov2021 https://github.com/alpinelab/docker-ruby-dev/blob/master/Dockerfile
ENV BUNDLE_PATH="${CONTAINER_USER_CONFIG_DIR_FULL_PATH}/.bundle"
ENV BUNDLE_BIN="${BUNDLE_PATH}/bin"
ENV BUNDLE_APP_CONFIG="${BUNDLE_PATH}/config"
ENV GEM_HOME="${BUNDLE_PATH}/global"
ENV PATH="${BUNDLE_BIN}:${GEM_HOME}/bin:${PATH}"
ENV DISABLE_SPRING="true"

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
      && apt-get install -y nodejs npm git curl \
      && apt-get clean -y \
      && npm install --global yarn \
      && gem install --install-dir /home/preinstalled-gems bundler:'~>2.0' || true \
      && gem install --install-dir /home/preinstalled-gems bundler:'~>1.0' \
      && gem install --install-dir /home/preinstalled-gems rails:${SECONDARY_VERSION}

WORKDIR ${MOUNTED_APP_ROOT_DIR_FULL_PATH}

CMD ["/bin/bash", "-l"]
