FROM fedora:latest
MAINTAINER Melissa Anderson <melissa@happypunch.com>

ENV GO_VERSION 1.5
ENV GOPATH /opt/go
ENV PATH /usr/local/go/bin:$GOPATH/bin:$PATH

RUN dnf install -y \
    python-pygit2 \
    wget \
    git \
    make \
    nodejs \
    npm \
    tar
RUN wget https://storage.googleapis.com/golang/go$GO_VERSION.linux-amd64.tar.gz
RUN tar -C /usr/local -xzf go$GO_VERSION.linux-amd64.tar.gz
RUN useradd pipeviz
RUN git clone https://github.com/pipeviz/pipeviz.git $GOPATH/src/github.com/pipeviz/pipeviz
RUN chown -R pipeviz $GOPATH
USER pipeviz
WORKDIR $GOPATH/src/github.com/pipeviz/pipeviz
RUN make && \
    make install
CMD ["pipeviz", "-b"]
