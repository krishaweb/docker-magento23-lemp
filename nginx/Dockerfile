FROM ubuntu:16.04

MAINTAINER Sanket Kulkarni <sanket@krishaweb.com>

RUN apt-get update \
    && apt-get install -y nginx \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* \
    && echo "daemon off;" >> /etc/nginx/nginx.conf

RUN \	
apt-get update && \
apt-get install -y vim nano

COPY ./conf/default /etc/nginx/sites-available/

EXPOSE 80
EXPOSE 443
CMD ["nginx"]