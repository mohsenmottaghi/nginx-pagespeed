# Nginx-Pagespeed
![Generic badge](https://img.shields.io/badge/Dockerfile-Pass-<COLOR>.svg) ![Generic badge](https://img.shields.io/badge/Build-Pass-<COLOR>.svg) ![Generic badge](https://img.shields.io/badge/Dockerfile_Layer-21-blue.svg) ![Generic badge](https://img.shields.io/badge/Dockerfile_Image_Size-about_450_MB-blue.svg) ![Generic badge](https://img.shields.io/badge/Dockerfile_Auto_Build-Yes-<COLOR>.svg) ![Generic badge](https://img.shields.io/badge/Maintainer-Mohsen_Mottaghi-yellow.svg)

This Docker image include Nginx , Pagespeed module and ...

---  
**Note**: Dockerfile Cloned by me from `elct9620`.

**Docker Image Tags:**
- latest
- ubuntu-16-04
- ubuntu-18-04
- ubuntu-18-10
- ubuntu-19-04
- debian-latest
- debian-stretch
- debian-jessie

**Version:**

* NGINX_VERSION 1.20.0 ( stable version )
* NPS_VERSION 1.13.35.2-stable
* OPENSSL_VERSION 1.1.0g

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

## GitHub Action Status
![ubuntu-1904 Docker Image CI](https://github.com/mohsenmottaghi/nginx-pagespeed/workflows/ubuntu-1904%20Docker%20Image%20CI/badge.svg)
![debian-buster Docker Image CI](https://github.com/mohsenmottaghi/nginx-pagespeed/workflows/debian-buster%20Docker%20Image%20CI/badge.svg)
![debian-jessie Docker Image CI](https://github.com/mohsenmottaghi/nginx-pagespeed/workflows/debian-jessie%20Docker%20Image%20CI/badge.svg)
![debian-latest Docker Image CI](https://github.com/mohsenmottaghi/nginx-pagespeed/workflows/debian-latest%20Docker%20Image%20CI/badge.svg)
![debian-stretch Docker Image CI](https://github.com/mohsenmottaghi/nginx-pagespeed/workflows/debian-stretch%20Docker%20Image%20CI/badge.svg)
![ubuntu-1604 Docker Image CI](https://github.com/mohsenmottaghi/nginx-pagespeed/workflows/ubuntu-1604%20Docker%20Image%20CI/badge.svg)
![ubuntu-1804 Docker Image CI](https://github.com/mohsenmottaghi/nginx-pagespeed/workflows/ubuntu-1804%20Docker%20Image%20CI/badge.svg)
![ubuntu-1904-mainline Docker Image CI](https://github.com/mohsenmottaghi/nginx-pagespeed/workflows/ubuntu-1904-mainline%20Docker%20Image%20CI/badge.svg)
![debian-jessie-mainline Docker Image CI](https://github.com/mohsenmottaghi/nginx-pagespeed/workflows/debian-jessie-mainline%20Docker%20Image%20CI/badge.svg)
![debian-buster-mainline Docker Image CI](https://github.com/mohsenmottaghi/nginx-pagespeed/workflows/debian-buster-mainline%20Docker%20Image%20CI/badge.svg)
![ubuntu-1604-mainline Docker Image CI](https://github.com/mohsenmottaghi/nginx-pagespeed/workflows/ubuntu-1604-mainline%20Docker%20Image%20CI/badge.svg)
![ubuntu-1804-mainline Docker Image CI](https://github.com/mohsenmottaghi/nginx-pagespeed/workflows/ubuntu-1804-mainline%20Docker%20Image%20CI/badge.svg)
![debian-stretch-mainline Docker Image CI](https://github.com/mohsenmottaghi/nginx-pagespeed/workflows/debian-stretch-mainline%20Docker%20Image%20CI/badge.svg)
![debian-latest-mainline Docker Image CI](https://github.com/mohsenmottaghi/nginx-pagespeed/workflows/debian-latest-mainline%20Docker%20Image%20CI/badge.svg)