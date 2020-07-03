## Multiple Servers Guide
For the following steps you need to have access to minimum 4 servers ('server1', 'server2', 'server3', 'server4') which all pass requirements described in [server setup](../SERVERSETUP.md).

#### Step 1:
On **server1** we install Dashboard-Interface alongside a postgres database
Create a docker-compose file with the following contents:
```
version: "3"

services:
  interface-database:
    image: postgres
    container_name: interface-database
    restart: always
    environment:
      POSTGRES_USER: interface
      POSTGRES_PASSWORD: Interface_database_password1
      POSTGRES_DB: interface_db

  interface:
    image: omvk97/docker-dashboard-interface
    container_name: interface
    ports:
      - 3001:3001
      - 5000:5000
    environment:
      DASHBOARDI_UI_PORT: 3001
      DASHBOARDI_SOCKET_SERVER_PORT: 5000
      DASHBOARDI_POSTGRES_CONNECTION_STRING: "Host=interface-database;Port=5432;Database=interface_db;Username=interface;Password=Interface_database_password1"
      DASHBOARDI_API_KEY: secureapiKey
      DASHBOARDI_JWT_KEY: cfeisecureJWTkey
      DASHBOARDI_API_DNS: https://<<SERVER1_DNS>>:5000
      DASHBOARDI_INIT_USER_EMAIL: testUser@email.com
      DASHBAORDI_INIT_PASSWORD: testUserPassword%1.
    depends_on: 
      - interface-database

```

Now change 'POSTGRES_USER' and 'POSTGRES_PASSWORD' alongside 'DASHBOARDI_POSTGRES_CONNECTION_STRING' to fit accordingly.

Now run the following command in the same directory you created the docker-compose file: `docker-compose up`. Check that the output doesn't contain errors.

Try to visit the DNS-resolvable ip of Server1 on port 3001 from a webbrowser.

In the upper right corner, login with testUser@email.com and password: testUserPassword%1.

TODO: Create images of the relevant pictures of the Dashboard-Interface and put them inside a folder in github repo. in the bottom of this file you should then put references to the pictures

After login, you should see this:

![interface homepage][interface-homepage]



#### Step 2
On server2, server3 and server4 we install the Dashboard-Server in order to remotely install services.

Create a docker-compose file on all three servers with the following contents:
```
version: "3"

services:
  server:
    image: cfei/docker-dashboard-server
    container_name: dashboard-server
    volumes:
      - /var/run/docker.sock:/var/run/docker.sock
    environment:
      SERVER_NAME: <<SERVERNAME>>
```
Change 'SERVER_NAME' accordingly (server2, server3, server4)

Now run the following command in the same directory you created the docker-compose file: `docker-compose up`. Check that the output doesn't contain errors.

#### Step 3

TODO:
Now go to the dashboard interface
PICTURE - CREATE NEW CONTAINER
SELECT Server2
USE database template
CHANGE ENVIRONMENT VARIABLES ACCORDINGLY
RUN CONTAINER, WAIT FOR SUCCESS MESSAGES
CHECK OVERVIEW TO ENSURE IT WORKS

CREATE NEW CONTAINER
SELECT SERVER2
USE kerberos template
CHANGE ENVIRONMENT VARIABLES ACCORDINGLY
RUN CONTAINER, WAIT FOR SUCCESS MESSAGES
CHECK OVERVIEW TO ENSURE IT WORKS

CREATE NEW CONTAINER
SELECT Server3
USE ZOOKEEPER template
CHANGE ENVIRONMENT VARIABLES ACCORDINGLY
RUN CONTAINER, WAIT FOR SUCCESS MESSAGES
CHECK OVERVIEW TO ENSURE IT WORKS

CREATE NEW CONTAINER
SELECT Server3
USE kafka template
CHANGE ENVIRONMENT VARIABLES ACCORDINGLY
RUN CONTAINER, WAIT FOR SUCCESS MESSAGES
CHECK OVERVIEW TO ENSURE IT WORKS

CREATE NEW CONTAINER
SELECT server4
USE ACL-Security-Manager template
CHANGE ENVIRONMENT VARIABLES ACCORDINGLY
RUN CONTAINER, WAIT FOR SUCCESS MESSAGES
CHECK OVERVIEW TO ENSURE IT WORKS


[interface-homepage]: https://unsplash.com/photos/5Oe8KFH5998/download "Interface Homepage"
