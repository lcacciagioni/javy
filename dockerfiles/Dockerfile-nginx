FROM nginx:stable-alpine

ADD https://s3.amazonaws.com/infra-assessment/static.zip /usr/share/src/static/static.zip

ADD nginx.conf /etc/nginx/nginx.conf

RUN apk add --update unzip && rm -rf /var/cache/apk/* && \
  cd /usr/share/src/static/ && \
  unzip static.zip && rm -rf static.zip && \
  chown -R nginx:nginx /usr/share/src/static
