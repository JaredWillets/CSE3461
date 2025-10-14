# Midterm Review

## Network Structures

### Network Edge

- Consists primarily of the clients and servers
- *Phones, PCs, laptops, servers*

### Access Networks

- Local communication networks
- *Home WiFi networks, mobile networks, university Ethernet networks*

### Network Core

- Global network connecting different access networks
- Include networks owned by differe **internet service providers (ISPs)**
- It is a "network of networks"

Different ISPs are connected through **internet exchange points (IXPs)**

## Switching Techniques

### Packet Switching

Hosts break messages into smaller chunks called packets.
Routers forward each packet independently on appropriate outgoing links, using the full link capacity as it is transferred.
A packet must arrive in its entirety at the router before it can be transmitted to the next link.

### Circuit Switching

Resources are reserved from end to end for a "call" between the source and destination. With these dedicated resources, there is no sharing of the circuit segment, meaning that it will be idle if you used by the "call." This results in guaranteed performance and is very common in traditional telephone networks.

### Which is better?

While a circuit switching technique has guaranteed performance with consistent throughput and less delay, it can be suboptimal with bursty/inconsistent traffic and has a greater complexity for setting up the connection itself. Meanwhile, packet switching is much better for bursty/inconsistent data, resource sharing, and is much simpler because it does not need to establish a "call." However, this technique also comes with many drawbacks: excessive congestion is possible, resulting in greater packet delay and potential packet loss.

## Glossary

 Term | Abbreviation | Definition 
 --- | --- | --- 
Internet Service Provider | ISP | The company or organization that provides and maintains internet access, handling the infrastructure and technical services to maintain internet connections.
| Internet Exchange Point | IXP | A physical locaiton where different **internet service providers** and other network companies connect to exchange traffic directly