FROM debian:stable-slim

RUN apt-get update && apt-get install -y apache2 git

RUN mkdir -p /var/www/html

RUN mkdir -p /tmp

RUN cd /tmp && git clone https://github.com/ErickStelo/exemplo-php-site.git

RUN mv /tmp/exemplo-php-site/* /var/www/html

RUN rm -rf /tmp/exemplo-php-site

WORKDIR /var/www/html

EXPOSE 80

# Inicia o Apache
CMD ["apachectl", "-D", "FOREGROUND"]
