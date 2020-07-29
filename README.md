# ProjectLeapNode
ProjectLeapNode is a temporary name for this project.

The project is a combination of multiple services, which combined creates a robust kafka & zookeeper cluster alongside a user friendly admin tool to manage the clusters. This includes both cluster health & notifications but most importantly it has the ability to grant/limit access to the cluster.

In this guide two different guides are described. 

The first guide is for a production ready setup with the use of a UI. The services are spread across 4 servers, this is the recommended approach. After following this guide, you are able to extend the zookeeper & kafka cluster by adding more servers.

The other approach is if you only have a single server. It is not recommended, but can be great in development situations or if you want the project to run and you only have one powerful machine to run it on. Note that this is horrible in regards to uptime and should never be used in production.


[**Multiple Servers Guide (recommended)**](MultipleServersGuide/README.md)


[**Single Server Guide**](SingleServerGuide/README.md)

## Troubleshooting
#### Kafka Cluster ID doesn't match stored ClusterID
In case of Kafka throwing an error in regards to Cluster ID it is due to volume issues. Go inside your volume directory 'containervolumes' on your host machine. Go inside kafka-data and remove the file called 'meta.properties'. Don't delete anything else and be careful!