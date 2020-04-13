---
title: "Chapter 5 - The Network Layer: Control Plane"
date: 2020-04-09T18:30:00+08:00
weight: 5
---

# Chapter 5 - The Network Layer: Control Plane

## 5.1 Introduction

How to compute, maintain and install flow tables?

![Per-router](intro-per-router.png)

*   **Per-router control**: a routing algorithm runs in each and every router, e.g. OSPF and BGP protocols

![Logically Centralized](intro-logical.png)

*   **Logically centralized control**: a logically centralized controller computes and distributes the forwarding tables, interacts with a control agent (CA) in each of the routers via a well-defined protocol.

## 5.2 Routing Algorithms

The goal of **routing algorithms** is to determine good (with least cost) paths from senders to receivers, through the network of routers.

*   A **centralized routing algorithm** computes the least-cost path using complete, global knowledge about the network. This requires the algorithm somehow obtain this information before calculating. Algorithms with global state information are often referred to as **link-state (LS) algorithms**, can be run at one site or be replicated in every router.
*   A **decentralized routing algorithm** calculate the least-cost path in an iterative, distributed manner. Through iterative process of calculation and exchange of information with its neighboring nodes, a node gradually calculates the least-cost path to a destination. A decentralized routing algorithm is called distance-vector (DV) algorithm.

Another classification is whether the routing algorithm is static or dynamic.

*   In **static routing algorithms**, routes change very slowly over time, often as a result of human intervention.
*   **Dynamic routing algorithms** change the routing paths as the network traffic loads or topology change. A dynamic algorithm can be run periodically or in direct response to topology or link cost changes. They may suffer from problems as routing loops and route oscillation.

A third classification is according to whether they are load-sensitive or load-insensitive.

*   In a **load-sensitive algorithm**, link costs vary dynamically to reflect the current level of congestion in the underlying link. If a high cost associated with a link that is congested, a routing algorithm will tend to choose other routes.
*   Today’s routing algorithms (RIP, OSPF, BGP) are **load-insensitive**, as a link’s cost does not explicitly reflect its current level of congestion.

### 5.2.1 The Link-State (LS) Routing Algorithm

Dijkstra’s algorithm （每次选一个距离最近的点，用它更新其他点的距离，具体略）

### 5.2.2 The Distance-Vector (DV) Routing Algorithm

DV algorithm is

*   iterative
*   asynchronous
*   distributed: each node receives some information from neighbors, performs a calculation and then distributes the results to neighbors

Bellman-Ford equation: $$d(x,y)=\min{c(x,v)+d(v,y)}$$

Each node xxx maintains the following routing information:

*   For each neighbor vvv, the cost $c(x,v)$ from xxx to directly attached neighbor vvv,
*   Node xxx's distance vector $D_x=[D_x(y)]$ , containing xxx's estimate of its cost to all destinations yyy,
*   The distance vectors of each of its neighbors $D_y$​.

![DV](dv.png)

From time to time, each node sends a copy of its distance vector to each of its neighbors. When a node xxx receives a new distance vector from any of its neighbors www, it saves www's distance vector and then uses the Bellman-Ford equation to update its own vector.

Problem and technique:

*   Link failure
*   Routing loop
*   Poisoned reverse

#### Comparison of LS and DV Routing Algorithms

*   Message complexity
*   Speed of coverage: DV can converge slowly and can have routing loops and suffers from count-to-infinity problem
*   Robustness

## 5.3 Intra-AS Routing in the Internet: OSPF

One router is indistinguishable from another in the sense that all routers executed the same routing algorithm to compute routing paths through the network. This model is simplistic for two reasons:

*   Scale: As number of routers becomes large, the overhead involved in communicating, computing and storing routing information becomes prohibitive.
*   Administrative autonomy: an organization should be able to operato and administer its network as it wishes, while still being able to connect its network to other outside networks.

Both of these problems can be solved by organizing routers into **autonomous systems (ASs)** with each AS consisting of a group of routers that are under the same administrative control.

Routers within the same AS all run the same routing algorithm and have information about each other. The routing algorithm running within an autonomous system is called an **intra-autonomous system routing protocol**.

OSPF is a link-state protocol that uses flooding of link-state information and a Dijkstra’s least-cost path algorithm. With OSPF, each router constructs a complete topological map of the AS. Each router then locally runs Dijkstra’s shortest-path algorithm to determine a shortest-path tree to all subnets, with itself as the root node.

With OSPF, a router broadcasts routing information to all other routers in the AS, not just to neighbors. A router broadcasts link-state information whenever there is a change in a link’s state. It also broadcasts a link’s state perodically even if there is no change. The OSPF protocol must itself implement functionality such as reliable message transfer and link-state broadcast. The OSPF protocol also checks that links are operational (via a HELLO message) and allows an OSPF router to obtain a neighboring router’s database of network-wide link state.

Some of the advances embodied in OSPF:

*   **Security**. Exchanges between OSPF routers can be authenticated.
*   **Multiple same-cost paths**.
*   **Integrated support for unicast and multicast routing**.
*   **Support or hierarchy within a single AS**. An OSPF autonomous system can be configured hierarchically into areas.

## 5.4 Routing Among the ISPs: BGP

In the Internet, all ASs run the same inter-AS routing protocol, called the Border Gateway Protocol, known as BGP.

### 5.4.1 The Role of BGP

In BGP, packets are routed to CIDRized prefixes, with each prefix representing a subnet or a collection of subnets. A router’s forwarding table has entries of the form $(x,l)$, where xxx is a prefix and lll is an interface number for one of the router’s interfaces.

As a inter-AS routing protocol, BGP provides each router a means to:

*   **Obtain prefix reachabilitiy information from neighboring ASs**. BGP allows each subnet to advertise its existence to the rest of the Internet.
*   **Determine the “best” routes to the prefixes.** To determine the best route, a router will locally run a BGP route-selection procedure.

### 5.4.2 Advertising BGP Route Information

![BGP](bgp.png)

For each AS, each router is either a **gateway router** or an **internal router**. A gateway router is a router on the edge of an AS that directly connects to one or more routers in other ASs. An internal router connects only to hosts and routers within its own AS.

![eBGP and iBGP](ebgp-ibgp.png)

Pairs of routers exchange routing information over semi-permanent TCP connections using port 179. Each such TCP connection, along with all the BGP messages sent over the connection, is called a **BGP connection**. Furthermore, a BGP connection that spans two ASs is called an **external BGP (eBGP)** (vice versa, **internal BGP (iBGP)**). In order to propagate the reachability information, both iBGP and eBGP sessiona re used.

### 5.4.3 Determining the Best Routes

When a router advertises a prefix across a BGP connection, it includes with the prefix serveral **BGP attributes**. In BGP jargon, a prefix along with its attributes is called a **route**. Two of the more important attributes are AS-PATH and NEXT-HOP.

The AS-PATH attribute contains the list of ASs through which the advertisement has passed. BGP routers also use the AS-PATH attribute to detect and prevent looping advertisements. If a router sees that its own AS is contained in the path, it will reject the advertisement.

The NEXT-HOP is the _IP address of the router interface that begis the AS-PATH_.

#### Hot Potato Routing

![Hot Potato](hot-potato.png)

In hot potato routing, the route chosen is that route with the least cost to the NEXT-HOP router beginning that route.

Hot potate routing is a selfish algorithm - it tries to reduce the cost in its own AS while ignoring other components of the end-to-end costs outside its AS.

In pratice, BGP uses an algorithm that is more complicated than hot potato routing. For any given destination prefix, the input into BGP’s route-selection algorithm is the set of all routes to that prefix that have been learned and accepted by the router. If there are multiple routes to same prefix, then BGP sequentially invokes the following elimination rules until one route remains:

1.  A route is assigned a **local reference** value as one of its attributes. The local preference could have been set by the router or could have been learned from another router in the same AS. The value of the local preference attribute is a policy decision that is left entirely up to the AS’s network administrator. The routes with the highest local preference values are selected.
2.  From the remaining routes, the route with shortest AS-PATH is selected.
3.  From the remaining routes, the route with the closest NEXT-HOP router is selected (hot potato).
4.  If more than one route still remains, the router uses BGP identifiers to select the route.

### 5.4.4 IP-Anycast

BGP is often used to implement the IP-anycast serice, which is commonly used in DNS.

![IP Anycast](ip-anycast.png)

During the IP-anycast configuration stage, the CDN company assigns the _same_ IP address to each of its servers and uses standard BGP to advertise this IP address from each of the servers.

When a BGP router receives multiple route advertisements for this address, it treats these advertisements as providing different paths to the same physical location (different actually). Each router will locally use the BGP route-selection algorithm to pick the best route to that IP address.

### 5.4.5 Routing Policy

（一些设置策略，略）

### 5.4.6 Putting the Pieces Together: Obtaining Internet Presence

*   IP addressing
*   Domain name and DNS
*   BGP propagation

5.5 The SDN Control Plane
------------------------------------------------------

Four key characteristics of an SDN architecture:

*   **Flow-based forwarding.** Packet forwarding by SDN-controllered switches can be based on any number of header field values in the transport-layer, network-layer or link-layer header.
*   **Separation of data plane and control plane.**
*   **Network control functions: external to data-plane switches.**
*   **A programmable network.** The network is programmable through the network-control applications running in the control plane.

### 5.5.1 SDN Controller and SDN Network-control APplications

![SDN Architecture](sdn.png)

A SDN controller’s functionality can be broadly organized into three layers.

*   **A communication layer: communicating between the SDN controller and controlled network devices.** SDN controller controls the operation of a remote SDN-enabled switch, host or other devices. A device must be able to communicate locally-observed events to the controller. These events provide the SDN controller with an up-to-date view of the network’s state.
*   **A network-wide state-management layer.**
*   **The interface to the network-control application layer.** The northbound API allows network-control applications to read/write network state and flow tables within the state-management layer.

![SDN Components](sdn-components.png)

### 5.5.2 OpenFlow Protocol

The OpenFlow protocol operates between an SDN controller and an SDN-controlled switch or other device implementing the OpenFlow API. The OpenFlow protocol operates over TCP, with a default port number of 6653.

Among the important messages flowing from the controller to the controlled switch are the following:

*   **Configuration.** Allows the controller to query and set a switch’s configuration parameters.
*   **Modify-State.** Used by a controller to add/delete or modify entries in the switch’s flow table.
*   **Read-State.** Collect statistics and counter values from the switch.
*   **Send-Packet.** Send a specific packet out of a specified port at the controlled switch.

Among the messages flowing from the switch to the controller are the following:

*   **Flow-Removed.** Inform the controller that a flow table entry has been removed.
*   **Port-Status.** Inform the controller of a change in port status.
*   **Packet-in.** A packet arriving and not matching any flow table entry is sent to the controller for additional processing. (Matched packets may also be sent as an action taken on a match.)

An example in link-state change:

![SDN Scenario](sdn-change.png)

### 5.5.4 SDN: Past and Future

（略）

## 5.6 ICMP: The Internet Control Message Protocol

ICMP is used by hosts and routers to communicate network-layer information to each other. The most typical use of ICMP is for error reporting.

ICMP is often considered part of IP, but architecturally it lies just above IP, as ICMP messages are carried inside IP datagrams. When a host receives an IP datagram with ICMP as the upper-layer protocol, it demultiplexes the datagram’s contents to ICMP.

ICMP messages have a type and a code field, and contain the header and the first 8 bytes of the IP datagram that caused the ICMP message to be generated in the first place.

The well-known ping program sends an ICMP type 8 code 0 message to the specified host. The destination host, seeing the echo request, sends back a type 0 code 0 ICMP echo reply.

Source quench message is designed to perform congestion control - to allow a congested router to send an ICMP source quench message to a host to force that host to reduce its transmission rate.

Traceroute is implemented with ICMP messages. According to the rules of the IP protocol, the $n-th$ router observes that the TTL of $n-th$ datagram (is set to nnn originally) has just expired, the router discards the datagram and sends an ICMP warning message to the source (type 11 code 0). This warning message includes the name of the router and its IP address.

One of the datagrams will eventually arrive the destination host, with a UDP segment with an unlikely port number, the destination host sends a port unreachable ICMP message (type 3 code 3) back to the source. The source would know it does not need to send additional probe packets.

## 5.7 Network Maganement and SNMP

Network management includes the deployment, integration, and coordination of the hardware, software, and human elements to monitor, test, poll, configure, analyze, evaluate, and control the network and element resources to meet the real-time, operational performance, and Quality of Service requirements at a reasonable cost.

*   MIB = Management Information Base
*   SNMP = Simple Network Management Protocol
*   PDU = Protocol Data Unit

![Network Management](network-management.png)

The Simple Network Management Protocol version 2 (SNMPv2) is an application-layer protocol used to convey network-management control and information messages between a managing server and an agent executing on behalf of that managing server.

The most common usage of SNMP is in a request-response mode in which an SNMP managing server sends a request to an SNMP agent, who receives the request, performs some action, and sends a reply to the request. Typically, a request will be used to query (retrieve) or modify (set) MIB object values associated with a managed device. A second common usage of SNMP is for an agent to send an unsolicited message, known as a trap message, to a managing server. Trap messages are used to notify a managing server of an exceptional situation (e.g., a link interface going up or down) that has resulted in changes to MIB object values.