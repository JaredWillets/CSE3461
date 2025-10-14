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
- Responsible for *local forwarding* and *global routing*

Different ISPs are connected through **internet exchange points (IXPs)**

## Switching Techniques

### Packet Switching

Hosts break messages into smaller chunks called packets.
Routers forward each packet independently on appropriate outgoing links, using the full link capacity as it is transferred.
A packet must arrive in its entirety at the router before it can be transmitted to the next link.

### Circuit Switching

Resources are reserved from end to end for a "call" between the source and destination. With these dedicated resources, there is no sharing of the circuit segment, meaning that it will be idle if you used by the "call." This results in guaranteed performance and is very common in traditional telephone networks.

### Which is better?

While a circuit switching technique has guaranteed performance with consistent throughput and less delay, it can be suboptimal with bursty/inconsistent traffic and has a greater complexity for setting up the connection itself. Meanwhile, packet switching is much better for bursty/inconsistent data, resource sharing, and is much simpler because it does not need to establish a "call." However, this technique also comes with many drawbacks: excessive congestion is possible, resulting in greater packet delay and potential packet loss. It also requires protocols to have reliable data transfer and congestion control, which adds an additional layer of complexity. This technique is also unable to provide a circuit switching like behavior in cases where it is the optimal technique.

## Throughput

**Throughput** is a rate at which bits are transferred from one device (sender) to another device (receiver).

There are two main ways to evaluate the rate, instantaneous and average.

Instantaneous rate is the rate at a single given point of time.

Average rate is the rate measured over a longer period of time.

## Delay

$$ d_{hop} = d_{queue} + d_{proc} + d_{trans} + d_{prop} $$

The total delay of a hop ($d_{hop}$) is made up of the queueing delay, processing delay, transmission delay, and propagation delay.

| Name | Symbol | Description |
--- | --- | ---
Queueing Delay | $d_{queue}$ | The time waiting at the output link to be transmitted (likely due to packet switching queueing system). Depends heavily on the level of congestion at the router.
Processing Delay | $d_{proc}$ | The time it takes to process the packet, which primarily consists of checking bit errors and determining the output link.
Transmission Delay | $d_{trans}$ | This is the amount of time it takes one packet to have all bits transmitted into the medium. This is represented as $d_{trans} = \frac{L}{R}$, where $L$ is the length of the packet in bits and $R$ is the bandwidth of the link in bits per second.
Propagation Delay | $d_{prop}$ | This is the amount of time the bits are travelling in the medium (such as copper or fiber optic). This delay is often represented as $d_{prop} = \frac{d}{s}$ where $d$ is the length of the physical link in meters and $s$ is the speed of the propagation of the physical link in meters per second.

### Packet Queueing Delay

Recall the definitions of $L$ and $R$ from before. These will be used to determine the traffic intensity, which has a heavy impact on the average queuing delay. The traffic intensity follows the formula $ \text{Traffic Intensity} = \frac{La}{R} $ where the not yet introduced variable, $a$, is the average arrival rate of the packets. When the traffic intensity is near 0, the queueing delay is very small, when it is near 1, it is very large, if it is above 1, then the average delay will be infinite, as the queue will never be completed.

## 5-layer Internet Model

| # | Name | Data Term | Example Protocols | Description
--- | --- | --- | --- | ---
1 | Application | Message | HTTP, SMTP, SSH | This is the point that the applications directly interact with.
2 | Transport | Segment | TCP, UDP | This establishes reliable connection between sender and receiver.
3 | Network | Datagram |  | Uses sender and receiver addresses to find path for packets.
4 | Link | Frame | | Prepare packet to send to next hop
5 | Physical | | | Converts bits to electrical, light, or radio signals to transmit on medium.

### Encapsulation

The process by which various headers are added at different layers of the 5-layer model is called **encapsulation**. When the message is created in the application layer, it is sent to the transport layer, which adds its own headers to the data for all the information needed by the other transport layer and the network layer, similarly the network layer adds a header used by the future network layer and link layer, the link layer adds header information that is used by future link layers. This data is eventually used by the router to ensure that the packet is properly routed to the destination, which extracts the different headers as it goes back up through the layers to the application layer, leaving just the original message.

## Multiplexing / Demultiplexing

### Multiplexing at Sender

Handles data from multiple sockets, adds transport header which will later be used for demultiplexing.

### Demultiplexing at Receiver

Uses header information to deliver received segments to the correct socket.

## User Datagram Protocol (UDP)

UDP is connectionless by nature. This means:

- No handshaking between sender and receiver
- Each UDP segment is handled independent

The segments may be lost or delivered out-of-order to the app.

### The Header

The header is only 32 bits with UDP, and consists of the source port (2 bytes), destination port (2 bytes), length, and checksum. In the segment, this is followed by the actual payload with the requested data.

### Why use UDP?

There is no connection establishment, which means that there is no added delay from the handshake process. Since there is no connection state at the send, or receiver the protocol is much more simple. UDP also uses a very small header (32 bits total) and has no excess congestion control, meaning it can send as fast as desired. This is great for systems like real-time audio or video streaming or DNS requests.

### Checksum

The checksum is present to detect "errors" or "flipped bits" in the transmitted segment. To assemble the checksum, the sender treats segment contents (including the header fields) as a sequene of 16-bit integers. A one's complement sum is then created of all the segment's contents and the checksum value is then placed into the UDP checksum field.

Once the segment is received by the receiver, the checksum is computed on the receiver side. If the checksums match, then it is assumed there is no error (it is possible that there is still an error, but very unlikely). If they do not match, then there is certainly an error.

## Glossary

 Term | Abbreviation | Definition 
 --- | --- | --- 
Internet Service Provider | ISP | The company or organization that provides and maintains internet access, handling the infrastructure and technical services to maintain internet connections.
| Internet Exchange Point | IXP | A physical locaiton where different **internet service providers** and other network companies connect to exchange traffic directly