# Docker Image : python-nginx

[![Build Status](https://travis-ci.org/sanjibm/docker-nginx-server.svg?branch=master)](https://https://travis-ci.com/sanjibm/docker-nginx-server)
[![license](https://img.shields.io/github/license/sanjibm/docker-nginx-server/blob/master/LICENSE)


This image contains Nginx with Gunicorn on top of Python3 docker image.
These two software are managed with Supervisor.

## Usage

The entry point of your application must be named as **run.py**. Moreover, the instance in that file must be called **api**.
Also, by default the worker class used is Gevent.

You can include a custom Gunicorn configuration file into your application. By default the configuration file must be name as **gunicorn.config.py**

## Dockerfile example

Here is an example of a Dockerfile using that image :

```
FROM sanjibm/python-nginx:latest
LABEL maintainer="sanjibm2006@gmail.com"

# Copy the application
COPY . /api

# Install application requirements
RUN pip install -U pip
RUN pip install -r /api/requirements.txt
```

There is also a Flask demo application in the *api* folder of this repository.

## Build and run

First, build your image based on your Dockerfile.

```
docker build -t pyapi .
```

Then, you can run a container like this :

```
docker run -p 127.0.0.1:8000:80 pyapi
```

And finally access it with curl for instance :

```
curl localhost:8000
```
