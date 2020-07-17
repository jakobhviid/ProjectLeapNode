## Single Server Guide

For this setup you run the whole stack on a single linux server. It is not recommended, but can be useful in some cases.

This server is refered to as 'SingleServer'. Make sure this server passes the requirements described in [server setup](../SERVERSETUP.md). **Make sure you have opened all the ports and are on a linux machine**.

In order to make this viable in a production setup you need to seperate services onto other hosts. Each host should then have Dashboard-Server installed alongside the service.
E.g. Create a Kerberos server which installs Dashboard-Server, Kerberos, then onto another host install a Postgres Database for Kerberos.

### Step by step guide
1. Download the folder 'SingleServerGuide' from this repository
   1. In ubuntu you can use subversion to download the folder to your current working directory `apt install subversion && svn export https://github.com/jakobhviid/ProjectLeapNode/trunk/SingleServerGuide && cd SingleServerGuide`
2. Change values inside .env to fit your setup
3. Run the following command in your terminal (bash) `docker-compose up`
4. Control output in the console
   1. If you encounter problems try to run `docker-compose down && docker-compose up --build`


