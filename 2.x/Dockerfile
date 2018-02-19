FROM scratch

COPY --from=nginx:mainline-alpine / /

WORKDIR /srv

ARG archive=https://github.com/ElasticHQ/elasticsearch-HQ/archive/v2.0.3.tar.gz

COPY ["nginx.conf", "/etc/nginx/"]

# I strip the top level directory from the archive because
# Github tarballs wrap the entire repo in a top level directory
RUN apk add --update --no-cache curl tar \
 && curl -sLfo /tmp/elastic-hq.tgz $archive \
 && tar -xzf /tmp/elastic-hq.tgz -C /srv --strip 1 \
 && rm /tmp/elastic-hq.tgz /etc/nginx/conf.d/* \
 && touch /var/run/nginx.pid \
 && chown -R nginx /srv /var/cache/nginx /var/run/nginx.pid \
 && find /srv -type d -exec chmod 700 {} \+ \
 && find /srv -type f -exec chmod 600 {} \+

STOPSIGNAL SIGTERM
EXPOSE 8000
USER nginx

CMD ["nginx", "-g", "daemon off;"]
