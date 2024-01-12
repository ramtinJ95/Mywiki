# Networking

__Amazon VPC__; enables you to provision an isolated section of th aws cloud. In
this isolated secton, you csn launch resources in a virtual network thta you
define. Within a virtual private cloud (VPC), you van organize your
resourcesinto subnets. A subnet is a section of a vpc that can contain
resources such as EC2 instances. 

For public traffic from the internet to access your VPC, you attach an
__Internet Gateway__ to the vpc. An internet gateway is a connection between a
vpc and the internet. To access private resources in a vpc you can use a virtual
private gateway. The virtual private gateway is the component that allows
protected internet traffic to enter into the vpc. In other words a virtual
private enables you to establish a virtual private network (VPN) connection
between your vpc and a provate network, such as an on-premises dat center or
interal corporate network. A virtual private gateway allows traffivinto the vpc
only if it is coming from an approved network.

__AWS Direct Connect__ is a service that lets you establish a dedicated private
connection between your data center and a VPC. The private connection that aws
direct connect provide helps you reduce network costs and increase the amount of
bandwith tht can travel thorugh your network.

__Network traffic in a VPC__; It is possible to have both private and public
subnets and they can communicate with eath other in a vpc. When a customer sends
a request to an app hosted in aws cloud, this request is sent as a packet. A
packet is a unit of data sent over the internet or a network. It enters into a
VPC through internet gateway. Before a packet can enter into a subnet or exit
from a subnet, it checks doe permissions. These permissons indicate who sent the
packet and how the packet is trying to communicate with the resources in a
subnet. The vpc component that checks packet permissions for subnets is a
network access control list (ACL).

__Network ACL__ is a virtual firewall that controls inbound and outbound traffic
at the subnet level. Each aws account includes a default network ACL. By default
the network ACL allows all inbound and outbound traffic. For custom network ACLs
all network traffic is denied until you add rules to specifiy which traffic to
allow. Additonally,all network ACLs have an explicit deny rule. This rule
ensures that if a packet doesnt match any of the other rules on the list, the
packet is denied. 

Network ACLs perform stateless packet flitering. They remember nothing and check
packets that cross the subnet border each way, inbound and outbound. After a
packet has entered a subnet, it must have its permissons evaluated for resources
within the subnet, such as EC2 instances.

The vpc component that checks packet permissons for say an EC2 instance is a
security group.

__Security groups__ are a virtual firewall that controls inbound and outbound
traffic for an EC2 instance. By default a security group denies all inbound
traffic and allow all outbound traffic. When/if you add custom rules to
configure which traffic should be allowed everthing else is denied. 

Security groups perform stateful packet fuletering. When a packet response for
that request returns to the instance th security group remembers your previous
request. The security group allows the response tp proceed, regardless of
inbound security group roles.

__Amazon Route 53__ is a DNS web service. It gives developers and business a
reliable way to route end users to internet applications hosten in AWS. Route 53
can both route user requeststo infra running in aws and infra outside of AWS.

__Amazon route 53 and cloudfront__:
1. A customer requests data from the application by going to any companies
   website.
2. Route 53 uses DNS resolution to identify any companies corresponding ip
   adress. This info is sent back to the customer.
3. The customers request is sent to the nearest ege location through amazon
   cloudfront.
4. Amazon cloudfront connects the application loaf balancer, which send the
   incoming packet to an amazon EC2 instance
