# EC2
A virtual machine

Considerations
- Memory
- hard disk space
- How much does CPU need to process
- CPU and memory cannot be changed, everything else can be at any time.
- Network usually isn't as big of a concern, but you may need external network cards.

Choose an instance class based on what your priorities are. e.g. memory, cpu

m5.2xlarge where m is instance class, 5 is generation, 2xlarge is size within instance class

## General Purpose Instance
- Application, gaming, backend servers
- small and medium databases (not recommended, as this is a virtual machine and you don't know when it will die, the hard disk is not mirrored so once it dies you cannot read the data)
     - Can use one instance for processing and another for only storing data, to reduce the risk
     - Use EC2 for storage because it's fast, using EBS tech.
     - EFS can be used in the same way as another EC2 instance, whereas S3 can be accessed from an endpoint, from internal DNS (so no need to go through the edge, unlike from the outside) (These are slower than another EC2 instance.)
     - S3 is not within a regional network, even though it is linked to one.
        - The edge point is the endpoint, you technically are accessing through it, but AWS abstracts away that detail.
- AI model training

- Used for cheap web hosting.
- benefit of there being less restriction on traffic amount.

Data can only be accessed when the instance is running.

SSH port can be changed, but it will inconvenience you as app support defaults to port 22.

## Security groups
- Necessary
- Work as firewalls
- There has to be a security group with SSH access or you can't access the service. otherwise you need a dedicated switchboard machine.
- can be changed at any time