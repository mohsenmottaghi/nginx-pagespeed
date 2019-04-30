# Nginx-Pagespeed

This Docker image include Nginx , Pagespeed module and ...

---  
**Note**: Dockerfile Forked by me from `elct9620`.

**Version:**
NGINX_VERSION 1.14.0
NPS_VERSION 1.13.35.2
OPENSSL_VERSION 1.0.2h

Roadmap
---

- [ ] Add SSL support
- [ ] Add Proxy Mode support
- [ ] Improve template to support more complex config file struct
- [ ] Add Laravel support
- [ ] Add Let's Encrypt support with auto renew

Compiled Modules
---
- http_ssl_module
- http_realip_module
- http_gunzip_module
- http_gzip_static_module
- http_secure_link_module
- http_v2_module
- threads
- file-aio
- ipv6
- http-client-body-temp-path=/var/cache/nginx/client_temp
- http-proxy-temp-path=/var/cache/nginx/proxy_temp
- http-fastcgi-temp-path=/var/cache/nginx/fastcgi_temp
- http-uwsgi-temp-path=/var/cache/nginx/uwsgi_temp
- http-scgi-temp-path=/var/cache/nginx/scgi_temp
- http_addition_module
- http_sub_module
- http_dav_module
- http_flv_module
- http_mp4_module
- http_random_index_module
- http_secure_link_module
- http_stub_status_module
- http_auth_request_module
- http_xslt_module=dynamic
- http_image_filter_module=dynamic
- http_geoip_module=dynamic
- stream
- stream_ssl_module
- stream_ssl_preread_module
- stream_realip_module
- stream_geoip_module=dynamic
- http_slice_module
- mail
- mail_ssl_module
- compat 

Usage
---

The new version provide options to customize Nginx config.

### Host static files

```
docker run -v $(pwd)/www:/var/www/html elct9620/nginx-pagespeed
```

### Run with customize config

```
docker run --env='SERVER_NAME=example.com' elct9620/nginx-pagespeed
```

Options
---

To generate customize config file, just add environment variable when run.
Below is current supported options.

### Default

- `SERVER_NAME` The server name,  default is `localhost`
- `DOCUMENT_ROOT` The root path, default is `/var/www/html`. You can change it point to other path.
- `INDEX_FILES` The nginx default has `index.html index.htm` as index file, you can add other setting like `index.php`
- `ALLOW_ORIGIN` CROS setting, default is limited to same as server name.

### FastCGI

- `FASTCGI_HOST` When this variable is not empty, will enable FastCGI mode for PHP.
- `FASTCGI_PORT` The port for FastCGI server, default is `9000`
- `FASTCGI_INDEX` The default index file for FastCGI, default is `index.php`
- `FASTCGI_ROOT` Due to the FastCGI server is not run with Nginx, you can change the path for it. Default same as document root.

### PageSpeed

- `PAGESPEED_ENABLE` You can disable pagespeed by change this variable, default is `on`
- `PAGESPEED_REWRITE_LEVEL` The default pagespeed optimize options group, default is `PassThrough`
- `PAGESPEED_HEADER` The response header, default is `Powered by ngx_pagespeed`

### Cache

- `CACHE_LEVEL` The cache level for FastCGI (proxy will support soon), default is `1:2`
- `CACHE_ZONE_SIZE` The in memory cache size, default is `100m`
- `Cache_INACTIVE_TIME` The cache inactive time, default is `60m`

### Extension

This image also provide some extra config to fast setup some popular Framework/CMS.

- `WORDPRESS_ADDON` When set to `yes` will change config to add extra config to let `WordPress` work correctly.


