# VPC
Virtual Private Cloud

Each account can have 5 VPC

* All devices are within the AWS Cloud network
* There are different regions within the network, which can have different contents. There are multiple data centres in each availability zone, and services are only available within their availability zone.
* Each availability zone is within a region. If you want multiple regions, you need multiple VPCs.
    * Splits the workload between different physical Amazon data centres in the region. In Hong Kong you can split across at most 3 zones as there are 3 data centres, but you don't know which is which as it is set internally.
    * The availability zone allows for network load balancing.
* Your VPC can cross multiple availability zones.
* Within each availibility zone in the VPC you have a _public subnet_ and a _private subnet_.
    * Public - website, application data
    * Private - database, cisco, machine learning
    * There are solutions that allow for data from the private network to enter the public network and vice versa, by specifiying a particular device from the public network and connecting to a specified router.
    * You can also restrict access to the service to specific IP addresses.
    * The different availbility zones can connect to each other.

## IP addresses in AWS
* IPV4
    * Public IPv4
        * EC2 instance gets new one each time you stop and start
    * Private IPv4
        * Fixed for EC2

* IPv6
    * Not used as much as not supported by every device

* Elastic IP
    * Fixed public IPv4 address that allows access to your device.
    * If not attached to an active EC2 instance, has cost
    * Not really used

## VPC and Subnets
* VPC - Virtual Private Cloud
    * Put many services and components _(regional resources)_ into your private network
    * Partitioned by availability zone
    * Has public and private subnet
    * Uses route tables
        * Port forwarding 
        * Security

1) You enter a subdomain or elastic IP provided by AWS
2) Your IP is checked by AWS Cloud to check your permissions and which port you are connecting to, conducts DNS lookup
3) Takes you within the VPC
4) VPC routing table checks what service you need to use and connects you to the correct internal port for the web service

### Subnet IP ranges
* Can limit the number of devices connecting to the services
* Allows you to split between groups / teams / departments / regions
* Can be used to manage costs

## NAT Gateways
Network Address Translation
* You make a request (local IP address labelled as server, server domain name as reciever)
* Send data packages to the router (NAT translates local IP address to router's IP address, recording the ID of the request in a lookup table)
* The router sends the package to the server
* The server responds by sending packages back, via the router (NAT translates router's IP address back to your local IP address, checking the request ID in the lookup table to find the correct destination)

Public access requirements
1) Internet Gateways
    * Allow for the service to access online resources, but not necessarily for others to access the service from online.
    * For the entire VPC, has to go through the VPC and routing table first.
    * Relies on DNS lookup and routing table to find your device through the domain and port forwarding, or IP address.
    * Through AWS, so you need external services to manage security rules, and you have to set them for each server.
    * Free
2) NAT Gateway
    * Allows for others to access your subnetwork and access the service.
    * For the subnetwork, directly accesses using a direct routing table.
    * The benefit is you manage it yourself, including firewall, blacklist and whitelist, which can be set globally for the VPC.
    * More convenient
    * Costs money

## IP ranges
You can calculate the IP ranges for your subnets using a calculator.

* 10/8 prefix
* 172.16/12 prefix
* 192.168/12 prefix

> A CIDR block is expressed as <IP Address>/<Prefix Length>, where the IP address denotes the starting point of the network, and the prefix length specifies the number of bits designated for the network segment. For instance, the CIDR block 192.168.0.0/24 indicates that the initial 24 bits are reserved for the network, allowing the remaining 8 bits for host devices, resulting in a total of 256 possible addresses (ranging from 192.168.0.0 to 192.168.0.255).
>
>CIDR blocks and subnet masks often work together in a network. A network may be allocated a CIDR block, such as 192.168.0.0/16, which represents a large range of addresses. Within this range, subnet masks are applied to divide the network into smaller subnets, such as 192.168.1.0/24 for a smaller department or group of devices.
https://nrs.help/post/cidr-blocks-vs-subnet-masks/

## Security rules
* Network ACL
    * Allow and Deny rules
    * Use only IP address
    * Attached at subnet level, controls traffic to and from subnet

* Security Groups
    * Allow rules only
    * Use IP address and other security groups
    * Connects to EC2
    * Mainly used

## VPC Peering
A paid feature that allows for direct connection between different VPC, whereas normally you cannot and have to go through the internet and back into AWS Cloud again (which is free). Not often required, usually most use cases just need one VPC with multiple servers.

## VPC Endpoints
A domain provided by AWS unique within a region, allowing you to connect to a service. Each one corresponds to a service. Services such as S3, DynamoDB (non-relational databases) require an endpoint. Otherwise, you can use an IP address.

## PrivateLink
Allows for other VPCs to connect to a VPC without using peering, internet gateway, NAT or route tables. It allows you to use services from someone else's VPC.

## Setting up VPC
* Only VPC
* VPC and more - makes 2 subnetworks per availability zone, 3 routing tables, 1 internet gateway, 1 endpoint

* Renting
    * You can pay to host on your own internal network instead of on AWS servers.

Once you have set up the amount of IPs, you can't change it, you'll just have to delete it and make the services again.

Subnet CIDR typically is VPC CIDR + 4

Must tick DNS, as internal IP addresses may fluctuate, so there should be a device DNS name.

Even after generating the subnets, there are no routes established yet, so you have to go in and manually configure the routing table.

The private subnets should not be directly connected to the VPC, only the public subnets, for security reasons. Instead have a separate routing table for the private networks.

You can use the routing table to connect to the internet gateway to make a connection to the wider internet, and set a particular restriction on subnetwork or IP range for which one

Main things to do with routing tables
* Link subnetworks to the routing table, and then you can link them to the wider internet. All network actions need to be done through the routing table

# EC2
Elastic Compute Cloud

It's a virtual machine. It's best to keep your important data in a separate database service.

You can choose a different type of EC2 instance for your use case, though it can be a bit hard to decide.

Charges by uptime, not by amount of people accessing

m5.2xlarge

m - instance class (t = testing)
5 - generation (AWS improves them over time by replacing better servers)
2xlarge - size within the instance class

## General Purpose Instance
Balances computing, memory and networking resources.
Purposes:
* Application servers
* Gaming servers
* Backend servers for companies
* Small and medium databases

## Storage Optimised Instances
Best for large datasets on local storage

## Security Groups
Controls what users and software can access the EC2 instances. Acts as a firewall.