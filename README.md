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


