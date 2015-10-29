# SOS Jobscheduler

Dockerfile for Jobschedulerserver www.sos-berlin.com

Based on ubuntu:latest Image


# General

* Ports: 4444 (webinterface), 40444 (agents)
* you can either use mysql or mariadb
* mysql environment will be used in startup script

# Example

docker-compose.yml

```
jobscheduler:
  image: floedermann/jobscheduler
  links:
    - db:mysql
  ports:
    - "4444:4444"
    - "40444:40444"
db:
  image: mysql
  environment:
    MYSQL_USER: jobscheduler
    MYSQL_PASSWORD: jobscheduler
    MYSQL_ROOT_PASSWORD: scheduler
    MYSQL_DATABASE: jobscheduler

```
