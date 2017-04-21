# tox-docker

A plugin for [tox](https://tox.readthedocs.io/en/latest/) which runs one or
more [Docker](https://www.docker.com/) containers during the test run.

## Configuration

In the `testenv` section, list the Docker images you want to include in
the `docker` multi-line-list. Be sure to include the version tag.

You can include environment variables to be passed to the docker container
via the `dockerenv` multi-line list. These will also be made available to
your test suite as it runs, as ordinary environment variables:

    [testenv]
    docker =
        postgres:9-alpine
    dockerenv =
        POSTGRES_USER=username
        POSTGRES_DB=dbname

## Port Mapping

tox-docker runs docker with the "publish all ports" option. Any port the
container exposes will be made available to your test suite via environment
variables of the form `<image-basename>_<exposed-port>_<proto>`. For
instance, for the postgresql container, there will be an environment
variable `POSTGRES_5432_TCP` whose value is the ephemeral port number that
docker has bound the container's port 5432 to.

## Publishing to DevPI

Floodgate, etc.
