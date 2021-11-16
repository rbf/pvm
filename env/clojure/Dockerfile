ARG BASE_IMAGE_VERSION

FROM clojure:${BASE_IMAGE_VERSION}

WORKDIR /home/dev

# Needs to be declared after the FROM clause.
# SOURCE: 14sep2021 https://ryandaniels.ca/blog/docker-dockerfile-arg-from-arg-trouble/
ARG SECONDARY_VERSION

# SOURCE: 26sep2021 https://www.shellhacks.com/alpine-install-curl/
# DOC: https://wiki.alpinelinux.org/wiki/How_to_get_regular_stuff_working
RUN set -xe \
      && echo "alias la='ls -la'" >> /etc/profile \
      && git config --global init.defaultBranch main \
      && apt update -y \
      && apt install -y leiningen=${SECONDARY_VERSION}* \
      && lein repl

CMD ["/bin/sh", "-l"]
