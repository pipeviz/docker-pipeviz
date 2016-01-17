FROM fedora:latest
MAINTAINER Melissa Anderson <melissa@happypunch.com>

ENV GO_VERSION 1.5
ENV GOPATH /opt/go
ENV GLIDE_VERSION 0.8.3
env GO15VENDOREXPERIMENT 1
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

RUN wget -q https://github.com/Masterminds/glide/releases/download/$GLIDE_VERSION/glide-$GLIDE_VERSION-linux-amd64.tar.gz
RUN tar -C /tmp -xzf glide-$GLIDE_VERSION-linux-amd64.tar.gz
RUN cp /tmp/linux-amd64/glide /usr/local/bin

RUN useradd pipeviz
RUN git clone https://github.com/pipeviz/pipeviz.git $GOPATH/src/github.com/pipeviz/pipeviz
RUN chown -R pipeviz $GOPATH
USER pipeviz
WORKDIR $GOPATH/src/github.com/pipeviz/pipeviz
RUN make && \
    make install
CMD ["pipeviz", "-b"]
