# S3
Simple Storage Service

A basic version of a cloud storage similar to Google Drive but no smart features.

Free for small sizes (1-2GB). Payment is based on traffic, not file sizes.

- document library, allows for endpoint access

## Bucket
- Container for objects
- Has a unique name per region, not just per VPC
- has a url in the format
`https://bucket-name.s3.Region.amazonaws.com/key name`

e.g.
`https://my-bucket.s3.us-west-2.amazonaws.com/puppy.png`
- Provides version control, allowing multiple variants of an object, as well as who submitted a version
    -  Similar to SharePoint
- No need to host, and provides maintenance and access control.
- Can be replicated across multiple regions, by syncing a "master" bucket to other buckets across other regions.
- Can have different types depending on use case e.g. frequent or infrequent access
    - General purpose
    - Collaborative real-time editing
        - Not hot or cold data (Level 2)
        - Uses SSD
    - High Performance (data that needs instant access e.g. Big Data)
        - Hot Data (Level 1)
        - Uses SSD
    - Infrequent Access
        - Uses HDD
        - Cold Data (Level 3)
    - Glacier (Storing for a long time, you don't need to access it unless necessary)
        - Very Cold Data (Level 4)
        - Low cost
        - Uses Floppy Disks (yes really)
            - More robust against natural disasters such as earthquakes and flooding, and long-lasting

### AWS Lambda
For people who don't know how to write commands, but it lets you run pre-written programs.

## Object
- Everything is an object, this is a fundamental entity
- Identified by a Key
- Has attributes

## Keys
- Every object in a bucket has exactly one
- A unique identifier
- usually a file name

Turn on ACL if it is public access, otherwise ACL turn off.

The creator will be the owner, unless you turn on ACL, then you can set it as an IAM user.

If you set it to public, anyone can access it using the url. Otherwise, you have to configure IAM users.

Object ACL - can manage who sees it

free trial: 5GB standard storage

Start charging you at 1GB and charges per GB up to a threshold.

Convenient access through an AWS endpoint.

No fixed size, can put as much as you want.

# AWS-EBS
Elastic Block Storage

- no free version
- Backup, Snapshots, used in VM
- High speed, reliable storage, allows for convenient cloning.
- Creates a virtual hard disk (that uses an actual hard disk) can be used for EC2, Databases
- Used for services to upload data, faster because you are directly accessing the hard disk rather than going through an endpoint.
- SSD, HDD or Floppy (cost high to low)
- No endpoint
- Just need to choose EBS and add it to your instance.

Elastic because the *size is variable* and you can make it *automatically extend* (instantaneous)

EBS can have *snapshots*, a point in time backup that you can restore to. These can be stored in EBS itself, if storing to S3 is a bit slow. EC2 and databases also have snapshot functionality.

# AWS-EFS
Elastic File Storage

- no free version
- for storing file base data, allows network drive mounting
- A drive that has to be manually mapped to a VPC and mounted to an IP or endpoint DNS.
- file base, not a drive, can be extended but takes time (5 to 10 minutes)
- cheaper
- allows for direct access as a network drive, unlike EBS and S3.
- cannot be accessed through a web service endpoint.