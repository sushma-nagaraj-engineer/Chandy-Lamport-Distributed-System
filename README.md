# Chandy Lamport
Project Description

Implement a distributed system consisting of n nodes, numbered 0 to n − 1, arranged in a certain topology. The topology and information about other parameters will be provided in a configuration file. All channels in the system are bidirectional, reliable and satisfy the first-in-first-out (FIFO) property. You can implement a channel using a reliable socket connection (with TCP or SCTP).
For each channel, the socket connection should be created at the beginning of the program and should stay intact until the end of the program. All messages between neighboring nodes are exchanged over these connections. All nodes execute the following protocol:
• Initially, each node in the system is either active or passive. At least one node must be active at the beginning of the protocol.
• While a node is active, it sends anywhere from minPerActive to maxPerActive messages, and then turns passive. For each message, it makes a uniformly random selection of one of its neighbors as the destination. Also, if the node stays active after sending a message, then it waits for at least minSendDelay time units before sending the next message.
• Only an active node can send a message.
• A passive node, on receiving a message, becomes active if it has sent fewer than maxNumber messages (summed over all active intervals). Otherwise, it stays passive.
We refer to the protocol described above as the MAP protocol.

1.2 Part 2
Implement the Chandy and Lamport’s protocol for recording a consistent global snapshot.

1.3 Part 3
Design and implement a protocol for bringing all nodes to a halt after node 0 has detected termination of the MAP protocol.
Configuration Format
Your program should run using a configuration file in the following format:
The configuration file will be a plain-text formatted file no more than 100kB in size. Only lines which begin with an unsigned integer are considered to be valid. Lines which are not valid should be ignored. The configuration file will contain 2n + 1 valid lines. The first valid line of the configuration file contains six tokens. The first token is the number of nodes in the system. The
second and third tokens are values of minPerActive, and maxPerActive respectively. The fourth and fifth tokens are values of minSendDelay and snapshotDelay, in milliseconds. snapshotDelay is the amount of time to wait between initiating snapshots in the Chandy-Lamport algorithm. The sixth token is the value of maxNumber. After the first valid line, the next n lines consist of three tokens.
The first token is the node ID. The second token is the host-name of the machine on which the node runs. The third token is the port on which the node listens for incoming connections. After the first n + 1 valid lines, the next n lines consist of a space delimited list of at most n − 1 tokens.
The kth valid line after the first line is a space delimited list of node IDs which are the neighbor of node k. Your parser should be written so as to be robust concerning leading and trailing white space or extra lines at the beginning or end of file, as well as interleaved with valid lines. The # character will denote a comment. On any valid line, any characters after a # character should be
ignored.


