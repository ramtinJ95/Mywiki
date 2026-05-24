* Packets are small chunks of data sent on the network. Many packets together
make up an image, file or email etc.
* Packet switches are routers and link-layer switches.
* Packets switches are store-and-forward transmission based. Meaning they wait
until they have the full packet before they send it along. The router then
stores the packets in a buffer until they can be sent a long. A router has
finite amount of in and out links and a buffer. So if a packet is ready to be
sent but no free out links are available then it stays in the buffer. If there
is too many packets trying to fit into a packet switch then we have packet loss.
Packet loss means either incoming packets get dropped or packets in the buffer
get dropped
* Forwarding tables are used by the router to decide which out link to send the
  packet to. each packet has an OP address of the destination. So the forwarding
  table maps this destination address to an appropriate outbound link. These
tables are automatically set and updated by a number of routing protocols.
* Circuit switches are the other fundamental of 2 ways to move data through a
network. In Circuit switches the resources needed along the path are reserved
for the duration of the communication. This is not the case for packet switches.
This reserving allows for some hardware and feature grantees such as
transmission rates.
* Packet switching is the dominant and growing switch type. It's more efficient
  and utilizes resources more effectively
* Traceroute is a program that be use to trace the path of a packet from source
  to destination. Coupled with pingplotter once can get nice visualizations.
* Five layer internet protocol stack: Application -> Transport -> Network ->
Link -> Physical
* Application Layer: This is distributed over many end systems with the app in
one end systems using this layer to communicate with other apps. Protocols in
this layer are HTTP, SMTP, FTP. There are some network layer functions which are
done with a specific application layer protocol namely domain name system (DNS)
* Transport Layer: Transports application layer messages between app endpoints.
  There are (in Internet) two protocols TCP and UDP. TCP gives a connection
oriented service to its applications. This service includes guaranteed delivery
of application layer messages to the destination and flow control. TCP also
breaks long messages into shorter segments and provides a congestion-control
mechanism, so that a source throttles its transmission rate when the network is
congested. The UDP protocol provides a connectionless service to its
applications. This is a no-frills service that provides no reliability, no flow
control and no congestion control.
* Network layer: Responsible for moving network layer packets known as datagrams
  from one host to another. The transport layer protocol in a source host passes
  a transport layer segment and a destination address to the network layer. The
network layer then provides the service of delivering the segment to the
transport layer in the destination host. Network layer includes the IP protocol,
which defines the datagram fields as well as how the end systems and routers act
on these fields. There is only in IP protocol and all Internet components that
have a network layer must run the IP protocol. The network layer also contains
routing protocols that determine the routes that datagrams take between sources
and destinations.
* Link Layer: To move a packet form one node to the next node in the route the
network layer relies on the services of the link layer. in particular at each
node the network layer passes the datagram down to the link layer, which delivers
the datagram to the next node along the route. at this next node the link layer
passes the datagram to up to the network layer. The services provided by the
link layer depend on the specific link layer protocol that is employed over the
link. For example, some link layer protocols provide reliable delivery from
transmitting node over one link to receiving node. Note that this reliable
delivery service is different from the reliable delivery service of the TCP,
which provides reliable delivery from one end system to another. Examples of
link layer protocols include Ethernet, WIFI and cable access networks DOCSIS.
* Physical Layer: While the job of the link layer is to move entire link layer
packets from one network element to an adjacent network element, the job of the
physical layer is to move the individual bits within the frame from one node to
the next. The protocols in this layer are again link dependent and further
depend on the actual transmission medium of the link. For example Ethernet has
many physical layer protocols: one for twisted-pair copper wire and another for
fiber etc. 

