FROM nginx:stable-alpine-slim

COPY ./infrastructure/config/nginx.conf /etc/nginx/conf.d/default.conf

COPY ./public /var/www/html/public
