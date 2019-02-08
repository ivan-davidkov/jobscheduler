# Forked -> SOS Jobscheduler
This is my forked version of Jobschedulerserver www.sos-berlin.com

# Why fork it?
Main reason, was I am working on a PoC and CentOS is the target OS

# Update details
* OS => CentOS [FROM centos:latest]
* Java => OpenJDK [RUN yum install -y java-1.8.0-openjdk-src.x86_64 which]
* also added `which` [as used by the original script]
* removed 3th container use local folder as volumes
  * volumes_from anyways was remove from docker-compose while ago
* replaced curl test db part with simple 15sec sleep
* removed alpine sleep infinity hack :)

# General
* Ports:
  * 4446 (Webinterface, username/password: root/root)
  * 40444 (Agents)
* you can either use mysql or mariadb
* mysql environment will be used in startup script

# Usage
```bash
git clone https://github.com/ivan-davidkov/jobscheduler.git
docker-compose -f jobscheduler/docker-compose.yml up -d
google-chrome http://localhost:4446 #[or firefox http://localhost:4446 ]
```
login/password => root/root

# Example
docker-compose.yml

```
version: "3.3"
services:

  jobscheduler:
    build: app
    container_name: app
    links:
      - db:mariadb
    volumes:
      - $PWD/datastore:/opt/jobscheduler/data/scheduler/config/live
    ports:
      - "4446:4446"
      - "40444:40444"
    environment:
    DB_SERVER_DBMS: mariadb
    DB_SERVER_HOST: mariadb
    DB_SERVER_PORT: 3306
    DB_SERVER_USER: jobscheduler
    DB_SERVER_PASSWORD: jobscheduler
    DB_SERVER_DATABASE: jobscheduler

  db:
    image: mariadb:latest
    container_name: db
    environment:
      MYSQL_USER: jobscheduler
      MYSQL_USER: jobscheduler
      MYSQL_PASSWORD: jobscheduler
      MYSQL_ROOT_PASSWORD: scheduler
      MYSQL_DATABASE: jobscheduler
```
