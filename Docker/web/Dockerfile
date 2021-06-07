FROM ubuntu:16.04
MAINTAINER anhdtm

USER root
# Install required system packages
RUN apt-get -q -y update \
    && DEBIAN_FRONTEND=noninteractive apt-get -q -y upgrade \
    && apt-get -q -y install \
        sudo\
        python-minimal \
        python-dev \
        python-pip \
        python-virtualenv \
        python-wheel \
        libpq-dev \
        libxml2-dev \
        libxslt-dev \
        libgeos-dev \
        libssl-dev \
        libffi-dev \
        postgresql-client \
        build-essential \
        git-core \
        vim \
        wget \
        apache2 \
        libapache2-mod-wsgi \
        libmysqlclient-dev \
        libcurl4-openssl-dev \
        libldap2-dev \
        libsasl2-dev \
        gdal-bin \
    && apt-get -q clean \
    && rm -rf /var/lib/apt/lists/*


#Configure webserver
ADD Docker/web/apache.wsgi /etc/ckan/apache.wsgi
ADD Docker/web/ckan_default.conf /etc/apache2/sites-available/ckan_default.conf
ADD Docker/web/ports.conf /etc/apache2/ports.conf
RUN a2ensite ckan_default
RUN a2dissite 000-default

RUN mkdir -p /var/www/storage
RUN chown -R www-data:www-data /var/www/
RUN usermod -u 1000 -d /var/www/storage www-data

CMD ["/usr/sbin/apachectl", "-DFOREGROUND"]
EXPOSE 5000