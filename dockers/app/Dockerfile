FROM ruby:3.0.1

COPY Gemfile* ./

WORKDIR /app

RUN apt install -y curl && \
    curl -sL https://deb.nodesource.com/setup_lts.x \
    curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add - \
    echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list

RUN apt-get update && \
    apt-get install -y git-core zlib1g-dev build-essential libssl-dev libreadline-dev \
    libyaml-dev libsqlite3-dev sqlite3 libxml2-dev libxslt1-dev libcurl4-openssl-dev \
    software-properties-common libffi-dev nodejs yarn

ENV BUNDLE_BIN=/bundle/bin

RUN gem install bundler -v 2.3.21

RUN bundle install

RUN bundle config set --local path /bundle

COPY dockers/app/*.sh /scripts/

RUN chmod a+x /scripts/*.sh
