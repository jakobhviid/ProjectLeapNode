## Single Server Guide

For this setup you run the whole stack on a single server. It is not recommended, but can be useful in some cases.
This server is refered to as 'SingleServer'. Make sure this server passes the requirements described in [server setup](../SERVERSETUP.md).

In order to make this viable in a production setup you need to seperate services onto other hosts. Each host should then have Dashboard-Server installed alongside the service.
E.g. Create a Kerberos server which installs Dashboard-Server, Kerberos, then onto another host install a Postgres Database for Kerberos.

### Step by step guide
1. Download the folder 'SingleServerGuide' from this repository
2. Change values inside .env to fit your setup
3. Run the following command in your terminal (bash) `docker-compose up`
4. Control output in the console


