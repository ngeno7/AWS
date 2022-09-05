# AWS Essentials

## Amazon Elastic Compute Cloud

```
Foundational services in which AWS is based:
    - Compute
    - Storage
    - Database
    - Network
 ```
 
### Compute
Considered brains and powers required by applications and systems to carry out computational tasks via series of instructions.
#### Amazon EC2 - Elastic Compute Cloud
EC2 instance can be broken down into
  - Amazon Machine Images (AMIs)
  - Instance Types
  - Instance Purchasing Options
  - Tenancy
  - User Data
  - Storage Options
  - Security
 
 ##### AMIs
 Are essentially templates of preconfigured EC2 instances which allow you to launch a new EC2 instance based on the configuration within the AMI.
 An AMI is an image baseline within an OS and application along with any custom configuration.
 ##### Instance Types
 Once an AMI is selected, you have to select an instance type. Instance type defines the software of the instance based on a number of parameters.
 ##### Instance Purchasing Options
  - On demand instances: Can be launched at any time, used as long as you need, flat rate, used for short-term use cases.
  - Reserved Instances: Purchased for a set period of time for reduced cost.
  - Scheduled Instances: Pay for reservations for a recurring schedule. eg daily, weekly or monthly.
  - Spot Instances: Bid for unused EC2 Compute resources. Purchase large instances at a low price.
  - On-demand Capacity Reservations: 
##### Tenancy
Relates to what underlying host your EC2 instance will reside on (Physical server in a data center). 
 - Shared tenancy: Maybe used by multiple customers.
 - Dedicated instances: Hosted on hardware no other customer can access.
 - Dedicated hosts: Same as instance but there is additional visibility and control on the physical host.
##### User Data
Allows you to enter commands that will run during the first boot up on that instance.
##### Storage Options
Selecting storage for your EC2 instance will depend on instance selected, what you intend to use the instance for and how critical the data is.
 - Persistent storage: Available by attaching EBS volumes. EBS volumes are separated from the instance. volumes are logically attached Via AWS network. You can disconnect the volume from the instance maintaining the data.
 - Ephemeral storage: Created by EC2 instances using local storage. Physically attached to the instance. When instance is stopped or terminated, data is lost. If you reboot the data remain intact.

##### Security
During instance creation, you will be asked to select a security group for your instance. In the end of an EC2 creation, you will be asked to select an existing key pair or create and download a new one.
A key pair is made up of a public key and private key.


## AWS NETWORKING FUNDAMENTALS
Default VPC has: 
    - IPv4 CIDR block
    - /20 default subnet
    - Connected Internet Gateway
    - Security Group (SG)
** RFC1918 Range **
Avoid ranges that override with other networks to which you might connect.
#### Security Groups
    - Operates at the instance level
    - Support allow rules only
    - Is stateful, return traffic is automatically allowed regardless of any rules.
    - All rules evaluated before deciding whether to allow traffic.
    - Applies only to instances explicitly associated with the security group.
#### Network ACL
    - Operates at subnet level.
    - Supports allow and deny rules.
    - Is stateless, return traffic must be explicitly allowed by rules.
    - Rules evaluated in order when deciding whether to allow traffic.
    - Automatically applies to all instances launched into associated subnets.
#### Flow log
View the connection logs

## VPC Peering
- Full private IP connectivity between two VPCs.
- Can Peer VPCs accross regions.
- VPCs can be in different accounts.
- VPC CIDR ranges must not overlap.

## VPC - Virtual Private Cloud
- Is an isolated segment of the AWS infrastructure allowing you to provision your cloud resources.
- 5 vpcs are allowed per region.
### Subnets
 VPC must have a name and CIDR block address.
    - Public subnet: accessible from the internet. have private and public IP addresses. Has a route to the internet gateway.
    - Private subnet: Routed to the local vpc
 Internet Gateway: Managed component on the VPC that acts as a gateway to the internet

### NACL - Network Access Control Lists
- A way of controlling how traffic comes in or out of a subnet.
- Stateless: Any traffic has to be configured either inbound or outbound.
### Security Groups
Act as a virtual firewall at the instance level.
It is statefull. Only the defined rules will be used else other traffic that does not meet will be dropped. Has **no deny** rule

### NAT Gateway
 Allows private subnets to access the internet while blocking connections initiated from the internet.
 This allows for patch management so as the instances stay up to date.
### Bastion Hosts
Allow access to the private EC2 instances from remote.
Local user connect to the BH and then can connect from it to the private subnet.

## VPC Connectivity

### VPN - Virtual Private Network
It is a secure way of connecting to a remote network.
    - Customer Gateway
    - VPN tunnel
    - Virtual Gateway
    - **Dynamic and static routing**
 
    Process:

    1. You need to create a virtual gateway and this attaches directly to your VPC
    2. In the data center we create customer gateway.
        Info needed about customer gateway include:  IP address and the type of routing to be used (i.e dynamic or static).
    3. Customer Gateway initiates connection to VGW. 

   ```If there was some idle activity across this link for a period of 10 seconds or more, then this VPN tunnel connection would drop. So, to prevent that from dropping, you can set up network monitoring to set up continuous network pings from the customer gateway side to the virtual gateway to ensure that connection remains up and running.
   SG in the private subnet has to be configured also to allow traffic to be btw CG and VGW
   SG rules allow SSH and RDP types and DC IP address block.
   ```
## AWS S3
Object based storage services. Space is btw 0 bytes and 5 terrabytes.
Storage exists across a flat address space. To store data in a s3 you must first create a bucket with a unique name.

``` 
S3 Standard. This storage class is considered a general-purpose storage class. 
It is ideal for a range of use cases where you need high throughput with low latency with the added ability of being able to access your data frequently. 
By copying data to multiple availability zones, S3 Standard offers eleven nines of durability across multiple availability zones, 
meaning the OData remains protected against a single availability zone failure. 

Versioning allows your data to be identified by its latest version or by earlier versions. 
If you accidentally overwrite some important data, that data can, if you've enabled versioning,
be scored and available for retrieval should you need it.
```
```
Amazon Glacier is an extremely low-cost storage service that provides secure and durable storage for data archiving and backup. 
To keep costs low, Amazon Glacier is optimized for data that is infrequently accessed and for which retrieval times of several hours are suitable. 
The standard retrieval option, which is the default option, takes 3-5 hours to complete.
The other options are expedited, which downloads a small amount of data (250 MB maximum) in 5 minutes, and bulk, 
which downloads large amounts of data (petabytes) in 5-12 hours.
```
