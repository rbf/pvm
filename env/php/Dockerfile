ARG BASE_IMAGE_VERSION

FROM php:${BASE_IMAGE_VERSION}

WORKDIR /home/dev

RUN set -xe \
      && echo "alias la='ls -la'" >> /etc/bash.bashrc

CMD ["/bin/bash", "-l"]
