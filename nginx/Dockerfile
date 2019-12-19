FROM docker.pkg.github.com/spielhoelle/zelos_react/zelos_react_zelos_react_frontend:latest as pwa.tmy.io
FROM docker.pkg.github.com/spielhoelle/extsnd/extsnd-gatsby-static-frontend:latest as extsnd.com
MAINTAINER "Thomas Kuhnert"

#FROM debian:jessie as certbot
### Inspiration:
### https://hub.docker.com/r/gaafar/cron/
#RUN mkdir -p /etc/letsencrypt/live/extsnd.com
### Install cron, certbot, bash, plus any other dependencies
#RUN apt-get update \
#   && apt-get install -y cron bash wget \
#   && openssl req -x509 -nodes -days 365 -newkey rsa:2048 \
#    -keyout /etc/letsencrypt/live/extsnd.com/privkey.pem \
#    -out /etc/letsencrypt/live/extsnd.com/fullchain.pem \
#    -subj /CN=extsnd.com
##
#RUN mkdir -p /webroots/extsnd.com/.well-known /scripts
#
#WORKDIR /scripts
#RUN wget https://dl.eff.org/certbot-auto
#RUN chmod a+x ./certbot-auto
### Run certbot-auto so that it installs itself
#RUN /scripts/certbot-auto -n certificates

FROM nginx:1.12-alpine
#ARG CACHEBUST=1
RUN mkdir -p /var/www/certbot
COPY nginx.conf /etc/nginx/nginx.conf

#COPY ./certs/tmy.io.crt /etc/nginx/certs/tmy.io.crt
#COPY ./certs/tmy.io.key /etc/nginx/certs/tmy.io.key

#COPY --from=certbot /scripts /scripts
#COPY --from=certbot /etc/letsencrypt/live/extsnd.com /etc/nginx/certs/extsnd.com
COPY --from=pwa.tmy.io /home/node/build /var/www/pwa.tmy.io
COPY --from=extsnd.com /home/node/build /var/www/extsnd.com

EXPOSE 80 443
CMD ["nginx", "-g", "daemon off;"]
