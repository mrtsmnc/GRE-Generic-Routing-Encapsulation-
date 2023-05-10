# GRE-Generic-Routing-Encapsulation-

GRE (Generic Routing Encapsulation) 
is a protocol that encapsulates the headers of other network layer (OSI layer 3) protocols over the IP header to enable packet routing. It was developed by Cisco Systems as a tunneling protocol. By using GRE tunnels, different networks can be connected to each other, allowing devices in those networks to communicate with each other. To clarify this and provide a configuration example, a simple topology is presented below.

In this example, a GRE tunnel will be created on a simple topology, and the Central Router and Branch Router will be configured to use OSPF, a dynamic routing protocol, to teach each other the Loopback networks on them through this tunnel.

There are several important points to keep in mind when entering commands:

The source and destination IP addresses entered in the tunnel interface must be reachable for the device on which the tunnel is being created. In this example, routes were statically taught to the devices using the "ip route" command with the "network address", "subnet mask", and "next hop IP address".
The tunnel IP addresses must be from the same network.
After these operations, it can be seen that the Central and Branch devices have taught each other the network addresses of the loopback IP addresses, which are 172.0.0.0 /24 and 172.16.1.0 /24, without any additional configuration, through the GRE tunnel they established to the ISP device (Internet Service Provider device).

As in this simple example, private IP addresses can be used in our networks located in different locations through GRE tunnels. Private IP addresses are not normally routable because the same private IP addresses may be used by different individuals and organizations in different locations, making it impossible to perform healthy routing. Through GRE tunnels established between locations, private IP addresses can be securely and seamlessly routed, and different networks using private IPs can be taught to devices. This is the most common use of GRE tunnels.

The working principle of GRE is as follows:

GRE works by encapsulating an IP packet, including the network layer header. After being encapsulated with GRE, a new IP header is added. Thus, the GRE encapsulation contains a network layer header that includes information such as the source and destination IP addresses of the packet. Additionally, because a new network layer header is added outside of the encapsulation, this header also includes the source and destination IP addresses of the GRE tunnel.

When a packet is routed to a GRE tunnel, a GRE header is added to the packet at the entrance of the tunnel, followed by a new network layer header that includes information such as the source and destination IP addresses of the GRE tunnel. Third-layer devices such as routers between the beginning and end of the tunnel use this header for routing. When the packet reaches the end of the tunnel, the GRE header and its network layer header are removed, and the packet is then routed according to the destination IP address in the encapsulated header.

Using the OSI model, GRE can be illustrated as using two third-layer headers in the OSI layer.

Advantages of GRE Tunnels:

Enables the use of various protocols over a network that uses a specific protocol.
Provides a temporary solution for networks with limited number of devices.
Enables the connection of non-permanent subnetworks to each other.
Provides VPN (Virtual Private Network) connectivity in Wide Area Networks (WANs).

GRE Header Structure
C - Checksum Present (bit 0); If this bit is set to 1, the Checksum and Reserved1 fields contain valid information.
Reserved0 (bits 1-12); If any of bits 1-5 are not 0, the packet will be discarded by the receiving device. Bits 6-12 are reserved for future use and are sent as 0, and are not considered.
Ver – Version Number (bits 13-15); Indicates the GRE version, and since there is only one version, all bits should be 0.
Protocol Type (bits 17-32); Specifies the protocol of the encapsulated network layer header in the GRE payload.
Checksum (bits 33-48); This field is used to make the value of the bits in the field 0.
Reserved1 (bits 48-64); A field reserved for future use, and all bits are sent as 0.
