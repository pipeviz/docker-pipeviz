FROM debian:latest
MAINTAINER Melissa Anderson <melissa@happypunch.com>

ENV GO_VERSION 1.5
ENV GOPATH /opt/go
ENV GLIDE_VERSION 0.8.3
env GO15VENDOREXPERIMENT 1
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

RUN wget -q https://github.com/Masterminds/glide/releases/download/$GLIDE_VERSION/glide-$GLIDE_VERSION-linux-amd64.tar.gz
RUN tar -C /tmp -xzf glide-$GLIDE_VERSION-linux-amd64.tar.gz
RUN cp /tmp/linux-amd64/glide /usr/local/bin

RUN useradd pipeviz
WORKDIR $GOPATH/src/github.com/pipeviz/pipeviz
RUN git clone https://github.com/pipeviz/pipeviz.git $GOPATH/src/github.com/pipeviz/pipeviz
RUN git clone https://github.com/pipeviz/webapp $GOPATH/src/github.com/pipeviz/webapp
RUN chown -R pipeviz $GOPATH
USER pipeviz
RUN make && \
    make install
CMD ["pipeviz", "-b", "--webapp-dir=../webapp/public"]