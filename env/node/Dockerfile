# SOURCE: 21sep2021 https://github.com/recruitee/mix_docker
# DOC: https://docs.docker.com/develop/develop-images/multistage-build/

ARG NODE_VERSION

FROM node:${NODE_VERSION}

WORKDIR /home/dev

# SOURCE: 26sep2021 https://www.shellhacks.com/alpine-install-curl/
# DOC: https://wiki.alpinelinux.org/wiki/How_to_get_regular_stuff_working
RUN set -xe \
      && echo "alias la='ls -la'" >> /etc/profile \
      && apk --no-cache add git curl util-linux bash \
      && git config --global init.defaultBranch main \
      && npm install -g npm

CMD ["/bin/sh", "-l"]
