FROM ubuntu
MAINTAINER Marc Despland <marc.despland@art122-5.net>
RUN mkdir -p /project
ADD httpd-2.4.23.tar.gz /project/
ENV http_proxy http://proxy.rd.francetelecom.fr:8080
ENV https_proxy http://proxy.rd.francetelecom.fr:8080
RUN apt-get update && apt-get install -y g++ build-essential libapr1-dev libaprutil1-dev libpcre3-dev
WORKDIR /project/httpd-2.4.23/
COPY event.c /project/httpd-2.4.23/server/mpm/event/
RUN ./configure
RUN make
RUN make install
RUN sed -i 's/#Include conf\/extra\/httpd-mpm.conf/Include conf\/extra\/httpd-mpm.conf/' /usr/local/apache2/conf/httpd.conf
COPY httpd-mpm.conf /usr/local/apache2/conf/extra/
CMD /usr/local/apache2/bin/httpd -D FOREGROUND