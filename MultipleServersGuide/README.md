## Multiple Servers Guide
For the following steps you need to have access to minimum 4 servers ('server1', 'server2', 'server3', 'server4') which all pass requirements described in [server setup](../SERVERSETUP.md).

This guide has been written for the following versions:
**Kerberos**: 1.1.0
**Zookeeper**: 2.0.0-beta
**Acl-manager**: 1.0.0
**Kafka**: 2.0.0-beta
**Dashboard-Interface**: 1.0.0
**Dashboard-Server**: 1.0.0

#### Step 1/5
On **server1** we install [kerberos](https://hub.docker.com/repository/docker/cfei/kerberos).

1. Download the folder 'Server1' inside the 'MultipleServersGuide' folder from this repository.
   1.  **Ubuntu**: `apt install subversion && svn export https://github.com/jakobhviid/ProjectLeapNode/trunk/MultipleServersGuide/Server1 && cd Server1`
   
2. Change values inside the file '.env' to fit your setup
   1. This step requires you to already know the host url of server2 (zookeeper) and server3 (kafka). If you at this point don't know the ip-addresses you can comment 'KERBEROS_INIT_USERS' out and manually create zookeeper and kafka users later. For this please refer to [kerberos api endpoints documentation](https://github.com/jakobhviid/Kerberos-Server-Docker#api-endpoints).

3. Run `docker-compose up`
   1. **Note**: For a proper setup the postgres database should be put on a different host.

4. Control output
   1. If you encounter problems try to run `docker-compose down && docker-compose up --build`

#### Step 2/5
On **server2** we install [zookeeper](https://hub.docker.com/repository/docker/cfei/zookeeper) and [acl-manager](https://hub.docker.com/repository/docker/cfei/acl-security-manager).

1. Download the folder 'Server2' inside the 'MultipleServersGuide' folder from this repository.
   1.  **Ubuntu**: `apt install subversion && svn export https://github.com/jakobhviid/ProjectLeapNode/trunk/MultipleServersGuide/Server2 && cd Server2`
   
2. Change values inside the file '.env' to fit your setup

3. Run `docker-compose up`
   1. **Note**: For a proper setup zookeeper and acl-manager should be put on two different hosts.

4. Control output
   1. If you encounter problems try to run `docker-compose down && docker-compose up --build`


#### Step 3/5
On **server3** we install [kafka](https://hub.docker.com/repository/docker/cfei/kafka)

1. Download the folder 'Server3' inside the 'MultipleServersGuide' folder from this repository.
   1.  **Ubuntu**: `apt install subversion && svn export https://github.com/jakobhviid/ProjectLeapNode/trunk/MultipleServersGuide/Server3 && cd Server3`
   
2. Change values inside the file '.env' to fit your setup

3. Run `docker-compose up`

4. Control output
   1. If you encounter problems try to run `docker-compose down && docker-compose up --build`

#### Step 4/5
On **server4** we install [dashboard-interface](https://hub.docker.com/repository/docker/cfei/dashboard-interface) alongside a [postgres database](https://hub.docker.com/_/postgres).

1. Download the folder 'Server4' inside MultipleServersGuide from this repository.
   1.  **Ubuntu**: `apt install subversion && svn export https://github.com/jakobhviid/ProjectLeapNode/trunk/MultipleServersGuide/Server4 && cd Server4`

2. Change values inside the file '.env' to fit your setup

3. Run `docker-compose up`

4. Control output
   1. If you encounter problems try to run `docker-compose down && docker-compose up --build`


Try to visit the DNS-resolvable ip of Server4 on port 3000 from a webbrowser.

You should see this:

![interface homepage][interface-homepage]

In the upper right corner, login with the values you specified in the file 'env'. 'DASHBOARD_USER_EMAIL' and 'DASHBOARD_USER_PASSWORD'

![login-page][login-page]

After login, you should see somthing like this:

![after-login][after-login-page]

In the picture above one container has been started as an example. You will not see any containersin the table as we have not installed [dashboard-server](https://hub.docker.com/repository/docker/cfei/dashboard-server) on any servers yet.

Dashboard server is responsible for sending information on containers to the interface.

As soon as Dashboard server is installed we will also be able to create containers from the interface instead of manually setting it up as we have done so far.

This is done by clicking "Run Container" in the lower right corner. Which will bring up this menu:

![create-container][create-container]

So to get all these features and more, let's install dashboard-server in the next step.

#### Step 5/5
On **server1**, **server2**, **server3** and **server4** we install [Dashboard-Server](https://hub.docker.com/repository/docker/cfei/dashboard-server).

On each server do the following:

1. Download the folder Dashboard-Server-Setup inside 'MultipleServersGuide' from this repository.
   1.  **Ubuntu**: `apt install subversion && svn export https://github.com/jakobhviid/ProjectLeapNode/trunk/MultipleServersGuide/Dashboard-Server-Setup && cd Dashboard-Server-Setup`

2. Change values inside the file '.env' to fit your setup

3. Run `docker-compose -f dashboard-docker-compose.yaml up`

4. Control output
   1. If you encounter problems try to run `docker-compose down && docker-compose up --build`

## Interface usage
##### Container Control
In the containers table you can click the three dots which will give you container controls such as start and stop. The table also has a refetch button which you can use to manually refetch.

##### Kerberos & ACL
If you click the paw in the left side. You will see this page:

![kerberos][kerberos]

Here you can create users

##### Notifications
The interface also has notifications.
These notifications are still under development and are currently just a proof of concept. So when a container uses a lot of ressources. You will get a notification as seen below

![notifiaction][notification]

In the future these notifications will be more relevant and will also have a dedicated page for them. The notifications will also have "quick actions" which is recommendations. For example if your kafka / zookeeper cluster all is reporting errors. The interface will be able to detect this and recommend to restart kerberos as it is likely that it is kerberos which is the source of error when they all depend on kerberos.

Features like this comes in 2.0.0


[interface-homepage]: ./Pictures/HomePage.png "Interface Homepage"
[login-page]: ./Pictures/LoginPage.png "Login Page"
[after-login-page]: ./Pictures/AfterLogin.png "After Login"
[create-container]: ./Pictures/CreateContainer.png "Create Container"
[kerberos]: ./Pictures/KerberosCreation.png "Kerberos Creation"
[notification]: ./Pictures/Notification.png "Notification"