# ----------------------------------------------------------- #
#  MOHSEN MOTTAGHI |   nginx with speedpage     |  Feb  2019  #
# ----------------------------------------------------------- #

FROM ubuntu:18.10

LABEL maintainer="co.mohsen.docker.registry"

# Set Version of Tools - Stable Version
ENV NGINX_VERSION 1.16.1
ENV NPS_VERSION 1.13.35.2
ENV OPENSSL_VERSION 1.1.0g

# Setup Environment
ENV MODULE_DIR /usr/src/nginx-modules
ENV NGINX_TEMPLATE_DIR /usr/src/nginx
ENV NGINX_RUNTIME_DIR /usr/src/runtime
ENV SSL_CERTS_DIR /usr/certs

ENV DEBIAN_FRONTEND noninteractive

# Install Build Tools & Dependence
RUN echo "#!/bin/sh\nexit 0" > /usr/sbin/policy-rc.d
RUN sed -i -- "s/# deb-src/deb-src/g" /etc/apt/sources.list && \
    apt-get update && \
    apt-get install wget uuid-dev -y && \
    apt-get build-dep nginx -y && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* && \
#
    # ===========
    # Build Nginx
    # ===========
#
    # Create Module Directory
    mkdir ${MODULE_DIR} && \
#
    # Downloading Source
    cd /usr/src && \
    wget -q http://nginx.org/download/nginx-${NGINX_VERSION}.tar.gz && \
    tar xzf nginx-${NGINX_VERSION}.tar.gz && \
    rm -rf nginx-${NGINX_VERSION}.tar.gz && \
#
     cd /usr/src && \
    wget -q http://www.openssl.org/source/openssl-${OPENSSL_VERSION}.tar.gz && \
    tar xzf openssl-${OPENSSL_VERSION}.tar.gz && \
    rm -rf openssl-${OPENSSL_VERSION}.tar.gz && \
#
    # Install Addational Module
    cd ${MODULE_DIR} && \
    wget -q https://github.com/apache/incubator-pagespeed-ngx/archive/v${NPS_VERSION}-stable.tar.gz && \
    tar zxf v${NPS_VERSION}-stable.tar.gz && \
    rm -rf v${NPS_VERSION}-stable.tar.gz && \
    cd incubator-pagespeed-ngx-${NPS_VERSION}-stable/ && \
    wget -q https://dl.google.com/dl/page-speed/psol/${NPS_VERSION}-x64.tar.gz && \
    tar zxf ${NPS_VERSION}-x64.tar.gz && \
    rm -rf ${NPS_VERSION}-x64.tar.gz 
#
    # Compile Nginx
RUN cd /usr/src/nginx-${NGINX_VERSION} && \
    ./configure \
    --prefix=/etc/nginx \
    --sbin-path=/usr/sbin/nginx \
    --modules-path=/usr/lib/nginx/modules \
    --conf-path=/etc/nginx/nginx.conf \
    --pid-path=/var/run/nginx.pid \
    --lock-path=/var/run/nginx.lock \
    --error-log-path=/var/log/nginx/error.log \
    --http-log-path=/var/log/nginx/access.log \
    --with-http_ssl_module \
    --with-http_realip_module \
    --with-http_gunzip_module \
    --with-http_gzip_static_module \
    --with-http_secure_link_module \
    --with-http_v2_module \
    --with-threads \
    --with-file-aio \
    --with-ipv6 \
    --with-openssl="../openssl-${OPENSSL_VERSION}" \
    --add-module=${MODULE_DIR}/incubator-pagespeed-ngx-${NPS_VERSION}-stable \
    --http-client-body-temp-path=/var/cache/nginx/client_temp \
    --http-proxy-temp-path=/var/cache/nginx/proxy_temp \
    --http-fastcgi-temp-path=/var/cache/nginx/fastcgi_temp \
    --http-uwsgi-temp-path=/var/cache/nginx/uwsgi_temp \
    --http-scgi-temp-path=/var/cache/nginx/scgi_temp \
    --user=nginx \
    --group=nginx \
    --with-http_addition_module \
    --with-http_sub_module \
    --with-http_dav_module \
    --with-http_flv_module \
    --with-http_mp4_module \
    --with-http_random_index_module \
    --with-http_secure_link_module \
    --with-http_stub_status_module \
    --with-http_auth_request_module \
    --with-http_xslt_module=dynamic \
    --with-http_image_filter_module=dynamic \
    --with-http_geoip_module=dynamic \
    --with-stream \
    --with-stream_ssl_module \
    --with-stream_ssl_preread_module \
    --with-stream_realip_module \
    --with-stream_geoip_module=dynamic \
    --with-http_slice_module \
    --with-mail \
    --with-mail_ssl_module \
    --with-compat \
#
    # Install Nginx
    && cd /usr/src/nginx-${NGINX_VERSION} \
    && make && make install  \
    && mkdir -p /var/www/html  \
    && mkdir -p /etc/nginx/conf.d  \
    && mkdir -p /usr/share/nginx/html \
    && mkdir -p /var/cache/nginx \
    && mkdir -p /var/cache/ngx_pagespeed \
    && install -m644 html/index.html /var/www/html  \
    && install -m644 html/50x.html /usr/share/nginx/html \
#
    # Clear source code to reduce container size
    && rm -rf /usr/src/* \
    && mkdir -p ${NGINX_TEMPLATE_DIR} \
    && mkdir -p ${NGINX_RUNTIME_DIR} \
    && mkdir -p ${SSL_CERTS_DIR} \
#
    # clean packages to reduce container size
    && apt purge wget build-essential --auto-remove -y

# Forward requests and errors to docker logs
RUN ln -sf /dev/stdout /var/log/nginx/access.log && \
    ln -sf /dev/stderr /var/log/nginx/error.log

VOLUME ["/var/cache/nginx", "/var/cache/ngx_pagespeed", "/var/www/html", "/usr/certs"]

COPY nginx.conf /etc/nginx/nginx.conf

# Copy config template
COPY template/ ${NGINX_TEMPLATE_DIR}/
COPY runtime/ ${NGINX_RUNTIME_DIR}/
COPY entrypoint.sh /entrypoint.sh

EXPOSE 80 443

ENTRYPOINT ["/entrypoint.sh"]
CMD ["nginx", "-g", "daemon off;"]
