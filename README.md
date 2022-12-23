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


