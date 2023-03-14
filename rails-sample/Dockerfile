FROM ruby:latest

RUN apt update && apt install -y \
    build-essential \
    libpq-dev \
    nodejs \
    postgresql-client \
    yarn

WORKDIR /product-register

# GemfileとGemfile.lockをコピーして、コンテナでインストールする
COPY Gemfile Gemfile.lock /product-register/

RUN bundle install