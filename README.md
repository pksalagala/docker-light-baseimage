# osixia/light-baseimage

[![](https://badge.imagelayers.io/osixia/light-baseimage:latest.svg)](https://imagelayers.io/?images=osixia/light-baseimage:latest 'Get your own badge on imagelayers.io') | [Docker Hub](https://hub.docker.com/r/osixia/light-baseimage/) 

A Debian based docker image to help you build reliable image quickly. This image provide a simple opinionated solution to build multiple or single process image.

The aims of this image is to be used as a base for your own Docker images. It's base on the awesome work of: [phusion/baseimage-docker](https://github.com/phusion/baseimage-docker)

## Contributing

If you find this image useful here's how you can help:

- Send a pull request with your kickass new features and bug fixes
- Help new users with [issues](https://github.com/osixia/docker-openldap/issues) they may encounter
- Support the development of this image and star this repo ! ;)

## Overview

This image takes all the advantages of [phusion/baseimage-docker](https://github.com/phusion/baseimage-docker) but makes programs optionals to allow more lightweight images and single process images.

So major features are:
 - simple way to install services and multiple process image stacks
 - getting environment variables from **.yaml** and **.json** files
 - special environment files **.yaml.startup** and **.json.startup** deleted after image startup files first execution. To keep the image setup secret.

## Quick Start

### Image directories structure


### Single process image


### Multiple process image


## Advanced User Guide


### Run options

## Image Assets Details

### /container/tool

#### run

The run tool is defined as the image ENTRYPOINT (see [Dockerfile](image/Dockerfile)). It set environment for startup scripts and images process. More information in the Advanced User Guide

#### setuser
A tool for running a command as another user. Easier to use than su, has a smaller attack vector than sudo, and unlike chpst this tool sets $HOME correctly. Available as /sbin/setuser.

#### log-helper
A simple bash tool to print message base on the log level set by the run tool.

#### install-multiple-process-stack
A tool to install the multiple process stack: runit, cron syslog-ng-core and logrotate.

#### install-service
A tool that execute /container/service/install.sh and /container/service/\*/install.sh if file exists.

#### install-service-available
A tool to install services in the service-available directory.

#### complex-bash-env
A tool to iterate trough complex bash environment variables created by the run tool when a table or a list was set in environment files.

### /container/service-available

#### runit
Replaces Debian's Upstart. Used for service supervision and management. Much easier to use than SysV init and supports restarting daemons when they crash. Much easier to use and more lightweight than Upstart.

This service is part of the multiple-process-stack

#### cron
Cron daemon.

This service is part of the multiple-process-stack

#### syslog-ng-core
Syslog daemon so that many services - including the kernel itself - can correctly log to /var/log/syslog. If no syslog daemon is running, a lot of important messages are silently swallowed.

Only listens locally. All syslog messages are forwarded to "docker logs".

This service is part of the multiple-process-stack

#### logrotate
Rotates and compresses logs on a regular basis.

This service is part of the multiple-process-stack

#### cfssl
CFSSL is CloudFlare's PKI/TLS swiss army knife. It is both a command line tool for signing, verifying, and bundling TLS certificates.

Comes with cfssl-helper tool that make it docker friendly by taking command line parameters from environment variables.

### Tests

We use **Bats** (Bash Automated Testing System) to test this image:

> [https://github.com/sstephenson/bats](https://github.com/sstephenson/bats)

Install Bats, and in this project directory run:

	make test

## Changelog

Please refer to: [CHANGELOG.md](CHANGELOG.md)
