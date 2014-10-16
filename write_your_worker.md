# How to write a dolater.io worker

This document will guide you through the creation of a *dolater.io* worker.

We have some [templates](https://github.com/dolaterio/templates) in different languages with the simplest structure for your worker.

## Configuration via environment variables

All configuration for your worker should be stored in environment variables.

Environment variables can be set (1) within your worker image or (2) in the job.

## Send job-specific data via STDIN

Your worker may need some data to run a job. When queuing a job, send data to the worker using the standard input stream.

If you're not sure how to read from the standard input, check our [examples](examples/). Drop us an [email](mailto:admin@dolater.io) if you're having trouble and we'll help you out.

## Build a docker container with your worker

You'll need to wrap your worker in a docker image. The easiest way to get up to speed on creating a _Dockerfile_ and building a docker image is by reading the [Dockerfile reference](https://docs.docker.com/reference/builder/). There are plenty of Dockerfiles you can use as a reference, you'll just have to search a bit. If you need help, drop us an [email](mailto:admin@dolater.io).

dolater.io runs the image as it is, so keep in `CMD` the exact command to execute your worker.

## Monitoring STDOUT & STDERR when a job runs

To test is your image is working, run it in docker with `echo YOUR_STDIN | docker run -i -e ENV_1=a -e ENV_2=b your/image` replacing `YOUR_STDIN` with the standard input you want to send to the process and replacing the environment variables with whatever your image needs.

When a job runs on dolater.io, we capture the standard output and standard error, so whatever you see when you run the process will be available.

## Publish your image

Right now dolater.io only supports public images stored at [the public docker hub](https://hub.docker.com/). See [How to work with Docker Hub](http://docs.docker.com/userguide/dockerrepos/) for a guide on publishing your images.

We will be able to support private images when external read-only permissions are introduced.
