Ticket
========

# Setup Infrastructure

## Requirements

You'll need the following software installed on your machine:

* [Docker](https://docs.docker.com/install/)
* [Docker Compose](https://docs.docker.com/compose/install/)
* [PHP Coding Standards Fixer](http://cs.sensiolabs.org/)

## Docker

Create docker-compose environment file based on `dist.env`

```bash
cp infra/docker/local/dist.env infra/docker/local/.env
```

Build the containers, if you see any problem you can provide the `no-cache` argument  (this action may take several minutes)

```bash
bin/docker build
```

Start up the containers

```bash
bin/docker up
```

Add entries to your `/etc/hosts` file:

```bash
127.0.0.1 ticket-api.loc
```

## Database

```bash
echo "CREATE DATABASE IF NOT EXISTS ticket" | bin/docker db-load
echo "GRANT ALL ON ticket.* TO 'ticket'@'%' IDENTIFIED BY 'ticket'" | bin/docker db-load
```

## Mailcatcher

```bash
http://ticket-api.loc:8083/mailcatcher
```

## App vendors

```bash
cp dist.env .env
```


Install PHP vendors via composer, warmup cache, check security vendors and generate DB schema.

```bash
bin/docker php composer install
```
