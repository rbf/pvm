# SOURCE: 21sep2021 https://github.com/recruitee/mix_docker
# DOC: https://docs.docker.com/develop/develop-images/multistage-build/

ARG RUBY_VERSION

FROM ruby:${RUBY_VERSION}

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
ARG RUBYONRAILS_VERSION

# SOURCE: 26sep2021 https://www.shellhacks.com/alpine-install-curl/
# DOC: https://wiki.alpinelinux.org/wiki/How_to_get_regular_stuff_working
RUN set -xe \
      && apt update -y \
      && apt install -y nodejs npm \
      && npm install --global yarn \
      && echo "alias la='ls -la'" >> /etc/bash.bashrc \
      && echo 'PATH="/home/dev/.bundle/bin:/home/dev/.bundle/global/bin:/home/preinstalled-gems/bin:${PATH}"' >> /etc/bash.bashrc \
      && git config --global init.defaultBranch main \
      && gem install --install-dir /home/preinstalled-gems rails:${RUBYONRAILS_VERSION} rubocop

CMD ["/bin/bash", "-l"]
