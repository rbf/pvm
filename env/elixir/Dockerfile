# SOURCE: 21sep2021 https://github.com/recruitee/mix_docker
# DOC: https://docs.docker.com/develop/develop-images/multistage-build/

ARG ELIXIR_VERSION

FROM elixir:${ELIXIR_VERSION}

WORKDIR /home/dev

# Needs to be declared after the FROM clause.
# SOURCE: 14sep2021 https://ryandaniels.ca/blog/docker-dockerfile-arg-from-arg-trouble/
ARG PHOENIX_VERSION

# SOURCE: 26sep2021 https://www.shellhacks.com/alpine-install-curl/
# DOC: https://wiki.alpinelinux.org/wiki/How_to_get_regular_stuff_working
RUN set -xe \
      && echo "alias la='ls -la'" >> /etc/profile \
      && apk --no-cache add git curl util-linux bash \
      && git config --global init.defaultBranch main \
      && git clone https://github.com/dependabot/elixir-security-advisories.git /root/.local/share/elixir-security-advisories \
      && mix local.hex --force \
      && mix local.rebar --force \
      && mix archive.install hex phx_new ${PHOENIX_VERSION} --force

CMD ["/bin/sh", "-l"]
