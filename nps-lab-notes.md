# NPS Lab - Important Points

Refer to [this Github Repository](https://github.com/ananyagupta6/NP-LAB) for all lab codes.

## Lab 1
> 5 components of a computer network -> Sender, Receiver, Message, Transmission medium, Protocols

A machine (client) makes a request to connect to another machine (server) for providing some service. The services running on the server run on known ports (application identifiers) and the client needs to know the address of the server machine and this port in order to connect to the server. On the other hand, the server does not need to know about the address or the port of the client at the time of connection initiation. The first packet which the client sends as a request to the server contains these information about the client which are further used by the server to send any information. Client (Active Open) acts as the active device which makes the first move to establish the connection whereas the server (Passive Open) passively waits for such requests from some client.


### Socket Programming

- Same machine: signals/pipes
- Different machine: sockets (full-duplex communication)
- Berkeley API for UNIX C
- Socket = IP Address + Port Number `192.168.1.2 49152`
- Communication services: TCP (Connection-oriented i.e. establish connection first) and UDP (Connectionless i.e. just transfer the data)
- TCP uses Stream Sockets (use when you need reliability in the connection) and UDP uses Datagrams 
- Use cases: TCP (file transfers, sending emails) and UDP (audio/video streaming)

### For TCP

Client: Create a socket, Establish a connection, Send/Receive data, Close the socket
Server: Create a socket, Bind the socket (attach a local address to the socket), Listen for requests, Accept a connection, Send/receive data, Close the socket

![](https://raw.githubusercontent.com/nandiniproothi/nps-lab-notes/main/img/tcp-socket.png?token=ALD5GB7QNU5FG2L2BTU3DMC754X7G)

### For UDP

Client: Create a socket, Send/Receive data
Server: Create a socket, Bind the socket (attach a local address to the socket), Send/receive data

![](https://raw.githubusercontent.com/nandiniproothi/nps-lab-notes/main/img/udp-socket.png?token=ALD5GB5GXJRLHBND25M2SG2754YFU)

### Header Files
- sys/types.h: defines socket address in unsigned long
- sys/socket.h: takes pointers to the socket address structure called sockaddr
- sys/netinet.h: defines IPv4 socket address structure called sockaddr_in
- arpa/inet.h: defines the macros used in netinet.h
- sys/stat.h
- netdb.h
- errno.h
- unistd.h 
- fcntl.h
- string.h
- stdlib.h
- stdio.h

> smol tip: in the client/server code that is provided in the lab, please add ```#include <arpa/inet.h>``` to compile it without errors.

### Structures
- sockaddr: address family, 14 bytes protocol-specific address
- sockaddr_in: address family, port, ip address, null
- in_addr: service port
- hostent: host name, aliases, address family, length of ip, internet address
- servent: service name, alias, port number, protocol

### Ports

Just don't go beyond 65535. Avoid reserved ports. Safe to use anything in the range `49151 - 65535`

### Byte Ordering

![](https://raw.githubusercontent.com/nandiniproothi/nps-lab-notes/main/img/byte-ordering.png?token=ALD5GB7MBKRK2S6XC2DM5AS754YII)

### IP Address Functions
- inet_aton
- in_addr_tinet_addr
- inet_ntoa
- connect
- bind
- listen
- accept
- send
- recv
- sendto
- recvfrom
- close
- shutdown

![](https://raw.githubusercontent.com/nandiniproothi/nps-lab-notes/main/img/def.png?token=ALD5GB3UCXOI6M3CHKUBLK2754YHG)

---

### Understanding Socket Programming Code

- Make sure you convert all data to a character/character array before passing it to the server/client side.
- Most functions return -1 in case of failure. Make sure you check for that condition

---

## Lab 2

### File Opening Functions
- Add header file `#include <fcntl.h>`
- access(filename, F_OK) should not be -1 then the file exists
- use fopen(filepointer, operating-mode); operating-modes: read (r), write (w), append (a)
- use fgetc(filepointer) to get characters
- use fprintf(filepointer, character/string) to write to the file
```
if(feop(filepointer)){
  break; //to find eof
}
```

---

## Lab 3

```
int pid
pid = fork();
if(pid>0){
  //parent
}
else{
  //child
}
```

- If fork() succeeds, it returns the PID of the child to the parent process, and returns 0 to the child process. If it fails, it returns -1 to the parent process and no child is created
- getpid() for process ID
- getppid() for paren't process ID

---

## Lab 5

### For printing the IP address
```
struct hostent *host_entry;
int hostname;
char hostname[256];
char *ipbuffer;
hostname = gethostname(hostbuffer, sizeof(hostbuffer));
host_entry = gethostbyname(hostbuffer);
ipbuffer = inet_ntoa(*(structu in_addr*)host_entry->h_addr_list[0]);
char ip[50];
strcpy(ip, ipbuffer);

```
---

## Lab 8

Packet Tracer Modes

- Logical (setup) and Physical (arrangement of buildings and all)
- Simulation (you can control packet transfer and other operations) and Realtime (sends packets on its own, like how it would do irl)

### Cables Used

- Cross-over: joins two networks of the same type (PC-PC, Router-Router)
- Straight-through: it's a type of twisted pair cable that is used to connect a computer to a network hub (router)

### CLI commands to configure a router
```
enable
configure terminal
interface fastethernet 0/0
ip address 192.168.1.1 255.255.255.0
no shutdown

interface fastethernet 1/0
ip address 192.168.2.1 255.255.255.0
no shutdown

exit
```
---
## Lab 9

Topology: How nodes, devices are physically (how it's arranged) and logically (how data flows) arranged in a network. Data efficiency, energy usage, operational and maintenance costs depend on the network topology

### Bus Topology 
![](https://raw.githubusercontent.com/nandiniproothi/nps-lab-notes/main/img/bus-topology.png)

- Has a bus/backbone
- Single network cable runs in a LAN

### Ring Topology

![](https://raw.githubusercontent.com/nandiniproothi/nps-lab-notes/main/img/ring-topology.png)

- Each node keeps forwarding the message till it reaches the destination. Each node has a repeater

### Star Topology

![](https://raw.githubusercontent.com/nandiniproothi/nps-lab-notes/main/img/star-topology.png)

- Add an extra PT-SWITCH-NM-1CFE port to the switch (one fast ethernet)
- Everything goes via the central location (hub)
- Set default gateway for each PC

### Mesh Topology

![](https://raw.githubusercontent.com/nandiniproothi/nps-lab-notes/main/img/mesh-topology.png)

- All nodes are connected to each other
- Failure in one node doesn't lead to a failure in others

---
## Lab 10

### RIP Routing

![](https://raw.githubusercontent.com/nandiniproothi/nps-lab-notes/main/img/rip-routing.png)

- Configure all devices
- Connect the RIP routers using DCE cable

Code for setting up router for RIP
```
enable
configure terminal
interface fastinterface 0/0
ip address 10.0.0.1 255.0.0.0
no shutdown
exit

interface serial 0/0/0
ip address 20.0.0.1 255.0.0.0
clock rate 64000
bandwidth 64
no shutdown
exit

router rip
network 10.0.0.0
network 20.0.0.0
exit

copy running-config startup-config

```
### RIP Commands
`router rip` for enabling RIP protocol
`network x.y.w.z` configure the network i.e. directly connected
`no network x.y.w.z` removes the network from RIP routing process
`version 2` for RIP v2
`version 1` for RIP v1
`no auto-summary` to turn off auto summarisation in v2
`passive-interface serial 0/0/0` RIP updates will not be sent to this port
`no ip split-horizon` turns off split horizon (on by default)
`ip split-horizon` enables split horizon
`timers basic 30 90 180 270 360` update (s), invalid (s), hold-down (s), flush (s), sleep (ms)
`debug ip rip` displays all RIP activity in real time
`show ip rip database` displays contents of RIP database

---

### OSPF Routing

![](https://raw.githubusercontent.com/nandiniproothi/nps-lab-notes/main/img/ospf-routing.png)

- Open Shortest Path First
- Use wildcard mask for OSPF

```
enable
configure terminal
router ospf 1 
network 10.10.10.0 0.0.0.3 area 0
network 10.10.10.4 0.0.0.3 area 0
```

`router ospf 1 //1 is the process ID`
