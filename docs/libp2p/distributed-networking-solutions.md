---
description: The Problems & Modular Solution of Libp2p
---

## Circuit Relays

In some cases, peers might no be publicly reacheable. For example, consider that peer `A` wants to connect to `B`, but peer `B` is behind a firewall that does not allow incoming connections.

To solve this issue, libp2p provides a protocol called _circuit-p2p_. When a peer is not recheable by other peers, another machine listens for connections on its behalf. Then, those connections are forwarded to the non-reacheable peer.

Consider the following diagram

// image

1. `A` is not recheable, so it asks `C` to listen for connections on its behalf.
2. `B` establishes a connection to `C`.
3. `C` forwards messages from `B` to `A`.

Note that `A` starts the connection to `C` because `A` is not publicly accessible.

### Multiaddresses

When sending messages over a circuit relay, we must know how to reach the _relay machine_ (i.e. the machine that is acting as bridge). In the previous example, `B` has to find out how to reach `C`.

Multiaddresses identify circuit relays by using the IDs of the peers involved. The following is a sample circuit relay multiaddress.

```
/ip4/127.0.0.1/tcp/2330/p2p/PEER_ID_OF_C/p2p-circuit/p2p/PEER_ID_OF_A
```

You can read the previous address like: "Make a connection to `127.0.0.1` at TCP port `2330`, which is the address of the peer `C`. Then, perform a circuit relay to peer `A`".

Currently, there are two different version of the circuit relay protocol in libp2p: .

## Publish/Subscribe

A PubSub (Publish/Subscribe) system allows peers to only receive messages of a specific type. A _publisher_ sends messages of a specific type to _subscribers_ of that type. For example, consider a chat application with a chat group called `music`. Users interested subscribe to the group; when someone sends a message to the group, only those subscribed receive the message.

In libp2p, peers subscribe and send messages to _topics_. The concept is pretty similar to messaging systems (e.g. Kafka), but libp2p allows this behaviour in a decentralized way. The main implementation of the protocol are: FloodSub and GossipSub.

In FlooSub, the first implementation of the pub/sub protocol, messages are delivered to all the nodes of a peer. For example, consider the following diagram.

// image

1. `Peer 1` is connected to `Peer 2` and `Peer 3`; `Peer 2` and `Peer 3` are connected to `Peer 4`.
2. `Peer 1` publishes a message, which is sent to `Peer 2` and `Peer 3`.
3. Both `Peer 2` and `Peer 3` forward the message to `Peer 4`.

The main problem of FloodSub is that it duplicates message delivery, thus using a lot of bandwidth. In the previous example, `Peer 4` receives the message two times.

## The Problems
In the course of creating and researching distributed apps, there were a number of problems encoutered that the libp2p project addressed.

<!-- Add list of problems & summary here -->

#### Solving Distributed Networking Problems with Libp2p | IPFS Camp

<!-- Summary? Who does it feature?  -->

{% embed url="https://www.youtube.com/watch?v=oIMZP7sfFtM" %}
