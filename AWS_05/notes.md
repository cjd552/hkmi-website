# Amazon Relational Database Service (RDS)

Hosting your own database
- Buying a server (can be $10000)
- electricity bills

Hosting a database in EC2
- for medium-large size data with moderate traffic
- still requires manual setup and OS installation, but AWS provides security

Hosting with a managed DB service (RDS)
- Built by default, you only need to set admin settings
- Only need to optimise the apps, the database is abstracted away
- Is technically still a type of EC2, but with preset defaults

SQL for relational databases, NOSQL for non-relational databases (used JSON, no fixed schema, big data, real time)

# RDS
Relational databases, pay what you use, simple, fast, fully managed

- Default encryption included, both data level and server level
- Access control by security groups

Databases usually don't have many cores, usually more RAM.

The system can be upgraded after creation, but it'll take half an hour and slow down data access.

Usually SSD. Because Amazon's data centres are monitored and use RAID, and the SSDs are replaced periodically.

## Aurora
- primary for data analysis and nonSQL so it supports higher max storage, only for Amazon
- Must use 3 Availability Zones, because they create synchronised mirrors to improve access.
- Will resolve conflicts and sync on its own.
- Distributed writing system means less I/O
- automatic storage scaling
- S3 backups at no additional cost.

## Data locality

Can create a system with a master node for writing, and read-only nodes spread around the world, providing fast real-time data.

You don't know which one is the master, and you don't need to worry about it.

## Backups

Auto: - updates daily at a time of low traffic, and when the database is killed. Can be saved for up to 35 days. Saved in its own area, not counted in the cost, on by default. However, not part of the free plan.

Manual - costs, stored in S3.

## Converting to RDS with Aurora
- Cannot just use a backup from another service, because you cannot directly access the console. You need to use their built in database migration service.

## Database Migration Service

- No need to kill existing running services
- If the table is available in AWS, it will direct reads to AWS.
- Domains have to be changed to AWS in advance.
- CDC Chain Data Capture used to replicate data between instances. Keeps track on what still needs to be done and make corresponding actions between two different instances.
- Can do one source to many targets or many to one migration.
- Oracle can only go to Oracle or Aurora
- For unsupported databases conversions e.g. Oracle to SQL Server, need to use database conversion tools to translate SQL statements to different frameworks

Connect to EC2 means that only that instance can access as set in the firewall rules. don't connect EC2 if you want anyone to access.

If connection timeout, check that the security group allows the correct access e.g. PostgresSQL access.

Use `tnc` to check if endpoint can be accessed (make sure to specify `-port` e.g. `-port 5432`)

## Killing the database

UNTICK the final snapshot, as that will cost money.