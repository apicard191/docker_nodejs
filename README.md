# Docker Node Environment
This repository allows the creation of a Docker environment to work locally.

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT)

## Architecture
* `web`: ![node: 12](https://img.shields.io/badge/node-12-blue.svg)
* `mysql`: [percona:5.6](https://hub.docker.com/_/percona/) image.
* `redis`: [redis:latest](https://hub.docker.com/_/redis/) image.
* `maildev`: [djfarrelly/maildev:latest](https://hub.docker.com/r/djfarrelly/maildev/) image.

## Additional Features
* **HTTPS** : assumes the support of https locally. Please check the [tips section](#tips) to know how to use it

### Percona
The `./mysql/custom.cnf` file is used to customize the MySQL configuration during the image build process.

## Installation
This process assumes that [Docker Engine](https://www.docker.com/docker-engine) and [Docker Compose](https://docs.docker.com/compose/) are installed.
Otherwise, you should have a look to [Install Docker Engine](https://docs.docker.com/engine/installation/) before proceeding further.

:bangbang: You also need the `make` linux package.

### Set up the environment
```bash
$ make setup
```
#### OR
```bash
$ make env
$ make aliases
$ make cron
$ make vhost
```
> Let's see in the [tips section](#tips) all what you can do

### Build the environment
```bash
$ make install
```

### Check the containers
```bash
$ docker-compose ps
        Name                      Command               State                      Ports
------------------------------------------------------------------------------------------------------------
environment_maildev_1     bin/maildev --web 80 --smtp 25   Up      25/tcp, 0.0.0.0:1080->80/tcp
environment_mysql_1       docker-entrypoint.sh mysqld      Up      0.0.0.0:3306->3306/tcp
environment_redis_1       docker-entrypoint.sh redis ...   Up      0.0.0.0:6379->6379/tcp
environment_web_1         docker-custom-entrypoint         Up      0.0.0.0:443->443/tcp, 0.0.0.0:80->80/tcp
```
Note: You will see something slightly different if you do not clone the repository in a `environment` directory.
The container prefix depends on your directory name.

## Tips
1. **Getting started** :
Launch the command below and see all what you can do :
```bash
$ make help
```

2. **General informations** :
    - To plug your database to your application (if you didn't change the information in `.env` file) :
        - host : `'mysql'`
        - database : `yourdatabasename`
        - user : `'root'`
        - pass : `null`

3. You can add custom virtual hosts: all `./web/vhosts/*.conf` files are copied in the Apache directory during the image build process.

4. The HTTPS can be used easily. Check `./web/vhosts/environment.conf` as a model to get it on all your websites. You don't need to change the cert and key files.
