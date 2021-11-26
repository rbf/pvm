# pvm - Polyglot Version Manager

A polyglot version manager leveraging Docker. It currently supports:

  - [clojure](https://clojure.org/guides/getting_started) (default version based on image `clojure:openjdk-18-tools-deps-1.10.3.1020-bullseye`)
  - [elixir](https://elixir-lang.org/getting-started/introduction.html) (default version based on image `elixir:1.12.3`)
  - [golang](https://golang.org/doc/tutorial/getting-started) (default version based on image `golang:1.17.3-bullseye`)
  - [node](https://nodejs.org/en/docs/guides/getting-started-guide/) (default version [based on image `node:17.1.0-bullseye`)
  - [php](https://www.php.net/manual/en/getting-started.php) (default version based on image `php:8.0.12-bullseye`)
  - [ruby](http://www.ruby-lang.org/en/documentation/) (default version based on image `ruby:3.0.2-bullseye`)
  - [rust](https://www.rust-lang.org/learn/get-started) (default version based on image `rust:1.56.1-bullseye`)

All base images are official language images from [DockerHub][dhi].

[dhi]: https://hub.docker.com/search?type=image&category=languages&image_filter=official

## Install

Currently `pvm` only works for Zshell and on macOS. Bash and Linux compatibility
might come in the future.

It can be installed with `brew`:

  - `brew install rbf/tap/pvm`

