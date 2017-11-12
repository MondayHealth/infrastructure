# Infrastructure Documentation

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