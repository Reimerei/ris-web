FROM ubuntu:12.04

RUN echo "deb http://archive.ubuntu.com/ubuntu precise main universe" > /etc/apt/sources.list

RUN apt-get update
RUN apt-get upgrade -y
RUN apt-get install -y git apache2 libapache2-mod-wsgi python-virtualenv

# change this to a repo/branch with the right configs
RUN git clone https://github.com/OpenRuhr/ris-web /opt/ris-web 

# apache2 config
RUN cp /opt/ris-web/apache-vhost-template /etc/apache2/sites-available/ris-web
RUN cp /opt/ris-web/template.wsgi /opt/ris-web/ris-web.wsgi
RUN a2enmod wsgi
RUN a2ensite ris-web

ENV APACHE_RUN_USER ris-web
ENV APACHE_RUN_GROUP ris-web

EXPOSE 80

ENTRYPOINT ["/usr/sbin/apache2"]
CMD ["-D", "FOREGROUND"]
