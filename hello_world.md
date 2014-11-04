# Build your own Hello World worker!

This article will guide you through the creation of a worker that will return "Hello world". The worker will be written in ruby.

## Prerequisites

You will need an account in the [public docker registry](https://hub.docker.com/). Just signup and you'll be ready to go.

In the documentation I use `yourhandler` to represent your docker hub username. Replace it with the right value.

You will also need an account on [dolater.io](http://dolater.io).

## Write your worker

Create a folder for your worker and a file within the folder called `worker.rb` with the following code:

```ruby
puts "Hello world"
```

To make sure it works, run it:

```
$ ruby worker.rb
Hello world
```

## Wrap it into a docker image

Create another file called `Dockerfile` with the following content:

```
FROM ubuntu:14.04

RUN locale-gen en_US.UTF-8 && \
    apt-get update && \
    apt-get upgrade -y && \
    apt-get install -y --no-install-recommends software-properties-common && \
    apt-add-repository ppa:brightbox/ruby-ng && \
    apt-get update && \
    apt-get install -y --no-install-recommends ruby2.1 ruby2.1.dev zlib1g-dev build-essential libssl-dev libreadline-dev libyaml-dev libxml2-dev libxslt1-dev libcurl4-openssl-dev

WORKDIR /opt/

ADD worker.rb /opt/worker.rb

ENTRYPOINT ["ruby", "worker.rb"]
```

This file is used to create the docker image. Visit the [Dockerfile documentation](http://docs.docker.com/reference/builder/) to understand all lines of that file.

Once you have both files in the worker directory you have to build the docker image.

```
docker build -t yourhandler/hello_world .
```

This will load the `Dockerfile` in the current directory and will use it to build a docker image tagged as `yourhandler/hello_world`.

It will take a while to build. Once it's finished, test it running:

```
$ docker run --rm yourhandler/hello_world
Hello world
```

## Upload your docker image to the public registry

Just push the image:

```
docker push yourhandler/hello_world
```

## Submit your image to dolater.io

Access [your images on dolater.io](http://dolater.io/admin/images) and click on _New image_.

Type `Hello world` as _Name_ and `yourhandler/hello_world` as _Docker image_ and click on _Create image_.

Once the image is created, click on _View Jobs_ to access the jobs of the image and click on _New job_ and _Create Job_. Since the worker doesn't need any input we don't need any other information for it.

As soon as you click on _Create Job_, we will run the job on a free slot in our servers. The first time you run it might take a while because we have to pull the image from the docker hub.

Keep refreshing the job page until the state of the job is `completed`. You'll see "Hello world" in the _STDOUT_
