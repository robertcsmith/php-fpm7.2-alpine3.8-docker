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
    - named volume:  unix-sockets-wufgear-nginx:/var/run/php/wufgear \
    - bind-mount:    /app/src/wufgear:/var/www/wufgear \
    - bind-mount:    /app/binds/wufgear/usr-local-etc-php-fpm.d:/usr/local/etc/php-fpm.d \
\
This image is not meant to be extended nor is it generic. It is meant for this project ONLY."

