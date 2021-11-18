ARG BASE_IMAGE_VERSION

FROM ruby:${BASE_IMAGE_VERSION}

WORKDIR /home/dev

# SOURCE: 15nov2021 https://github.com/alpinelab/docker-ruby-dev/blob/master/Dockerfile
ENV BUNDLE_PATH="/home/dev/.bundle" \
    BUNDLE_BIN="/home/dev/.bundle/bin" \
    BUNDLE_APP_CONFIG="/home/dev/.bundle" \
    GEM_HOME="/home/dev/.bundle/global" \
    PATH="/home/dev/.bundle/bin:/home/dev/.bundle/global/bin:${PATH}" \
    HISTFILE="/home/dev/.config/.zsh_history" \
    DISABLE_SPRING="true"

# Needs to be declared after the FROM clause.
# SOURCE: 14sep2021 https://ryandaniels.ca/blog/docker-dockerfile-arg-from-arg-trouble/
ARG SECONDARY_VERSION

# SOURCE: 26sep2021 https://www.shellhacks.com/alpine-install-curl/
# DOC: https://wiki.alpinelinux.org/wiki/How_to_get_regular_stuff_working
RUN set -xe \
      && apt update -y \
      && apt install -y nodejs npm git curl \
      && npm install --global yarn \
      && echo "alias la='ls -la'" >> /etc/bash.bashrc \
      && git config --global init.defaultBranch main \
      && gem install --install-dir /home/preinstalled-gems bundler:'~>2.0' || true \
      && gem install --install-dir /home/preinstalled-gems bundler:'~>1.0' \
      && gem install --install-dir /home/preinstalled-gems rails:${SECONDARY_VERSION}

CMD ["/bin/bash", "-l"]
