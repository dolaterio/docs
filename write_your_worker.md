# How to write a worker

This document will guide you through the creation of a worker to be executed in dolater.io.

While you code your worker keep in mind that dolater.io executes it for each job.

# Configuration variables

Any configuration should be passed to your worker using environment variables.

There are two ways you can send environment variables to your job, from the image or from the job itself.

# Standard Input

When you queue a job you might need to send some data to it. This data is specific to the job and is sent to the process through the standard input stream.

If you are not sure how to read from the standard input, check our examples. If you still can't make it work, please let us know and we'll assist you.

There's no length limit for the standard input, but if it becomes an issue some day we might limit it, so please try to send __just__ the data you need to avoid future problems.

# Build a docker container with your worker

You'll need to wrap your worker in a docker imager. If you don't know how to do it, start reading the [Dockerfile reference](https://docs.docker.com/reference/builder/). You'll learn how to create a _Dockerfile_ and build an image. There're plenty of Dockerfiles you can use as a reference, you'll just have to search a bit. Again, if you're not sure how to make this work, don't hesitate to contact us.

dolater runs the image as it is, so keep in `CMD` the exact command to execute your worker.

To test is your image is working, run it in docker with `echo YOUR_STDIN | docker run -i -e ENV_1=a -e ENV_2=b your/image` replacing `YOUR_STDIN` with the standard input you want to send to the process and replacing the environment variables with whatever your image needs.

dolater will capture the standard output and stardard error, so whatever you see when you run the process will be available too in dolater.

# Publish your image

Right now dolater.io only supports public images stored at [the public docker hub](https://hub.docker.com/). Chec this guide on [How to work with Docker Hub](http://docs.docker.com/userguide/dockerrepos/) to learn how to publish your images.

We will add support to private images as soon as the docker hub has a good support for external read-only permissions.
