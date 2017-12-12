Introduction
============

This repository  contains the Dockerfile used to create a Docker image capable
of building Sherpa conda packages for compatibility with CentOS 5 systems.

The repository is linked to a
[Docker Hub](https://hub.docker.com/r/sherpadev/legacy-builds/) repository and
images are built automatically at each commit.

This is not a supported product, but an effort to help those Sherpa users who
need back-porting Sherpa on an unsupported platform.

At this point the only platform supported is CentOS 5.

This repo also contains conda recipes for the 4.9.1 build, which could be edited to
build future versions of Sherpa. Alternatively, you can pass the container the path
to a custom conda recipe which will be built instead.

There is no guarantee that future versions of Sherpa can be built on these
Docker images without additional changes.

How to run the image
====================

On a system with Docker installed, to build the default package use
(assuming a `bash` shell):

```
$ git clone https://github.com/sherpa/legacy-builds
$ cd legacy-builds
$ docker run -v $(pwd):/opt/project sherpadev/legacy-builds
```

The `latest` tag points to the latest build from the master branch. Additionally,
tags are provided for each individual platform being targeted.

The only tag currently available is `centos5`.

The output of the build will be copied inside the `/opt/project/output` folder, so
in order to fetch it you need to bind the `/opt/project` volume to a local folder.

By default the container will look for a conda recipe in `/opt/project/recipes/sherpa.conda`.

The easiest way to customize the build is to simply edit the recipe in that folder.

Alternatively you can override the default path, as long as the recipe is inside the volume. For instance,
assuming the local folder `/home/user/sherpa-recipes` contains a recipe in the `sherpa-4.9.1` subfolder,
you can:

```
$ cd /home/user/sherpa-recipes
$ docker run -v $(pwd):/opt/project sherpadev/legacy-builds /opt/project/sherpa-4.9.1
```

The resulting conda package will be created in `/home/user/sherpa-recipes/output`.

