<<<<<<< HEAD
# https://github.com/robertcsmith/php-fpm7.2-alpine3.8-docker

## Maintained by: [Robert C Smith](https://github.com/robertcsmith)

This is the Git repo of the PHP-FPM v7.2.1 for [php](https://hub.docker.com/_/php/) (not to be confused with any official php images as this version had been modified greatly to fit our needs). 

This image also serves as an intermediate for a few front ends residing upstream from our virtual host application server (nginx). So this image is never made into a container but does pull the weight from the primary language to execute the code that is responded to from a request.

## So feel free to use this implementation of PHP-FPM

We also have a CLI intermediate which just serves Bash with all code accessible. And finally we have a CLI final image that can be used with all sorts of tools to engineer our derivative PHP-FPM code base.

Here is more info taken from a child Dockerfile: \
\
"This image provides the tools needed to properly install the source code for http://wufgear.com and/or make modifications to it for debugging and/or perform maintenance functions and/or upgrades through an interactive BASH shell. The container this image builds operates on a separate development source code, however, the connection to the database and cache containers are those used in production and the container is meant to be built with, and ran with only the tools needed and ONLY while the production container is stopped (aka down for maints) by the developer and the container instance should disconnect all volumes and binds, commit and push source code changes to git and GitHub (as well as image chaanges to other subtrees (aka other container images) before being destroyed. To make the changes within production, manually perform a git pull on the production source code. Any changes made to other subtrees should also be updated but assuming the changes were to the images The containers will need to be removed and recreated. A better document for this proceedure can be found in the README.md found in the same directory of this image as well as the directory of the Compose file which is responsible for building this app. See below for the needed bind mounts and volumes which must be created and paired with the container this image builds for proper functionality: \
\
    - named volume:  unix-sockets-nginx-wufgear:/var/run/php/wufgear \
    - bind-mount:    /app/src/wufgear:/var/www/wufgear \
    - bind-mount:    /app/binds/wufgear/usr-local-etc-php-fpm.d:/usr/local/etc/php-fpm.d \
\
This image is not meant to be extended nor is it generic. It is meant for this project ONLY."
=======
# php-fpm 7.2 on Alpine 3.8 via Docker


## Supported tags and respective `Dockerfile` links


Table of Contents
=================

* [Description](#description)
* [Usage](#usage)
* [Tips & Pitfalls](#tips--pitfalls)
* [Docker CMD](#docker-entrypoint)
* [Building (from source)](#building-from-source)
* [Changelog & Authors](#changelog--authors)
* [Copyright & License](#copyright--license)


Description
===========



Docker is a container management platform.


(#build-options) :

 * file-aio
 * http_addition_module
 * http_auth_request_module
 * http_dav_module
 * http_flv_module
 * http_geoip_module=dynamic
 * http_gunzip_module
 * http_gzip_static_module
 * http_image_filter_module=dynamic
 * http_mp4_module
 * http_random_index_module
 * http_realip_module
 * http_secure_link_module
 * http_slice_module
 * http_ssl_module
 * http_stub_status_module
 * http_sub_module
 * http_v2_module
 * http_xslt_module=dynamic
 * ipv6
 * mail
 * mail_ssl_module
 * md5-asm
 * pcre-jit
 * sha1-asm
 * stream
 * stream_ssl_module
 * threads


Usage
=====

If you are happy with the build defaults, then you can use the openresty image from the [Docker Hub](https://hub.docker.com/r/openresty/openresty/).  The image tags available there are listed at the top of this README.

```
docker run [options] openresty/openresty:stretch-fat
```

*[options]* would be things like -p to map ports, -v to map volumes, and -d to daemonize.

`docker-openresty` symlinks `/usr/local/openresty/nginx/logs/access.log` and `error.log` to `/dev/stdout` and `/dev/stderr` respectively, so that Docker logging works correctly.  If you change the log paths in your `nginx.conf`, you should symlink those paths as well. This is not possible with the `windows` image.

nginx config files
==================

The Docker tooling installs its own [`nginx.conf` file](https://github.com/openresty/docker-openresty/blob/master/nginx.conf).  If you want to directly override it, you can replace it in your own Dockerfile or via volume bind-mounting.

For the Linux images, that `nginx.conf` has the directive `include /etc/nginx/conf.d/*.conf;` so all nginx configurations in that directory will be included.  The [default virtual host configuration](https://github.com/openresty/docker-openresty/blob/master/nginx.vh.default.conf) has the original OpenResty configuration and is copied to `/etc/nginx/conf.d/default.conf`. 

You can override that `default.conf` directly or volume bind-mount the `/etc/nginx/conf.d` directory to your own set of configurations:

```
docker run -v /my/custom/conf.d:/etc/nginx/conf.d openresty/openresty:alpine
```

When using the `windows` image you can change the main configuration directly:
```
docker run -v C:/my/custom/nginx.conf:C:/openresty/conf/nginx.conf openresty/openresty:windows
```
>>>>>>> 67e059a0208eb4cb5d752550e943b597186adad8

