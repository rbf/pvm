ARG BASE_IMAGE_VERSION

FROM python:${BASE_IMAGE_VERSION}

# Needs to be declared after the FROM clause.
# SOURCE: 14sep2021 https://ryandaniels.ca/blog/docker-dockerfile-arg-from-arg-trouble/
ARG MOUNTED_APP_ROOT_DIR_FULL_PATH
ARG CONTAINER_USER
ARG CONTAINER_USER_CONFIG_DIR_FULL_PATH
ARG SECONDARY_VERSION

# # https://docs.python.org/3/using/cmdline.html#environment-variables
# SOURCE: 26nov2021 https://stackoverflow.com/a/24425357
# FIXME: 26nov2021 Properly configure env vars to point python folders to ${CONTAINER_USER_CONFIG_DIR_FULL_PATH}
# ENV PYTHONHOME="${CONTAINER_USER_CONFIG_DIR_FULL_PATH}"
# ENV PYTHONPATH="${PYTHONHOME}:/usr/local/lib/python3.10/:${PYTHONPATH}"
# ENV PYTHONUSERBASE="${CONTAINER_USER_CONFIG_DIR_FULL_PATH}"
# ENV PYTHONUSERSITE="${PYTHONUSERBASE}/lib/site-packages"

RUN set -xe \
      && adduser --disabled-password --gecos '' ${CONTAINER_USER} \
      && echo "alias la='ls -la'" >> /etc/bash.bashrc \
      && echo 'uname --all' >> /etc/bash.bashrc \
      && echo '(source /etc/os-release; echo ${PRETTY_NAME} - \(cat /etc/os-release for details\))' >> /etc/bash.bashrc \
      && apt-get update -y \
      && apt-get install -y make man curl wget git zip unzip less vim \
      && apt-get clean -y \
      && git config --global init.defaultBranch main

RUN set -xe \
      && /usr/local/bin/python -m pip install --upgrade pip

WORKDIR ${MOUNTED_APP_ROOT_DIR_FULL_PATH}

CMD ["/bin/bash", "-l"]
