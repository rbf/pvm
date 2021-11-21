ARG BASE_IMAGE_VERSION

FROM node:${BASE_IMAGE_VERSION}

# Needs to be declared after the FROM clause.
# SOURCE: 14sep2021 https://ryandaniels.ca/blog/docker-dockerfile-arg-from-arg-trouble/
ARG MOUNTED_APP_ROOT_DIR_FULL_PATH
ARG CONTAINER_USER
ARG CONTAINER_USER_CONFIG_DIR_FULL_PATH
ARG SECONDARY_VERSION

# DOC: https://docs.npmjs.com/cli/v8/configuring-npm/folders
# SOURCE: 21nov2021 https://stackoverflow.com/questions/40178366/how-to-change-the-npm-prefix-without-config
ENV CUSTOM_NODE_PREFIX="${CONTAINER_USER_CONFIG_DIR_FULL_PATH}/.node"
ENV PATH="${CUSTOM_NODE_PREFIX}/bin:${PATH}"

RUN set -xe \
      && adduser --disabled-password --gecos '' ${CONTAINER_USER} \
      && echo "alias la='ls -la'" >> /etc/bash.bashrc \
      && echo 'uname --all' >> /etc/bash.bashrc \
      && echo '(source /etc/os-release; echo ${PRETTY_NAME} - \(cat /etc/os-release for details\))' >> /etc/bash.bashrc \
      && apt-get update -y \
      && apt-get install -y make git zip unzip less vim \
      && apt-get clean -y \
      && git config --global init.defaultBranch main

RUN set -xe \
      && apt-get install -y libnss3-dev libgdk-pixbuf2.0-dev libgtk-3-dev libxss-dev libasound2 \
      && apt-get clean -y \
      && npm config set prefix /home/preinstalled-node-prefix \
      && npm install --global npm@${SECONDARY_VERSION} \
      && npm install --global nodemon eslint

USER ${CONTAINER_USER}

RUN set -xe \
      && npm config set prefix "${CUSTOM_NODE_PREFIX}" \

WORKDIR ${MOUNTED_APP_ROOT_DIR_FULL_PATH}

CMD ["/bin/bash", "-l"]
