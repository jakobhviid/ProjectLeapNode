## Multiple Servers Guide
For the following steps you need to have access to minimum 4 servers ('server1', 'server2', 'server3', 'server4') which all pass requirements described in [server setup](../SERVERSETUP.md).

During this guide we will visit each server twice.

#### Step 1/5
On **server1** we install kerberos.

1.1 - Download the folder 'Server1' inside the 'MultipleServersGuide' folder from this repository.

1.2 - Change values inside the file '.env' to fit your setup

1.3 - Run `docker-compose up`

1.4 - Control output

#### Step 2/5
On **server2** we install zookeeper, acl-manager and dashboard-server.

#### Step 3/5
On **server3** we install kafka and dashboard-server

#### Step 4/5
On **server4** we install Dashboard-Interface and dashboard-server alongside a postgres database.

4.1 - Download the folder 'Server4' inside MultipleServersGuide from this repository.

4.2 - Change values inside the file '.env' to fit your setup

4.3 - Run `docker-compose up`

4.4 - Control output

Try to visit the DNS-resolvable ip of Server1 on port 3000 from a webbrowser.

In the upper right corner, login with the values you specified in the file 'env'. 'DASHBOARD_USER_EMAIL' and 'DASHBOARD_USER_PASSWORD'

TODO: Create images of the relevant pictures of the Dashboard-Interface and put them inside a folder in github repo. in the bottom of this file you should then put references to the pictures

After login, you should see this:

![interface homepage][interface-homepage]

The tables are empty, but we now have all the necesarry containers to install dashboard-server on all our servers.

#### Step 5/5
On **server1**, **server2**, **server3** and **server4** we install Dashboard-Server.

On each server do the following:

5.1 - Download the folder Dashboard-Server-Setup inside 'MultipleServersGuide' from this repository.

5.2 - Change 'KAFKA_URL' and 'SERVER_NAME' inside 'dashboard-docker-compose.yaml'




[interface-homepage]: ./Pictures/test.jpeg "Interface Homepage"
