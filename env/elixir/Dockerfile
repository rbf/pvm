ARG BASE_IMAGE_VERSION

FROM elixir:${BASE_IMAGE_VERSION}

# Needs to be declared after the FROM clause.
# SOURCE: 14sep2021 https://ryandaniels.ca/blog/docker-dockerfile-arg-from-arg-trouble/
ARG MOUNTED_APP_ROOT_DIR_FULL_PATH
ARG CONTAINER_USER
ARG CONTAINER_USER_CONFIG_DIR_FULL_PATH
ARG SECONDARY_VERSION

RUN set -xe \
      && adduser --disabled-password --gecos '' ${CONTAINER_USER} \
      && echo "alias la='ls -la'" >> /etc/bash.bashrc \
      && echo 'uname --all' >> /etc/bash.bashrc \
      && echo '(source /etc/os-release; echo ${PRETTY_NAME} - \(cat /etc/os-release for details\))' >> /etc/bash.bashrc \
      && apt-get update -y \
      && apt-get install -y make git zip unzip less vim \
      && apt-get clean -y \
      && git config --global init.defaultBranch main

USER ${CONTAINER_USER}

RUN set -xe \
      && git clone https://github.com/dependabot/elixir-security-advisories.git ~/.local/share/elixir-security-advisories \
      && mix local.hex --force \
      && mix local.rebar --force \
      && mix archive.install hex phx_new ${SECONDARY_VERSION} --force

WORKDIR ${MOUNTED_APP_ROOT_DIR_FULL_PATH}

CMD ["/bin/bash", "-l"]
