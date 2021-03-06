# Dockerfiles for Lucee application servers

Dockerfiles to build Lucee application servers.; used for the official LAS Lucee Docker images.

Lucee Docker images are available on Docker Hub: https://hub.docker.com/u/lucee/

## Lucee Base Images

Lucee provides a number of different base images for your Lucee project.  

### Lucee 5.1

- [NGINX / Tomcat 8.0-JRE8 Dockerfile](./lucee-nginx/5.1/) 
  &nbsp; &nbsp; [![Docker Pulls](https://img.shields.io/docker/pulls/lucee/lucee5-nginx.svg?label=DockerHub+Images)](https://hub.docker.com/r/lucee/lucee5-nginx/) [![](https://badge.imagelayers.io/lucee/lucee5-nginx:latest.svg)](https://imagelayers.io/?images=lucee/lucee5-nginx:latest)
- [Tomcat 8.0-JRE8](./5.1/)
  &nbsp; &nbsp; [![Docker Pulls](https://img.shields.io/docker/pulls/lucee/lucee5.svg?label=DockerHub+Images)](https://hub.docker.com/r/lucee/lucee5/) [![](https://badge.imagelayers.io/lucee/lucee5:latest.svg)](https://imagelayers.io/?images=lucee/lucee5:latest)

### Lucee 5.0

- [NGINX / Tomcat 8.0-JRE8 Dockerfile](./lucee-nginx/5.0/) 
  &nbsp; &nbsp; [![Docker Pulls](https://img.shields.io/docker/pulls/lucee/lucee5-nginx.svg?label=DockerHub+Images)](https://hub.docker.com/r/lucee/lucee5-nginx/) [![](https://badge.imagelayers.io/lucee/lucee5-nginx:5.0.0-t8.0.36.svg)](https://imagelayers.io/?images=lucee/lucee5-nginx:5.0.0-t8.0.36)
- [Tomcat 8.0-JRE8](./5.0/)
  &nbsp; &nbsp; [![Docker Pulls](https://img.shields.io/docker/pulls/lucee/lucee5.svg?label=DockerHub+Images)](https://hub.docker.com/r/lucee/lucee5/) [![](https://badge.imagelayers.io/lucee/lucee5:5.0.0-t8.0.36.svg)](https://imagelayers.io/?images=lucee/lucee5:5.0.0-t8.0.36) 

### Lucee 4.5

- [NGINX / Tomcat 8.0-JRE8 Dockerfile](./lucee-nginx/4.5/) 
  &nbsp; &nbsp; [![Docker Pulls](https://img.shields.io/docker/pulls/lucee/lucee4-nginx.svg?label=DockerHub+Images)](https://hub.docker.com/r/lucee/lucee4-nginx/) [![](https://badge.imagelayers.io/lucee/lucee4-nginx:latest.svg)](https://imagelayers.io/?images=lucee/lucee4-nginx:latest)
- [Tomcat 8.0-JRE8](./4.5/)
  &nbsp; &nbsp; [![Docker Pulls](https://img.shields.io/docker/pulls/lucee/lucee4.svg?label=DockerHub+Images)](https://hub.docker.com/r/lucee/lucee4/) [![](https://badge.imagelayers.io/lucee/lucee4:latest.svg)](https://imagelayers.io/?images=lucee/lucee4:latest) 


For an example of setting up a Lucee Docker project see [Lucee Docker Workbench](https://github.com/modius/lucee-docker-workbench).

## Example Project Dockerfile

**Example FarCry application from [Chelsea Docker](https://github.com/modius/chelsea-docker)**
```
FROM lucee/lucee4-nginx:latest

MAINTAINER Geoff Bowers <modius@daemon.com.au>

# TOMCAT CONFIGS
# COPY catalina.properties server.xml web.xml /usr/local/tomcat/conf/
# Custom setenv.sh to load Lucee
# COPY setenv.sh /usr/local/tomcat/bin/

# NGINX configs
COPY config/nginx/ /etc/nginx/
# Lucee server configs
COPY config/lucee/ /opt/lucee/web/
# Deploy codebase to container
COPY code /var/www/farcry
```

## Features

### Java optimisation tweaks

- Lucee 4's [Java Agent](http://blog.getrailo.com/post.cfm/railo-4-1-smarter-template-compilation) is enabled for better memory management of compiled CFML code.

- JVM is set to [use /dev/urandom as an entropy source for secure random numbers](http://support.run.pivotal.io/entries/59869725-Java-Web-Applications-Slow-Startup-or-Failing) to avoid blocking Tomcat on startup.

- Tomcat is configured to [skip the default scanning of Jar files on startup](http://www.gpickin.com/index.cfm/blog/how-to-get-your-tomcat-to-pounce-on-startup-not-crawl), significantly improving startup time.

### Optimised for single-site application

The default configuration serves a single application for any hostname on the listening port. Multiple applications can be supported by editing the `server.xml` in the Tomcat config.


## Contributing to this Project

The Lucee Dockerfiles project is maintained by the community. Chief protagonist is @modius ([Geoff Bowers](https://github.com/modius) of [Daemon](http://www.daemon.com.au)). Bug reports and pull requests are most welcome.

### Spinning things up locally

Using the [Daemon Docker Workbench](https://github.com/justincarter/docker-workbench) provided, or using your own Docker tooling.

These instructions assume you have the parent Workbench up and running:
```
git clone git@github.com:lucee/lucee-dockerfiles.git
cd lucee-dockerfiles
docker-compose up
```

Containers are forwarded onto the following addresses:
```
lucee45 -> $ open http://workbench.192.168.99.100.nip.io:8045/
lucee50 -> $ open http://workbench.192.168.99.100.nip.io:8050/
lucee51 -> $ open http://workbench.192.168.99.100.nip.io:8051/
nginx45 -> $ open http://nginx45.192.168.99.100.nip.io
nginx50 -> $ open http://nginx50.192.168.99.100.nip.io
nginx51 -> $ open http://nginx51.192.168.99.100.nip.io
```


## License

The Docker files and config files are available under the [MIT License](LICENSE). The Lucee engine, Tomcat, NGINX and any other softwares are available under their respective licenses.
