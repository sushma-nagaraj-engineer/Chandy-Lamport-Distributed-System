# Chandy Lamport
1 Project Description
This project consists of three parts.
1.1 Part 1
Implement a distributed system consisting of n nodes, numbered 0 to n − 1, arranged in a certain topology. The topology and information about other parameters will be provided in a configuration file. All channels in the system are bidirectional, reliable and satisfy the first-in-first-out (FIFO) property. You can implement a channel using a reliable socket connection (with TCP or SCTP).
For each channel, the socket connection should be created at the beginning of the program and should stay intact until the end of the program. All messages between neighboring nodes are exchanged over these connections. All nodes execute the following protocol:
• Initially, each node in the system is either active or passive. At least one node must be active at the beginning of the protocol.
• While a node is active, it sends anywhere from minPerActive to maxPerActive messages, and then turns passive. For each message, it makes a uniformly random selection of one of its neighbors as the destination. Also, if the node stays active after sending a message, then it waits for at least minSendDelay time units before sending the next message.
• Only an active node can send a message.
• A passive node, on receiving a message, becomes active if it has sent fewer than maxNumber messages (summed over all active intervals). Otherwise, it stays passive.
We refer to the protocol described above as the MAP protocol.
1.2 Part 2
Implement the Chandy and Lamport’s protocol for recording a consistent global snapshot. Assume that the snapshot protocol is always initiated by node 0 and all channels in the topology are bidirectional. Use the snapshot protocol to detect the termination of the MAP
protocol described in Part 1. The MAP protocol terminates when all nodes are passive and all channels are empty. To detect termination of the MAP protocol, augment the Chandy and Lamport’s snapshot protocol to collect the information recorded at each node at node 0 using a converge-cast operation over a spanning tree. The tree can be built once in the beginning or on-the-fly for an instance using MARKER messages. Note that, in this project, the messages exchanged by the MAP protocol are application messages and the messages exchanged by the snapshot protocol are control messages. The rules of the MAP protocol (described in Part 1) only apply to application messages. They do not apply to control messages.

Testing Correctness of the Snapshot Protocol Implementation:
To test that your implementation of the Chandy and Lamport’s snapshot protocol is correct, implement Fidge/Mattern’s vector clock protocol described in the class. The vector clock of a node is part of the local state of the node and its value is also recorded whenever a node records its local state. Node 0, on receiving the information recorded by all the nodes, uses these vector timestamps
to verify that the snapshot is indeed consistent. Note that only application messages will carry vector timestamps.
1.3 Part 3
Design and implement a protocol for bringing all nodes to a halt after node 0 has detected termination of the MAP protocol.
Configuration Format
Your program should run using a configuration file in the following format:
The configuration file will be a plain-text formatted file no more than 100kB in size. Only lines which begin with an unsigned integer are considered to be valid. Lines which are not valid should be ignored. The configuration file will contain 2n + 1 valid lines. The first valid line of the configuration file contains six tokens. The first token is the number of nodes in the system. The
second and third tokens are values of minPerActive, and maxPerActive respectively. The fourth and fifth tokens are values of minSendDelay and snapshotDelay, in milliseconds. snapshotDelay is the amount of time to wait between initiating snapshots in the Chandy-Lamport algorithm. The sixth token is the value of maxNumber. After the first valid line, the next n lines consist of three tokens.
The first token is the node ID. The second token is the host-name of the machine on which the node runs. The third token is the port on which the node listens for incoming connections. After the first n + 1 valid lines, the next n lines consist of a space delimited list of at most n − 1 tokens.
The kth valid line after the first line is a space delimited list of node IDs which are the neighbor of node k. Your parser should be written so as to be robust concerning leading and trailing white space or extra lines at the beginning or end of file, as well as interleaved with valid lines. The # character will denote a comment. On any valid line, any characters after a # character should be
ignored.
Listing 1: Example configuration file
# s i x g l o b a l parameter s ( s e e above )
5 6 10 100 2000 15
0 dc02 1234 # nodeID hostName l i s t e nPo r t
1 dc03 1233
2 dc04 1233
3 dc05 1232
4 dc06 1233
1 4 # spac e de l imi t ed l i s t o f ne ighbor s f o r node 0
2 3 4 # spac e de l imi t ed l i s t o f ne ighbor s f o r node 1
0 1 3 # . . . node 2
0 4 # . . . node 3
1 3 # . . . node 4
4 Output Format
If the configuration file is named <config_name>.txt and is configured to use n nodes, then your
program should output n output files, named in according to the following format:
<config_name>-<node_id>.out, where node_id ∈ {0, ..., n − 1}.
The output file for process j should be named <config_name>-j.out and should contain the
following: If your program took m snapshots, then each output file should contain m lines. The
ith line should contain the vector timestamp of the ith snapshot as seen by process j. Each line of
the output file should contain n space delimited tokens, each of which should be a non-negative
integer. In each line, the timestamps must appear in increasing order of process id. That is, the kth
number in the ith line should be the timestamp value for process k. An example file is described
below.

Listing 2: Example output file for 7 nodes
0 4 3 6 0 2 3
3 7 6 7 2 4 4
6 9 11 10 5 7 5
8 12 14 23 8 10 7
In this example, the first snapshot has vector clock value h0, 4, 3, 6, 0, 2, 3i; the value of node 0’s
clock is 0, and the value of mode 3’s clock is 6.

