###Overview

A simple p2p chat using GOLANG over UDP

###How Does It Work

I am using `UDP hole punching` for establishing connection between peers.

#### UDP Hole Punching

The easiest way to establish connection between peers over NAT.
The process:
1. p1 --> p2 (echo "puching a hole" | nc -u -p 5001 <p2.ip> 5002) puch a hole in firewall
2. p2 --> p1 (echo "puching a hole" | nc -u -p 5001 <p1.ip> 5002) puch a hole in firewall
3. p1 (nc -u -l 5001)
4. p2 (nc -u -l 5001)
5. p1 <--> p2 (echo "data" | nc -u -p 5001 <p1/2.ip> 5002)

##### Description

In steps (1-2) the peer is "punching a hole" in the firewall by sending a `UDP` packet to the other peer from a specified source port to the peer destination port and by that he is telling the router that he is waitin for a comeback packet from the other peer with the same ip and port.

In steps (3-4) the peer is listening to income packets.

In step (5) the peers can send packets to each other while the connection is still alive.
* The connection may die after 20-40 seconds, and this is why there are keepalive packets.
