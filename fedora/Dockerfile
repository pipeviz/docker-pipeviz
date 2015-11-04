# Fedora Dockerfile 0.1.1
#
# To use this Dockerfile, do the following:
#
# Build the docker image:
#   docker build -f Dockerfile.fedora -t pipeviz/pipeviz .
#
# Run a docker container names pipeserv using the image you just build:
#   docker run -ti -p 8008:8008 --rm --name pipeserv  pipeviz/pipeviz
#
# In a seperate shell, run a separate container to manually send input to the pipeviz server:
#   docker run -ti --link pipeserv:pipeserv --rm pipeviz/pipeviz pvutil fixr fixtures/realistic -pt http://pipeserv:2309

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
RUN make gen && \
    make install
CMD ["pipeviz", "-b"]
