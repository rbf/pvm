ARG BASE_IMAGE_VERSION

FROM node:${BASE_IMAGE_VERSION}

WORKDIR /home/dev

# Needs to be declared after the FROM clause.
# SOURCE: 14sep2021 https://ryandaniels.ca/blog/docker-dockerfile-arg-from-arg-trouble/
ARG SECONDARY_VERSION

# SOURCE: 26sep2021 https://www.shellhacks.com/alpine-install-curl/
# DOC: https://wiki.alpinelinux.org/wiki/How_to_get_regular_stuff_working
RUN set -xe \
      && echo "alias la='ls -la'" >> /etc/profile \
      && apt-get update -y \
      && apt-get install -y libnss3-dev libgdk-pixbuf2.0-dev libgtk-3-dev libxss-dev libasound2 \
      && apt-get clean \
      && git config --global init.defaultBranch main \
      && npm install --global npm@${SECONDARY_VERSION} nodemon

CMD ["/bin/sh", "-l"]
