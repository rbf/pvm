ARG BASE_IMAGE_VERSION

FROM rust:${BASE_IMAGE_VERSION}

WORKDIR /home/dev

# SOURCE: 16nov2021 https://www.digitalocean.com/community/tutorials/understanding-the-gopath
ENV GOPATH="/home/dev/.gopath"

RUN set -xe \
      && echo "alias la='ls -la'" >> /etc/bash.bashrc \
      && echo 'PATH="${GOPATH}:${PATH}"' >> /etc/bash.bashrc

CMD ["/bin/bash", "-l"]
