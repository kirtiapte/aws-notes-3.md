# Databases

## Amazon RDS
- OLTP managed relational database
- used for predefined schema, strong transactional capabilities, complex queries
- supports aurora, postgresql, mysql, mariadb, oracle, , microsoft sql
- multi az deployment, read replicas, autoscaling, automated backup, manual snapshots
- AWS responsible, availability, durability, scalability, patches, backups
- customer responsible for - managing users, app optimization-index, tables
- can not ssh to EC2 instance, install patches
- multiaz - standby database different AZ, synchronous replication
- can not connect application to standby  , improves availability but not scalability
- automatic failure- cname recor flipped, if compute, network, storage
- read replicas - reporting and data warehouse
    - your app can connect to read replicas
    - async replication
    - eventual consistency
    - need read replicas to delete explicitely
- enable automatic backups when creating read replicas
- mysql- 5, aurora- 15, , sql server does not support read replicas

### Amazon Aurora
- mysql , postgresql compatible
- 2 copies of data in min 3azs
- uses cluster volume - multiaz storage
- global database - region wide outage, global reads
- deployment options - one writer, one reader, multi writers, serverless
- up 15 replicas
- data in flight - add verts

### review 258 for usage
- when you stop a db instance are you billed - billed for storage, iops, , backups, snapshots but not billed for db instance hours
- need RDS for one year - RDS reserved instances
- database connections- rds proxy

## No SQL database
- no sql key-value document database
- no need to provision a database, create a table, configure read/write capacity
- automatically partition db , maintains 3 replicas in one region
- use cases - user profiles, shopping carts, high volume read and write apps
- use s3 for large objects, dynamodb for smaller objects
- partition key and sory key - data is partitioned using parition key, sorting is done on sort key - optimal performance from dynamodb
### Indexes
- secondary indexes to query on indexes other than primary and sort keys
- local secondary index- same partition key as a primary key but diff sort key, should be created at table creation
- global secondary index - partition and sort key are different from primary key, stored separately from orig table
- query - query using partition key , optional sory keys, filters, max 1 mb
- scan - reads every item , expensive paging above 1mb
### Consistency
- eventual consistency
- request for strong consistent reads - consistentread: true
- supports transactions - twice the cost

### Rad write capacity modes
- provisioned - provision read and write capacity, you will be billed for provisioned capacity, dynamically adjustable, unused capacity can be used in bursts
- on demand - use if workload is spiky, cauing low utilization of provisioned capacity, expensive, use when usage is low 
- 1 capacity unit to read is 4 kb or smaller 
- 1 capacity unit to write 1 kb or mre
- for strongly consistent twice the capacity
- on demand RCU is 8 times the cost of provisioned rcu

### Operations
- AWS data migration service - migrate data from rds to mongodb
- use TTL to automatically expire item
- enable point is time recovery (max 35 days)
- server side and client side encryption (dynamodb encryption client)

### difference dynamo db and RDS - review 272

### DynamoDB Accelerator
- cache in front of dynamodb
- reduce cost - redice rcu
- not recommended for write intensive apps, recommended for read intensive apps

## Elastic Cache
- distributed caching in memory data store
- redis, memcached
### Redis
- caching, session store, chat , queues, message broker, gepspatial apps
- automatic failover in multiaz deployment
- redis cluster - shard - collection of one or more nodes
- one node read/write primary and other read replicas- up to 5 replicas allowed
- primary is replaces in acse of failure, dns entry updated
### Memcached
- speed up dynamic web application  
- pure cache, non persistent, 
- up to 20 cache nodes
- auto discovery and discover cache nodes
- back or restore not supported, snapshots not supported
- use large small nodes

### review 281


# Redshift
- relational database - petabyte scale distributed datawarehouse based on postgresql - OLAP
- RDS - optimzed for OLTP, row based
- MPP, columar data storage, data compression, single node data can be distributed across multiple nodes
- ETL (extract, transform, load), OLAP, business intelligence
- leader node, compute nodes, distribute nodes on multiple azs
- client talk to leader node and query is performed on compute node
- client can not talk to compute nodes
- design tables - compression encoding, sort keys, timestamp based sort keys, how rows are distributed across node,
default row distribution even, based on keys, all (look up tables)
- loading data - simple - sql insert
   - redshift copy s3, dynamodb. emr
   - data pipelines
   - on premise - storage gateway 
   - AWS database migration service
   - prefer copy command
 - workload management - prioritized queue- long running low concurrency
                       - short running queries - 50 concurrent
                       - workload management configuration creation of queues
 - Security - kms, master key, based on master key cluster, database key, data encryption keys
            - IAM cluster permission
 - Operations - can not modify existing cols., add new cols.
 
 
 # Redshift spectrum
- run sql queries on Amazon S3
- configure metadata - define in redshift- uses metadata, s3 unstrcucted data format , parquest, csv, ion,json, avon
- storage is separate from compute
- integrated with Athena and EMr

# EMR - Elastic Map Reduce
- managed hadoop service
- gives access to underlying OS 
- hadoop tools, spark, presto, pig, hive
- log processing insight, click stream analysis, genomic and lifesciences
- stroage - hadoop distributed file system (HDFS), EMR file system
- use HDFS for persistent cluster 24/7 analysis - used EBS or instance storage, transient jobs - EMR file system (s3)

# When to use what
- Amazon EMR - data processing with high customizations, machine learning, grapgh analysis
- Amazon Redshift - complex queries against data warehouse, structured + unstructred data from various sources
- Redshift Spectrum - run queries against S3 without loading data to data warehouse, queries against structured data
- Amazon Athena - no compute cluster needed , ad-hoc queries

# Datalakes
 - data intelligence- collecting, analysing, visualizing
 - single platform storgae, managment, analyics
 - stroage, ingestion - s3 and s3 glacier storage for data lakes
 - ingestion - Amazon Kinesis firehose - streaming data , transform and store to s3
 - Bulk data upload - Amazon Snowball
 - integrate with storage gateway to s3
 - Query in place from s3 and s3 glacier
 1. s3 select - parquest. csv, json
 2. Amazon Athena - adhoc queries , preso
 3. redshift spectrum
 4. store data in parquest format
 5. gzip compression format
 6. Analytics - EMR, Amazon machine learning, Quicksight (visualization)
 , Amzon recognizion (review 340)
 
 ## Data cataloging
 - metadata generation
 - hive metastore catalg
 - AWS glue - simplify data prep
 - Steps for glue - collect data from rds, aurora, redshift, s3, Glue generates data catalog, ready for searching and querying , Apache spark to run jobs, Glue data catalog can be used from Amazon EMR, Athena, Redshift spectrum
 
 ## Data warehouse vs data lake (342)
 - data lake to data warehouse
 
 ## Amazon MSK - managed kafka service (342)
 ## AWS lake formation - data prep for 
 
 # Kinesis
- 
- 
- 

