# What is Pipeviz?
Pipeviz is a system for visualizing what you need to know as a
software-driven organization: your development workflow, the state of your
infrastructure, and more. It's a database and visualization webapp rolled
into one, informed by an ecosystem of agents and other message producers.

See the [Pipeviz Github](https://github.com/pipeviz/pipeviz#pipeviz) repository for more information.

The two Dockerfiles currently included in the pipeviz-docker repository are
primarily to verify on update to the master branch of Pipeviz that the
project builds successfully on both Debian and Fedora operating systems. The
`latest` build defaults to Debian.

The images are suitable for demonstration and testing by using pre-created
fixtures included in the Pipeviz repository.

## Pull the image:

   docker pull pipeviz/pipeviz:latest
OR
   docker pull pipeviz/pipeviz:fedora-latest

## Run a docker container named pipeserv using the image build above:
    docker run -ti -p 8008:8008 --rm --name pipeserv pipeviz/pipeviz

The Pipeviz instance should be accessible in your host environment at
`http://localhost:8008`.

## To send test data:
Once the Pipeviz daemon is running, you can manually send input to the daemon
from a separate container with:

    docker run -ti --link pipeserv:pipeserv --rm pipeviz/pipeviz \
    pvutil fixr fixtures/realistic/ -t http://pipeserv:2309


