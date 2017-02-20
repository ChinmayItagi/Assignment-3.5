Q1 
Combination of the different namenodes in order to get lager cluster and also the secondary name node does not make the primary free from data loss. That is still the namenode is single point of failure. Even if the new namenode is formed it will take min 30 min to come to full functionality. In order to get solution for the above problems Hadoop 2.x came up with solution of high availability, in this two namenodes are created in active and stand by functionality.  In this even if the active namenode fails the standby becomes active and takes over the functionality of the other namenode without any kind of human intervention and no down time.
The Architectural Changes that have to done in Hadoop 2.x are 
1)	The namenodes must have shared storage space to share the edit logs.
2)	Datanodes must send the block mappings to both the nodes.
3)	Clients must be programmed to handle the node failure in transparent to the users.
4)	The secondary namenode’s role is subsumed by the standby, which takes periodic
checkpoints of the active namenode’s namespace.



Q2
As the name suggests the check pointing is just keeping a check on the data and what modifications haven taken place the mapping of the data. This process of check pointing is always done on secondary namenode and is done in the following way.
As we know fsimage is the image of the file system. Suppose that if the file system crashes then the file system can be brought to its stable state by using the fsimage. But it is not feasible to always keep on changing the fsimage even when small amount of changes are done to the file system. Hence instead of that the changes are first noted down in the edit logs and then when the check pointing time comes the edit logs as well as the last fsimage are merged and new fs image is formed. This merging of the old fsimage and the edit logs to get new fsimage is done in the secondary namenode. Once the new fs image is created then it is given back to the primary namenode. This is very efficient process and very less time to start a namenode. The check pointing process can be periodically performed with the configured time. In real world scenario the time is somewhat more than 60 min. 


Q3
With Hadoop 1.x only one name space can be generated and handle a cluster of only max 4000 nodes but these are not  enough for recent times where clusters have to big e.g yahoo, 
facebook etc. In order to provide solutions for this the Hadoop federation came into existence
The Hadoop federation implements 2 or more namenodes which are totally independent. These name spaces are federated that is, they do not require any co-ordination. Datanodes are used as the common  storage and each of the datanode is registered with each of the namenode.
Advantages of the Hadoop federation are – scalability and isolation, Generic Storage Device, Simple Design.


Q4

The configuration files that are to be edited while installing a hadoop cluster are :

   1) Core-site.xml
   2) HDFS-site.xml
   3) YARN-site.xml
   4) xml
1) Core-site.xml :-
  1.Name node address configuration
  2.Rack awareness configuration
  3.Select type of security
2) Setting up HDFS
	
	1.Select the access port
	2. Ss1 client authentication
	3. Network interface configuration
	4. Changing file permission. 
3) Settings to be done in YARN-site.xml :- 
	1. Configure WebAppProxy. 
	2. Configure  MapReduce. 
	3. Configure  NodeManager. 
	4. Configure ResourceManager. 
	5. Configure  IPC.


