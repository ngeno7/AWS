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
 Once an AMI is selected, you have to select an instance type. Instance type defines the size of the instance based on a number of parameters: ECUs, vCPUs, Physical processor, clock speed, memory, instance storage, EBS optimized available, Network performance, IPv6 support, Processor architecture, AES-NI, AVX, Turbo.
 
 ##### Instance Purchasing Options
  - On demand instances: 
  
        - Can be launched at any time, used as long as you need, flat rate, used for short-term use cases.
        - Best fit for testing and development purposes.
        - 
  - Reserved Instances: 
  
        - Purchased for a set period of time for reduced cost.
        - All upfront complete payment for 1 or 3 year time frame.
        - Best for long term, predictable workloads.
        - 
  - Scheduled Instances: 
  
        - Pay for reservations for a recurring schedule. eg daily, weekly or monthly.
        - You could set up a scheduled instance to run during that set time frame once a week.
  - Spot Instances: 
  
        - Bid for unused EC2 Compute resources.
        - Cons: No guarantees for a fixed period of time.
        - Fluctuation of prices due to supply and demand.
        - Pros: Purchase large EC2 instances at a very low price.
        - Used for processing data that can be suddenly interrupted.
  - On-demand Capacity Reservations: 
  
        - Reserve capacity based on different attributes such as instance type, 
            platform and tenancy within a particular availability zone for any period of time.
        - Could be used in conjunction with your reserved instance discount.
 
##### Tenancy
Relates to what underlying host your EC2 instance will reside on (Physical server in a data center). 
 - Shared tenancy: 
    - Maybe used by multiple customers.
    - EC2 instance is launched on any available host with the required resources.
    - AWS security mechanisms prevent one EC2 instance from accessing another in the same host.
 - Dedicated instances: 
    - Hosted on hardware no other customer can access.
    - Maybe required to meet compliance.
    - Incur additional charges.
 - Dedicated hosts: 
    - Same as instance but there is additional visibility and control on the physical host.
    - Allows you to use the same host for a number of instances.
    - Maybe required to meet compliance

##### User Data
Allows you to enter commands that will run during the first boot up on that instance.
    - Perform functions upon boot such as pull down any additional software you want.
    - Download latest OS updates.

##### Storage Options
Selecting storage for your EC2 instance will depend on instance selected, what you intend to use the instance for and how critical the data is.
 - Persistent storage: Available by attaching EBS volumes. EBS volumes are separated from the instance. volumes are logically attached Via AWS network. You can             disconnect the volume from the instance maintaining the data.
 - Ephemeral storage: Created by EC2 instances using local storage. Physically attached to the instance. When instance is stopped or terminated, data is lost. If you       reboot the data remain intact.

##### Security
During instance creation, you will be asked to select a security group for your instance. 
In the end of an EC2 creation, you will be asked to select an existing key pair or create and download a new one. A key pair is made up of a public key and private key. The function of key pairs is to encrypt log in information for linux and Windows EC2 instances and then decrypt the same information allowing you to authenticate on to the instance. ***Windows - Private key decrypts this data allowing you to gain access to the login credentials. In linux it allows you to remotely connect to the instance via SSH.***

 - Public key is held and kept by AWS and private is your responsibility to keep and ensure it is not lost.
 - It is possible to use the same key pair on multiple instances.
 - You can set up additional less privileged access controls such as local windows accounts.

    It is your responsibility to maintain and install the latest OS updates and security patches released by the OS vendor as dictacted within the AWS shared responsibility model.

## EC2 Container Service:
This service allows you to run docker-enabled applications packaged as containers across a cluster of EC2 instances. without requiring you to manage a complex and administratively heavy cluster management system. The burdern of running your own cluster management system is abstracted with the ECS service by passing that responsibility over to AWS, specifically through the use of AWS Fargate.
**Container** - Contains everything an application needs to run from within its container package. They are decoupled from the operating system making container applications very portable.
ECS removes the need for you to manage your own cluster management system thanks to its interaction with AWS Fargate.
With ECS there is no need to install any management or monitoring software for your cluster.
#### Launching ECS Cluster:
- **Fargate Launch:**
        Requires you to specify the CPU and memory required, define networking and IAM policies. In addition to you having to package your applications into containers.
- **EC2 Launch:**
        You are responsible for patching and scaling your instances and you can specify the instance type and how many containers should be in a cluster.
#### Monitoring Containers:
Monitoring is taken care of through the use of Amazon Cloudwatch. You can easily create alarms based off of these metrics, providing you notification of when specific events occur, such as your cluster size scaling up and down.

```
Amazon ECS cluster is comprised of a collection of EC2 instances. Features such as Security Groups, Elastic Load Balancing 
and Auto Scaling can be used with these instances.

Clusters act as a resource pool, aggregating resources such as CPU and memory.

Clusters are dynamically scalable and scalable and multiple instances can be used.

Clusters can only scale in a single region.

Containers can be scheduled to be deployed across your cluster.

Instances within the cluster also have a Docker daemon and an ECS agent.
```

## Amazon Elastic Container Registry (ECR)
ECR provides a secure location to store and manage your docker images. This is a managed service, so you dont need to provision any infrastructure to allow you to create this registry of docker images. This service allows developers to push, pull and manage their library of docker images in a central and secure location.

#### Components
  - Registry: The ECR registry allows you to host and store your docker images, as well as create image repositories. Your account will have read and write access by default to any images you create within your registry or any repositories. Access can be controlled via IAM policies in addition to repository policies. Before your docker client can access your registry, it needs to be authenticated as ***AWS User via Authorization Token***
  - Authorization Token: 
  - Repository: These are objects within your registry that allows you to group together and secure different docker images. You can create multiple repositories with the registry allow you to organize and manage your docker images into different categories. Using policies from both IAM and repository policies you can assign set permissions to each repository.
  - Repository Policy: Are resource based policies. You need to ensure you add a principal to the policy to determine who has access and what permissions they have. For an AWS user to gain access to the registry, they will require access to the ***ecr:GetAuthorizationToken*** API call.
  - Image: 

## Amazon EKS - Elastic Container Service For Kubernetes

## AWS Elastic Beanstalk
Is an AWS managed service that takes your uploaded code of your web application and automatically provisions and deploys the required resources within AWS to make web application operational.
These resources include EC2, Auto scaling, application health monitoring and elastic load balancing, in addition to capacity provisioning.
It is able to operate with a variety of platforms and programming languages.
### Components
 - Application Version: Is a specific reference to deployable code. The application version will point typically to S3, simple storage service to where the code may reside.
 - Environment: An environment refers to an application version that has been deployed on AWS resources, which are configured and provisioned by AWS beanstalk.
 At this stage, the application is deployed as a solution and becomes operational within your environment. It is comprised of all the resources created by Elastic Beanstalk not just the EC2 instance with the uploaded code.
 - Environment Configurations: This is a collection of parameters and settings that dictate how and environment will have its resources provisioned by Elastic Beanstalk and how these resources will behave. 
 - Environment Tier: Web server or worker environment.
 - Configuration Template: Baseline for creating new/unique environment configuration.
 - Platform: Is a culmination of components in which you can build your application upon using elastic beanstalk.
 - Applications: Application is a collection of different elements such as environments, environment configurations and application versions.
 - 

## AWS LAMBDA
The AWS lambda is a serveless compute service that allows you to run your application code without having to manage EC2 instances.
It means you dont have to worry about provisioning and managing your compute resource to run your own code, instead it managed and provisioned by AWS.

The service does require compute power to carry out your code requests, but because the AWS user does not need to be concerned with what managing this compute power or where it is provisioned from. It is considered **serveless** from the user perspective.

#### Steps of operations
1. You can either upload your code to Lambda or write with provide code editors. Languages include: **Nodejs, Java, C#, Python, Go, Powershell and Ruby**
2. Configure your lambda functions to execute upon specific triggers from supported event sources.
3. Once the specific trigger is initiated, Lambda will run your code (as per your Lambda function) using only the required compute power as defined.
4. AWS records the compute time in milliseconds and the quantity of Lambda functions run to ascertain the cost of service.
---

## AWS NETWORKING FUNDAMENTALS
Default VPC has: 
    - IPv4 CIDR block
    - /20 default subnet
    - Connected Internet Gateway
    - Security Group (SG)
**RFC1918 Range**
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
It is ideal for a range of use cases where you need high throughput with low latency 
with the added ability of being able to access your data frequently. 
By copying data to multiple availability zones, S3 Standard offers eleven 
nines of durability across multiple availability zones, 
meaning the OData remains protected against a single availability zone failure. 

Versioning allows your data to be identified by its latest version or by earlier versions. 
If you accidentally overwrite some important data, that data can, if you've enabled versioning,
be scored and available for retrieval should you need it.
```
```
Amazon Glacier is an extremely low-cost storage service that provides secure and durable storage for data archiving and backup. 
To keep costs low, Amazon Glacier is optimized for data that is infrequently accessed 
and for which retrieval times of several hours are suitable. 
The standard retrieval option, which is the default option, takes 3-5 hours to complete.
The other options are expedited, which downloads a small amount of data (250 MB maximum) in 5 minutes, and bulk, 
which downloads large amounts of data (petabytes) in 5-12 hours.
```

### S3 Bucket Properties
 - **Standard S3:** 
     - Versioning: Exists on objects in a bucket. Not enabled by default but can be paused (not disabled) once enabled.
     - Server Access Logging: Captures reqs made to bucket or object.
     - Static Website Hosting
     - Object - level logging
     - Default encryption

- **Advanced:**
    - Object lock
    - Tags
    - Transfer Acceleration
    - Events
    - Requester Pays


### Elastic Load Balancer
Helps to manage and control the flow of inbound requests destined to a group of targets by distributing these resources across the targeted resource group. Targets could be a fleet of EC2 instances, lampda functions, a range of IP addresses or even containers.
The targets defined within the ELB could be situated across different Availability Zones or placed within a single AZ.

One of the many advantages of using ELB is the fact that it is managed by AWS.
 #### Components
 **Listeners:** For every load balancer, you must configure at least one listener. The listener defines how your inbound connections are routed to your target groups          based on ports and protocols set as conditions.
 
 **Target Groups:** Is a group of your resources that you want your ELB to route your requests to. You can configure your ELB with a number of different target groups, each associated with a different listener configuration and associated rules.

**Rules:** are associated with each listener that you have configured within your ELB.

**Health checks:** That is performed against the resources defined within the target group. These health checks allow an ELB to contact each target using specific protocol to receive a response.

**Internet-Facing ELB:** The nodes of ELB are accessible via the internet and so have a public DNS name that can be resolved to its public IP address, in addition to an IP address. this allows ELB to serve requests from the internet before distributing and routing the traffic to your target groups.

**Internal ELB:** Has internal IP hence serve requests from the VPC itself.

**ELB Node:** For each AZ selected an ELB node will be placed within that AZ. You need to ensure that you have an ELB node associated to any AZs for which you want to route traffic to. The node are used by the ELB to distribute traffic to your target groups.

**Cross-zone Load balancing:** Depending on which ELB option you select you may have the option of enabling and implementing cross-zone load balancing within your environment.

```
When cross-zone load balancing is disabled, each ELB in its associated AZ will distribute the traffic within that AZ only. 
With cross zone load balancing enabled, the ELB will distribute all incoming traffic between targets.
```

#### Application Load Balancer
Operates on layer 7, application layer. The application servers as the interface for users and application processes to access network services.

#### SSL Server Certificates
The application load balancer provides flexible feature set for your web applications running HTTP or HTTPS protocols.

#### Network Load Balancer
Operates on layer 4 of the OSI model ***(Transport Layer)*** enabling to balance requests purely based on TCP protocol.

#### Classic Load Balancer
Support TCP, SSL/TLS, HTTP and HTTPS protocols. It is considered best practice ALB over classic load balancer unless you have an existing application running in the EC2-classic network.
No longer supported by new AWS accounts.

### EC2 Autoscaling
Is the mechanism that allows you to increase or decrease your EC2 resources based off of custom defined metrics and thresholds.

```
    Automation
    Your infrastructure can elastically provision the required resources preventing your operation
    team from manually deploying and removing resources.
```
```
```
    Greator customer satisfaction
    If you are always able to provision enough capacity within your environment, 
    then its end users will exprerience performance issues.
```

```
    Cost reduction
    With the ability to automatically reduce the amount of resources you 
    have when the demand drops,  you will stop paying for those resources.



#### Components of autoscaling
    - Launch configuration/launch template
    - Autoscaling group
