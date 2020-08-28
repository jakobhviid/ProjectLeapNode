## Server Setup
- Linux OS.
- Docker and docker-compose installed. (**ubuntu**: `sudo apt update && sudo apt install -y docker.io docker-compose`)

## Server Requirements

**Definitions**
- **Network ports** refers to necessary open ports which is used for internal communication between all the servers. 
- **Public ports** refers to DNS-resolvable ports which are used for user connections. Many of the public ports can be changed depending on your docker container setup.

#### Recommended

| Name         |  CPU  |  RAM  | Storage |     Network Ports      |                                Public Ports                                |
| ------------ | :---: | :---: | :-----: | :--------------------: | :------------------------------------------------------------------------: |
| Server1      |   2   |  4GB  |  45GB   |        88, 6000        |                                                                            |
| Server2      |   4   |  6GB  | 100GB+  | 2181, 2888, 3888, 9000 |                                     -                                      |
| Server3      |   4   |  8GB  | 100GB+  |          9092          |                                    9093                                    |
| Server4      |   4   |  6GB  | 100GB+  |          5000          |                                    3000                                    |
| SingleServer |   6   | 12GB  | 250GB+  |           -            | 9091, 9092, 9093, 9094, 9095, 9096, 3000, 5000, 2181, 2888, 3888, 5432, 88 |

#### Minimum

| Name         |  CPU  |  RAM  | Storage |     Network Ports      |                                Public Ports                                |
| ------------ | :---: | :---: | :-----: | :--------------------: | :------------------------------------------------------------------------: |
| Server1      |   2   |  2GB  |  20GB   |        88, 6000        |                                                                            |
| Server2      |   2   |  3GB  |  50GB   | 2181, 2888, 3888, 9000 |                                     -                                      |
| Server3      |   2   |  4GB  |  50GB   |          9092          |                                    9093                                    |
| Server4      |   2   |  3GB  |  50GB   |          5000          |                                    3000                                    |
| SingleServer |   4   |  6GB  |  80GB   |           -            | 9091, 9092, 9093, 9094, 9095, 9096, 3000, 5000, 2181, 2888, 3888, 5432, 88 |

#### Individual Service Requirements
Kafka and zookeeper storage can be increased depending on your needs. If your kafka / zookeeper cluster is huge, you will need to increase storage as they store logs on disk.

| Name                         |  CPU  |  RAM  | Storage |  Network Ports   | Public Ports |
| ---------------------------- | :---: | :---: | :-----: | :--------------: | :----------: |
| Dashboard-Interface          |   2   |  2GB  |   5GB   |        -         |  3000, 5000  |
| Dashboard-Interface Database |   4   |  4GB  |  100GB  |        -         |      -       |
| Dashboard-Server             |   1   |  1GB  |   5GB   |        -         |      -       |
| Kerberos                     |   1   |  2GB  |   5GB   | 88 TCP/UDP, 6000 |      -       |
| Kerberos Database            |   2   |  2GB  |  40GB   |        -         |      -       |
| Zookeeper                    |   1   |  2GB  |  80GB   | 2181, 2888, 3888 |      -       |
| ACL-Security-Manager         |   2   |  2GB  |  20GB   |       9000       |      -       |
| Kafka                        |   4   |  8GB  |  100GB  |       9093       |     9092     |
