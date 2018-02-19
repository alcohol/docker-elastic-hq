# alcohol/elastic-hq

A simplistic Docker image, that serves up [ElasticHQ] using nginx, while requiring no privileges to run.

Docker Hub: https://hub.docker.com/r/alcohol/elastic-hq/

# running

## 1.x / 2.x

```
docker run --rm -d --cap-drop ALL --publish 8000:8000 --name elastic-hq alcohol/elastic-hq
```

## 3.x

Since `3.0.0`, the default port exposed by the container has changed due to upstream changes.

```
docker run --rm -d --cap-drop ALL --publish 8000:5000 --name elastic-hq alcohol/elastic-hq
```

> Note: while previously the connection was established within the browser, since version 3.0.0,
> it is established inside the container. This means that your container will need to be able to
> resolve and connect to your target host.

# building

The image builds straight from Github tarballs of the [ElasticHQ] project. The archive you want
to use can be specified as a `--build-arg` to `docker build`. For further details, please see
the [`Dockerfile`](Dockerfile).

Example for building the v3.0.0 version:

```
docker build \
    --build-arg archive=https://github.com/ElasticHQ/elasticsearch-HQ/archive/v3.0.0.tar.gz \
    --tag <tagname> \
    3.x
```

# contributing

Feel free to leave comments or suggestions through a Github issue.


[ElasticHQ]: http://www.elastichq.org
