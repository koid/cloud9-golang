FROM node:slim
RUN apt-get update \
 && apt-get autoremove -y \
 && apt-get upgrade -y \
 && apt-get install -y git curl python make gcc vim locales locales-all \
 && apt-get clean
RUN locale-gen ja_JP.UTF-8
ENV LANG=ja_JP.UTF-8 \
    LANGUAGE=ja_JP.UTF-8 \
    LC_CTYPE=ja_JP.UTF-8 \
    LC_ALL=ja_JP.UTF-8

WORKDIR /
RUN git clone https://github.com/c9/core.git /c9 \
 && /c9/scripts/install-sdk.sh

ENV GOVERSION=1.14 \
    LINTVERSION=v1.23.8 \
    GOROOT=/usr/local/go \
    GOPATH=/go
WORKDIR /usr/local/src
RUN curl https://dl.google.com/go/go${GOVERSION}.linux-amd64.tar.gz -o go${GOVERSION}.linux-amd64.tar.gz \
 && tar -xvf go${GOVERSION}.linux-amd64.tar.gz -C /usr/local \
 && curl -sfL https://install.goreleaser.com/github.com/golangci/golangci-lint.sh \
    | sh -s -- -b $(go env GOROOT)/bin ${LINTVERSION} \
 && ln -s /usr/local/go/bin/go* /usr/local/bin/.

ENV USERNAME user
ENV PASSWORD pass
EXPOSE 8080
ENTRYPOINT ["sh", "-c", "/usr/local/bin/node /c9/server.js -l 0.0.0.0 -p 8080 -w $GOPATH -a $USERNAME:$PASSWORD"]
