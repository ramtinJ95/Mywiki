EC2 instances change their ips when you start and stop them. If you need to have
a fixed public IP for your instance, you need an Elastic IP. An Elastic IP is
public IPv4 you own as long as you dont delete it and you can attach it to one
instance at a time. You can only have 5 elastic IPs in your account, you can ask
AWS to increase that though.

These elastic IPs can be used to mask the failirue of an instance or software by
rapidly remapping the address to another instance in your account. But these
types of solutions and the use of Elastic IPs should be avoided if possible.

Instead one should use a random public IP and register a DNS name to it, or use
a load balances and dont use a public IP.

## EC2 placement groups
Sometimes we need more control over the EC2 instance placement strategy, in
those cases we can use placement groups. When we create a placement group, we
can specify one of the following strategies for the group:
- Cluster instances into a low-latency group in a __single__ AZ
- Spread instances across underlying hardware (max 7 instances per group per
  AZ), this is mostly used for critical applications.
- Partition, spreads instances across many different partitions within an AZ,
  these paritions rely on different sets of racks. Scales to 100s of EC2
  instances per group.

#### Cluster
For this option all the EC2 instances will be on the same rack, i.e the same
hardware in the same AZ. We would choose this type of setup if we need super
high speeds between our instances since in this configuration there is a 10Gbps
bandwith between the instances.

Obviously the great risk with this setup is that we have a greater risk of
failure since all of our instances sits on the same rack and if that rack
experiences problems then our entire group will go down. Having said this there
is no more performant setup than this so it should be used for use cases that
need such low latency between the instances.

#### Spread
This is the opposite of the Cluster strategy. Here each EC2 instance is on a
seperate rack and we can have instances in different AZ's. This is a super
realiable option since our instances are on different physical hardware spread
in different AZ's so the risk of our service becoming completely unreachable is
pretty much zero. But one con is that we can only have 7 instaces per az per
placement group when using this Spread strategy. This means that we cannot have
super huge and compute intensive workloads using this strategy, it is not
designed for that use case. 

So this is great for applications that need max availability and critical
application where each instance much be isolated from failure from each other.

#### Partition
In the Partition strategy we spread our EC2 instances among different
partitions. Each partition lives on different racks, i.e partition 1 and 2 are
on different hardware racks and thus are isolated from rack failures between
them. We can have up to 7 partitions per AZ and we can have partitions in
multiple AZ's. This allows us to have 100s of EC2 instances running. 

Using this strategy a rack failure could bring down many EC2 instances since we
could have many instances running in each partition but we will never lose all
of our instances since they are on diffrent racks and in different zones. 

EC2 instances get access to the partition information as metadata service. 

This is mostly used for partition aware big data applications such as Kafka,
hadoop and Cassandra. 

## Elastic Network Interfaces (ENI)
Logical component in a VPC that represents a virtual network card. The ENI can
have the following attributes:
- Primary private IPv4, one or more secondary IPv4
- One Elastic IP per private IPv4
- One Public IPv4
- One or more security groups
- A MAC address

You can create ENI indenpendently and attack them on the fly (move them) on EC2
instances for failover. These ENI are bound to a specific AZ. 

for more detailed information read: https://aws.amazon.com/blogs/aws/new-elastic-network-interfaces-in-the-virtual-private-cloud/

## EC2 Hibernate
So in the normal case we working with EC2 instances we know we can stop and
terminate instances. Stopping an instance, then the data on disk when using EBS
( Elastic Block Storage) is kept intact in the next start. Terminating an
instance, then any EBS volumes (root) also set-up to be destroyed is lost. 

Then when we start an EC2 instance the following happens:
- First start: The OS boots and the EC2 User Data script is run
- Following starts: the OS boots up
- Then your applications starts, caches get warmed up, and that can take time! 

So instead we can use EC2 Hibernate:
- The in-memory (RAM) state is preserved
- The instances boot is much faster, because the OS is not stopped / restarted)
- Under the hood: the RAM state is written to a file in the root EBS volume
- The root EBS volume must be encrypted

Use cases:
- Long-running processing
- Saving the RAM state
- Services that take time to initialize

## EC2 Instance Storage Section

#### EBS
An EBS Volume has the following characteristics:
- It's a network drive, i.e not a physical drive
  - It uses the network to communicate with the instance, which means there
    might be a bit of latency.
  - It can be detached from an EC2 instance and attached to another one quickly.

- It's locked to an AZ
  - An EBS Volume in us-east-1a cannot be attached to us-east-1b
  - To move a volume across, you first need to snapshot it

- Have provisioned capacity ( size in GB's and IOPS)
  - You get billed for all the provisioned capacity
  - You can increase the capacity of the drive over time.

__EBS Snapshots__
- Make a backup of your EBS volume at a point in time
- Not necessarry to detach volume to do the snapshot, but recommended
- Can copy snapshots across AZ or Region.
- EBS snapshot archive
  - Move a snapshot to an " archive tier " that is 75% cheaper 
  - Takes within 24 to 72 hours for restoring the archive
- Recycle Bin for EBS snapshots
  - Setup rules to retain deleted snapshots so you can recover them after an
    accidental deletion
  - Specify retention (from 1 day to 1 year )
- Fast snapshot restore (FSR)
  - Force full initialization of snapshot to have no latency on the first use,
    but this is super expensive and should only be used when we have a huge EBS
    with important data that needs to be spun up fast.

__EBS Volume Types__
short overview:
- EBS Volumes come in 6 types
  - gp2/gp3: general purpose SSD volume that balances price and performance for
    a wide variery of workloads
    - Cost effective storage, low-latency
    - System boot volumes, Virual desktops, Development and test environments
    - 1 GiB - 16 TiB
    - gp3:
      - Baseline of 3000 IOPS and throughput of 125 MiB/s
      - Can increase IOPS up to 16000 and throughput up to 1000 Mib/s
        independently
    - gp2:
      - Older generation of general purpose ssds
      - Small gp2 volumes can burst IOPS to 3000
      - size of the volume and IOPS are linked, max IOPS is 16000
  - Provisioned IOPS io1/io2 Block express (SSD): Highest performance SSD volume for mission
    critical low-latency or high-throughput workloads great for database
    workloads.
    - Great for critical business applications with sustained IOPS performance
      requirements or applications that need more than 16000 iops
    - io1 (4 GiB - 16 TiB):
      - Max IOPS 64000 for Nitro EC2 instances & 32000 for other
      - Can increase IOPS independently from storage size
    - io2 Block Express (4 GiB - 64 TiB):
      - Sub-millisecond latency
      - Max IOPS 256000
    - Supports EBS Multi-attach
  - Hard Disk Drives:
    - Cannot be a boot volume
    - 125 GiB to 16 TiB
    - Throughput optimizes HDD(st1):
      - Low cost HDD volume designed for frequently accessed, throughput
      intensive workloads
      - Big Data, Data Warehouses, Log processing
      - Max throughput 500 Mib/s - max IOPS 500
    - Cold HDD (sc1): 
      - Lowest cost HDD volume designed for less frequently accessed
      workloads
      - For data that is infrequently accessed
      - Scenarios where lowest cost is important
      - Max throughput 250 Mib/s max IOPS 250

- EBS Volumes are characterized in Size | Throughput | IOPS
- Only gp2/gp3 and io1/io2 Block Express can be used as boot volumes

__EBS Multi-attach - io1/io2 family__
- Attach the same EBS volume to multiple EC2 instances in the same AZ
- Each instance has full read & write permissions to the high performance volume
- Use case:
  - Achieve higher application availability in clustered Linux applications (ex
    Teradata)
  - Applications mush manage concurrent write operations
- Up to 16 EC2 instances at a time max.
- Must use a file system that is cluster aware (i.e not XFS, EXT4 etc) 

##### EBS Encryption
- When you create an encrypted EBS volume, you get the following:
  - Data at rest is encrypted inside the volume
  - All the data in flight moving between the instance and the volume is
    encrypted
  - All snapshots are encrypted
  - All volumes created from the snapshot are encrypted
- Encryption and decryption are handled transparently
- Encryption has a minimal impact on latency
- EBS encryption leverages keys from KMS (AES-256)
- Copying an unencrypted snapshot allows encryption
- Snapshots of encrypted Volumes are encrypted

To encrypt an unencrypted EBS volume you would do the following:
- Create an EBS snapshot of the volume
- Encrypt the EBS snapshot (using copy)
- Create new EBS volume from the snapshot (the volume vill also be encrypted as
  we know)
- Now you can attach the encrypted volume to the original instance

#### EC2 Instance Store
EBS volumes are network drives with good but "limited" perfomance. If you need a
high-performance hardware disk, use EC2 Instance store instead.

- Better I/O performance
- EC2 Istance store lose their storage if they are stopped ( this is called
  ephemeral storage)
- Good for buffer / chache / scratch data / temp content
- Risk of data loss if hardware fails, since this type of storage is directly
  attached to the hardware which the EC2 instance is running on
- Backups and Replication is your responsibility.

#### Amazon Machine Image (AMI)
- AMI is a customization of an EC2 instance
  - You add your own software, configuration, operating system, monitoring etc
  - Faster boot/configuration time because all your software is pre-packaged
- AMI are built for a specific region (and can be copied across regions)
- You can launch EC2 instances from:
  - A public AMI: AWS provided
  - Your own AMI: you make and maintain them yourself
  - an AWS Marketplace AMI: an AMI someone else made and potentially sells.

#### EFS
- EFS is a managed NFS (network file system) that can be mounted on many EC2
  instances
- EFS works with EC2 instances in multi-AZ
- Highly available, scalable, expensive and pay per use

Overview of Amazon EFS
- Use cases: content managment, web serving, data sharing, Wordpress
- Uses NFSv4.1 protocol
- Uses security group to control access to EFS
- Compatible with Linux based AMI (not Windows)
- Encryption at rest using KMS
- POSIX file system (Linux) that has a standard file API
- File system scales automatically, pay-per-use, no need for capacity planning.

EFS - Performance classes
- EFS Scale:
  - 1000s of concurrent NFS clients, 10 GB/s throughput
  - Grow to Petabyte-scale network file system, automatically
- Performance Mode (set at EFS creating time):
  - General purpose (default) - latency-sensitive use cases (web server, CMS,
    etc)
  - Max I/O - higher latency, throughput, highly parallel (big, data, media
    processing)
- Throughput Mode:
  - Bursting - 1TB = 50 MiB/s burst of up to 100 MiB/s
  - Provisioned set your throughput regardless of storage size, ex: 1 GiB/s for
    1 TB storage
  - Elastic - automatically scales throughput up or down based on your workloads
    - Up to 3GiB/s for reads and 1GiB/s for writes
    - Used for unpredictable workloads
    - 

EFS - Storage classes
- Storage tiers (lifecycle managment feature - move file after N days)
  - Standard: for frequently accessed files
  - Infrequent access (EFS-IA): cost to retrieve files, lower price to store.
    Enable EFS-IA with a lifecycle policy
- Availability and durability
  - Standard: Multi-AZ, great for prod
  - One Zone: One AZ, great for dev, backup enabled by default, compatible with
    IA (EFS one zone-IA)
- Over 90% in cost savings.


#### General discussion around EFS and EBS
