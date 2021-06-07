FROM anhdtmse62452/web:16.04

MAINTAINER anhdtm

ENV CKAN_HOME /usr/lib/ckan
ENV BRANCH ckan-2.8.2

RUN virtualenv $CKAN_HOME && \
    mkdir -p $CKAN_HOME /project /var/www/storage && \
    chown -R www-data:www-data /var/www && \
    git clone --branch $BRANCH https://github.com/ckan/ckan /project/ckan && \
    $CKAN_HOME/bin/pip install setuptools==36.1 && \
    git clone --branch stable --depth 1 https://github.com/ckan/datapusher /project/datapusher && \
    $CKAN_HOME/bin/pip install -e git+https://github.com/ckan/ckan-service-provider#egg=ckanserviceprovider && \
    $CKAN_HOME/bin/pip install -r /project/ckan/requirements.txt && \
    $CKAN_HOME/bin/pip install -e /project/ckan && \
    $CKAN_HOME/bin/pip install ckanapi && \
    $CKAN_HOME/bin/pip install -r /project/datapusher/requirements.txt\
    $CKAN_HOME/bin/pip install Flask==0.12.4