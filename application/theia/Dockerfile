FROM node:21-bookworm-slim

ENV PUPPETEER_SKIP_DOWNLOAD=1

RUN apt-get update \
    && apt-get upgrade -y \
    && apt-get install -y pkg-config make build-essential libssl-dev libsecret-1-0 libsecret-1-dev libxkbfile-dev libx11-dev \
    && apt-get install -y libbz2-dev libreadline-dev libsqlite3-dev wget curl llvm \
    && apt-get install -y libncurses5-dev  libncursesw5-dev xz-utils tk-dev \
    && apt-get install -y python3 yarn
RUN apt-get install -y libnss3 libexpat1 libexpat1-dev libyaml-0-2 libyaml-dev libwmf-0.2-7 libwmf-dev libgcrypt20 libgcrypt20-dev

WORKDIR /home/theia
ADD package.json ./package.json
RUN yarn --pure-lockfile && \
    NODE_OPTIONS="--max_old_space_size=4096" yarn theia build && \
    yarn theia download:plugins && \
    yarn --production && \
    yarn autoclean --init && \
    echo *.ts >> .yarnclean && \
    echo *.ts.map >> .yarnclean && \
    echo *.spec.* >> .yarnclean && \
    yarn autoclean --force && \
    yarn cache clean

RUN mkdir -p /home/theia \
    && mkdir -p /home/project
ENV HOME /home/theia
WORKDIR /home/theia
EXPOSE 3000
ENV SHELL=/bin/bash \
    THEIA_DEFAULT_PLUGINS=local-dir:/home/theia/plugins
ENV USE_LOCAL_GIT true
ENTRYPOINT [ "node", "/home/theia/src-gen/backend/main.js", "/home/project", "--hostname=0.0.0.0" ]