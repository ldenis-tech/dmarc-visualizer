FROM python:3.11-alpine

RUN apk add --update --no-cache libxml2-dev libxslt-dev
RUN apk add --update --no-cache --virtual .build_deps build-base libffi-dev \
    && pip install parsedmarc \
    && apk del .build_deps

COPY sample_reports/ /input/
COPY parsedmarc.ini /

## Set up geoipudate for automatic updates
COPY geoip-update-dbs /usr/local/bin/
RUN chmod 755 /usr/local/bin/geoip-update-dbs
RUN geoip-update-dbs
COPY geoip_update_cron /etc/cron.d/
RUN chmod 644 /etc/cron.d/geoip_update_cron