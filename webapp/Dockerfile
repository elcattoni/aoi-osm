FROM python:3.7-stretch

RUN wget http://download.osgeo.org/libspatialindex/spatialindex-src-1.8.5.tar.gz
RUN tar -xvf spatialindex-src-1.8.5.tar.gz
RUN cd spatialindex-src-1.8.5 && ./configure; make; make install; ldconfig

RUN apt-get update && \
    apt-get install --no-install-recommends --yes osm2pgsql gdal-bin postgresql-client && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

ADD requirements.txt /tmp/requirememts.txt
RUN pip install -r /tmp/requirememts.txt

ADD . /webapp
RUN mkdir -p /webapp/tmp
WORKDIR /webapp

ENV FLASK_APP="webapp.py"
ENV FLASK_DEBUG=False

EXPOSE 5000

CMD ["/bin/sh", "-l", "-c", "flask run --host 0.0.0.0"]
