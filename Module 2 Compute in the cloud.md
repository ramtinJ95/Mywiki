# Compute in the cloud

### EC2 pricing
__On-demand__ instances are ideal for short-term irregular workloads that cannot
be interrupted. These run continuesly and you pay only for the compute that time
you use. These are mostly used dev and testing of applications and running
applications that have unpredicated usage patterns.

__Reserved Instances__ 2 different types:
- __standard Reserved Instances__; This option is a good fit if you know the
  type and size of the EC2 instance you need for your steady state applications.
  Here there is the option to specify availability zone (AZ) for your instance.
  If this is done you get EC2 capacity reservation. So you will have the
  resources you want when you want it in that zone.
- __Convertable Reserved Instances__; If you need to run EC2 instances in
  different AZs or need different types then this is the the type for you. At
  the end of a Reserved Instance term, you can continune using the amazon EC2
  instance without interruption. However, you are charged the on-demand prices
  until you either terminate the instance or purchase a new Reserved Instance.
  
  
  __EC2 Instance Savings Plans__; Reduce your EC2 instance costs when you make
  an hourly spend commitment, this results in savings up to 72% compared to
  on-demand prices. These savings are similar to savings provided by standard
  reserved instances. Unlike Reserved Instances you dint need to specify up
  front what EC2 instance type and sizen on and tenancy to get a discount.
  
  __Spot Instance__; are ideal for workloads with felxiable start and end times.
  or thta can withstand interruptions. These instances use unused available
  resources on EC2 and as such if there is nothing available they may not start
  or they may stop if the resourxes are needed for more high prio instance
  types.
  
  __Dedicated Hosts__; are physical servers that Amazon EC2 instance capacity
  that is fully dedicated to your use.
  
  __Scaling__, for scaling of EC2 instances one can use Amazon Autoscaling. Here
  one has to configure 3 thind in the auto scaling group.
  1. Minimium capacity, the capacity that is guranteed and that the instance
     starts with
  2. Desired capacity
  3. Maximum capacity

### Elastic load balancing
load balancer acts as a single point of contact for all incoming web traffic to
the auto scaling group. Although a separate service from the auto scaling group
they are often used together. And one of the main accomplishments of this
elastic load balancing is that one node will never carry all the load.
