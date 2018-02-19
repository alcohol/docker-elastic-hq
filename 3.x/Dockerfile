FROM scratch

COPY --from=python:3.6-alpine / /

WORKDIR /srv

ARG archive=https://github.com/ElasticHQ/elasticsearch-HQ/archive/v3.0.0.tar.gz

# I strip the top level directory from the archive because
# Github tarballs wrap the entire repo in a top level directory
RUN apk add --update --no-cache curl tar \
 && curl -sLfo /tmp/elastic-hq.tgz $archive \
 && tar -xzf /tmp/elastic-hq.tgz -C /srv --strip 1 \
 && rm /tmp/elastic-hq.tgz \
 && cd /srv \
 && pip install -r requirements.txt \
 && find /srv -type d -exec chmod 700 {} \+ \
 && find /srv -type f -exec chmod 600 {} \+

STOPSIGNAL SIGTERM
EXPOSE 5000

CMD ["python3", "manage.py", "runserver", "-h", "0.0.0.0", "-p", "5000", "-R", "-D"]
