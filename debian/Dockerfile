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
RUN make && \
    make install
CMD ["pipeviz", "-b"]
