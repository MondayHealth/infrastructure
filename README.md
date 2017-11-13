# Infrastructure Documentation

## Before You Start

Before reading the rest of this guide, you'll want to familiarize yourself with the following:

- [Dokku](http://dokku.viewdocs.io/dokku/) (it will also help to know the basics of [Docker](https://www.docker.com/))
- [Foreman](https://github.com/ddollar/foreman)
- [Redis](https://redis.io/)
- [SSDB](http://ssdb.io/)
- [Postgres](https://www.digitalocean.com/community/tutorials/sqlite-vs-mysql-vs-postgresql-a-comparison-of-relational-database-management-systems)
- [ActiveRecord](http://guides.rubyonrails.org/active_record_basics.html)
- [Resque](https://github.com/resque/resque)
- [Selenium](https://github.com/SeleniumHQ/selenium/wiki/Ruby-Bindings)

To access the cloud servers, you'll also need to be added to our account on [DigitalOcean](https://www.digitalocean.com/).

## Hosts

You should probably update your local hosts file to point to our servers' IP addresses until we give them DNS entries:

    # add to /etc/hosts with current values from DigitalOcean
    165.227.99.213  monday-scraper
    104.236.123.116 monday-crawler
    174.138.95.195  monday-postgres
    174.138.65.100  monday-ssdb
    138.197.20.146  monday-redis

## Servers

Monday's server infrastructure is split into small, single-purpose microservices, each hosted on its own DigitalOcean droplet:

### App Servers

- monday-scraper
- monday-crawler

### Database Servers

- monday-postgres
- monday-redis
- monday-ssdb

## Server Setup

### monday-scraper

OS: Ubuntu 16.04
Install: [dokku](http://dokku.viewdocs.io/dokku~v0.10.3/getting-started/installation/)
Customize: 

Create a shared directory for CSV files:

    dokku storage:mount monday-scraper /var/lib/dokku/data/storage:/app/storage

### monday-crawler

OS: Ubuntu 16.04
Install: [dokku](http://dokku.viewdocs.io/dokku~v0.10.3/getting-started/installation/), [polipo](https://www.irif.fr/~jch/software/polipo/)

### monday-postgres

OS: One-click Postgres installation
Install: [dokku](http://dokku.viewdocs.io/dokku~v0.10.3/getting-started/installation/)
Customize: See the [DigitalOcean guide](https://www.digitalocean.com/community/tutorials/how-to-install-and-use-postgresql-on-ubuntu-16-04) for info on how to create databases and users. Need to open up postgres to [outside connections](http://www.thegeekstuff.com/2014/02/enable-remote-postgresql-connection/?utm_source=tuicool, too. Create one database and a user, dokku, with a password that will end up in DATABASE_URL across all environments.

### monday-redis

OS: One-click Redis installation
Customization: See the [DigitalOcean guide](https://www.digitalocean.com/community/tutorials/how-to-use-the-redis-one-click-application) for details. Enable remote access.

### monday-ssdb

OS: Ubuntu 16.04
Install: [ssdb](http://ssdb.io/docs/install.html)