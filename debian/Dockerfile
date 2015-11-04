# Pipeviz Dockerfile 0.1.1
#
# To use this Dockerfile, do the following:
#
# Build a docker image tagged pipeviz:
#   docker build -f Dockerfile.debian -t pipeviz/pipeviz .
#
# Run a docker container named pipeserv using the image you just built:
#   docker run -ti -p 8008:8008 --rm --name pipeserv pipeviz/pipeviz
#
# In a seperate shell, run a separate container to manually send input to the pipeviz server:
#   docker run -ti --link pipeserv:pipeserv --rm pipeviz/pipeviz pvutil fixr fixtures/realistic/ -t http://pipeserv:2309

FROM debian:latest
MAINTAINER Melissa Anderson <melissa@happypunch.com>

ENV GO_VERSION 1.5
ENV GOPATH /opt/go
ENV PATH /usr/local/go/bin:$GOPATH/bin:$PATH

RUN apt-get update && apt-get install -y --no-install-recommends \
    wget \
    git \
    nodejs-legacy \
    npm \
    make \
    && rm -rf /var/lib/apt/lists/*
RUN wget -q https://storage.googleapis.com/golang/go$GO_VERSION.linux-amd64.tar.gz
RUN tar -C /usr/local -xzf go$GO_VERSION.linux-amd64.tar.gz
RUN useradd pipeviz
WORKDIR $GOPATH/src/github.com/pipeviz/pipeviz
RUN git clone https://github.com/pipeviz/pipeviz.git $GOPATH/src/github.com/pipeviz/pipeviz
RUN chown -R pipeviz $GOPATH
USER pipeviz
RUN make gen && \
    make install
CMD ["pipeviz", "-b"]