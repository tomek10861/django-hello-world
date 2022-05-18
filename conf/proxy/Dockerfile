FROM nginx:1.21

ENV CHECK_IP="ifconf.me"

RUN apt-get update && apt-get install curl openssl -y
RUN IP=`curl $CHECK_IP` && openssl req -x509 -nodes -days 365 -subj "/C=PL/L=Lublin/O=BardzoTajnaFirma Sp. z o.o./OU=IT/CN=$IP" -addext "subjectAltName=DNS:$IP" -newkey rsa:2048 -keyout /etc/ssl/private/selfsigned.key -out /etc/ssl/certs/selfsigned.crt;

COPY django-web.conf.template /etc/nginx/templates/
COPY uwsgi_params /etc/nginx/
