# Mathics Dockerized

## About

This is a [dockerized](https://www.docker.com/) environment for [rebcabin's fork](https://github.com/rebcabin/Mathics) of [mathics](https://mathics.github.io):

> A free, light-weight alternative to Mathematica.


## How it works

This environment runs through an entrypoint that supports two modes:

- command-line - [mathics](https://github.com/mathics/Mathics/wiki/Installing#running-mathics)
- web-ui - [mathicsserver](https://github.com/mathics/Mathics/wiki/Installing#running-mathics)

`PROJECT_ROOT/app/data` folder will be mapped to `/usr/src/app/data` inside docker container. All files in that folder are shared between host and container.

web-ui mode and command-line mode can run simultaneously in two separate docker containers. Simply run container in one mode first and another container in the other mode.


### entrypoint parameters

See `docker-compose` and `docker` sections below, which explain how to run a mathics container. Mathics container runs through the entrypoint. Run the a container with `--help` at the end to see a complete list of options supported by the container.


### docker-compose

docker-compose will pull all necessary images and build the target image automatically before the first run.

#### command-line

    $ cd PROJECT_ROOT
    $ docker-compose run --rm mathics --mode cli

#### web-ui

    $ cd PROJECT_ROOT
    $ docker-compose run --service-ports --rm mathics --mode ui

Mathics server will be available at <http://localhost:8000>


### docker

Target image has to be built manually with bare docker.

#### building

    $ cd PROJECT_ROOT
    $ docker build -t rebcabin/mathics app

#### running command-line

    $ docker run --rm -it --name rebcabin-mathics -v PROJECT_ROOT/app/data:/usr/src/app/data rebcabin/mathics --mode cli

#### running web-ui

    $ docker run --rm -it --name rebcabin-mathics -p 8000:8000 -v PROJECT_ROOT/app/data:/usr/src/app/data rebcabin/mathics --mode ui


## Mathics Documentation

To access documentation, start in web-ui mode, open <http://localhost:8000> in a browser and start searching.
