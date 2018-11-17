[![Codefresh build status]( https://g.codefresh.io/api/badges/pipeline/lirantal/lirantal%2Fdocker-travis-cli%2Fdocker-travis-cli?branch=master&key=eyJhbGciOiJIUzI1NiJ9.NTgxMjdkMTU3MzhhYTMwMTAwMjg2YWY4.4TkcAYZuKIcjt2ELMIndMUYK3L0pzZWErAzRnRGlDnE&type=cf-1)]( https://g.codefresh.io/pipelines/docker-travis-cli/builds?repoOwner=lirantal&repoName=docker-travis-cli&serviceName=lirantal%2Fdocker-travis-cli&filter=trigger:build~Build;branch:master;pipeline:5bf043d341859180ee3f5e4d~docker-travis-cli)
[![](https://images.microbadger.com/badges/version/lirantal/travis-cli.svg)](https://microbadger.com/images/lirantal/travis-cli "Get your own version badge on microbadger.com")
[![](https://images.microbadger.com/badges/image/lirantal/travis-cli.svg)](https://microbadger.com/images/lirantal/travis-cli "Get your own image badge on microbadger.com")




# About

One may often need to invoke the Travis CLI such as for encrypting environment variables for Travis CI, yet that requires to use
travis's ruby binary, and hence requires a ruby runtime.

This small docker image exposes the travis CLI so that it is easily accessible and isolated
inside of a docker container, leaving you out of the need to set it up yourself.


# Usage

The docker image already has ruby and the `travis` gem installed so it can execute any
commands for the Travis CLI.

The image's entrypoint is set to the `travis` executable so any command line arguments
appended to `docker run` will be added to that, providing easy access to users.

## Encrypting environment variables

When encrypting something, the travis cli needs a way to know what travis repository
you are encrypting for so it can use the correct private key. This is either done by
being in the project's git repository which has the details, or providing a `-r <owner>/<repo>`
argument that specifies this.

This docker image uses the latter as a more verbose and flexible option to encrypt
environment variables.

Example:

```
docker run --rm lirantal/travis-cli encrypt ENV_VARIABLE_NAME="GH_TOKEN_GOES_HERE" -r lirantal/dockly
```

Documentation Resources:
* [travis keys encryption](https://docs.travis-ci.com/user/encryption-keys/)

## Linting a .travis.yml file

Add the lint command option and the path to the `.travis.yml`:

```
docker run --rm lirantal/travis-cli lint .travis.yml
```

# Contributing

You're welcome to suggest any changes and/or improvements by updating the Dockerfile or any other
idea you may have.

Building the image from the Dockerfile and then you may execute it locally:

```
docker build --tag lirantal/travis-cli .
```

# Author
Liran Tal <liran.tal@gmail.com>
