# alcohol/elastic-hq

A simplistic Docker image, that serves up [ElasticHQ] using nginx, while requiring no privileges to run.

Docker Hub: https://hub.docker.com/r/alcohol/elastic-hq/

# running

```
# grab or update to latest version
docker pull alcohol/elastic-hq

# run latest version
docker run --rm -d --cap-drop ALL --publish 8000:8000 --name elastic-hq alcohol/elastic-hq
```

# building

The image builds straight from Github tarballs of the [ElasticHQ] project.
The archive you want to use can be specified as a `--build-arg` to `docker build`. For further details,
please see the [`Dockerfile`](Dockerfile).

```
docker build \
    --build-arg archive=https://github.com/ElasticHQ/elasticsearch-HQ/archive/v2.0.3.tar.gz \
    --tag <tagname> \
    .
```

# contributing

Feel free to leave comments or suggestions through a Github issue.


[ElasticHQ]: http://www.elastichq.org
