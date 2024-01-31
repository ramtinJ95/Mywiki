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


## EC2 Hibernate

