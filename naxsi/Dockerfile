FROM ubuntu:16.04
RUN apt-get update && \
        apt-get install -y wget tar apt-utils autoconf automake build-essential git libcurl4-openssl-dev libgeoip-dev liblmdb-dev libpcre++-dev libtool libxml2 libxml2-dev libssl-dev libyajl-dev pkgconf zlib1g-dev libpcre3-dev && \
 wget http://nginx.org/download/nginx-1.14.0.tar.gz && \
 wget https://github.com/nbs-system/naxsi/archive/0.56.tar.gz -O naxsi && \
 tar -xvf nginx-1.14.0.tar.gz && \
 tar -xvf naxsi && \
 cd nginx-1.14.0 && \
     ./configure \
    --conf-path=/etc/nginx/nginx.conf \
    --add-module=../naxsi-0.56/naxsi_src/ \
    --error-log-path=/var/log/nginx/error.log \
    --http-client-body-temp-path=/var/lib/nginx/body \
    --http-fastcgi-temp-path=/var/lib/nginx/fastcgi \
    --http-log-path=/var/log/nginx/access.log \
    --http-proxy-temp-path=/var/lib/nginx/proxy \
    --lock-path=/var/lock/nginx.lock \
    --pid-path=/var/run/nginx.pid \
    --user=www-data \
    --group=www-data \
    --with-http_ssl_module \
    --without-mail_pop3_module \
    --without-mail_smtp_module \
    --without-mail_imap_module \
    --without-http_uwsgi_module \
    --without-http_scgi_module \
    --prefix=/usr && \
 make && make install 
COPY naxsi_core.rules /etc/nginx/naxsi_core.rules
COPY naxsi.rules /etc/nginx/naxsi.rules
COPY error.html /usr/html/error.html
COPY error.html /usr/share/nginx/html/error.html
COPY nginx.conf /etc/nginx/nginx.conf
RUN mkdir -p /var/lib/nginx/body
CMD /usr/sbin/nginx -g 'daemon off;'
EXPOSE 80
