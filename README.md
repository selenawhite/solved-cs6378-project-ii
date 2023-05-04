Download Link: https://assignmentchef.com/product/solved-cs6378-project-ii
<br>
You are required to implement a tree-based quorum system as described below.

You are expected to write your own code without help from any other person or source. Any deviation from this requirement may trigger an investigation of academic misconduct.

The program must run on UTD machines (dc01, dc02, …, dc45).

<h1>1          Requirements</h1>

<ol>

 <li>There is a file (you can choose any name for that file) that each client node can write to. Initially, the file isempty.</li>

 <li>There are seven server nodes in the system, numbered from <em>S</em><sub>1 </sub>to <em>S</em><sub>7</sub>. The servers are logically arranged as a binary tree with <em>S</em><sub>1 </sub>as the root. The children of server <em>S<sub>i </sub></em>are nodes <em>S</em><sub>2<em>i </em></sub>and <em>S</em><sub>2<em>i</em>+1</sub>.</li>

 <li>There are five client nodes in the system, numbered from <em>C</em><sub>1 </sub>to <em>C</em><sub>5</sub>. Each client independently generates its requests to enter the critical section by executing the following sequence of operations until twenty of its requests have been satisfied:

  <ul>

   <li>Waits for a period of time that is uniformly distributed in the range [5, 10] time units before trying to enterthe critical section.</li>

   <li>Sends a REQUEST to a quorum of servers and waits for GRANTS. A quorum of a binary tree of serversis recursively defined as follows:

    <ol>

     <li>Root of the tree + a quorum of left subtree, or</li>

     <li>Root of the tree + a quorum of right subtree, or</li>

    </ol></li>

  </ul></li>

</ol>

<ul>

 <li>A quorum of left subtree + a quorum of right subtree.</li>

</ul>

<ol>

 <li>If the tree is a singleton node, then the tree’s quorum consists of that node.</li>

</ol>

Multiple quorums are possible in this system of seven servers. Each time a client makes a REQUEST, it should randomly select one of the quorums to send the REQUEST to. The goal is to select different quorums over the course of this project.

<ul>

 <li>Once a REQUEST has been granted by all nodes in the selected quorum, the client can enter its criticalsection.</li>

 <li>On entry into the critical section the client does the following:

  <ol>

   <li>Opens the file mentioned above.</li>

   <li>Writes “entering” followed by client number and current physical time in a new line at the end of thefile. iii. Lets 3 units of time elapse, closes the file, and then exits the critical section.</li>

   <li>Sends RELEASE message to all servers in the quorum.</li>

  </ol></li>

 <li>Once a client has successfully exited the critical section twenty times it sends a <em>completion notification </em>to server <em>S</em><sub>0</sub>.</li>

</ul>

<ol start="4">

 <li>The servers act as follows:

  <ul>

   <li>Initially, all servers are in an unlocked state.</li>

   <li>If an unlocked server receives a client’s REQUEST, the server gets locked by that client and sends aGRANT message to the client.</li>

   <li>If a locked server receives a client’s REQUEST, the server adds that client’s REQUEST to its queue orderedby the timestamp of the REQUEST.</li>

   <li>If a server receives a RELEASE message from a client:

    <ol>

     <li>If the server is locked by that client, the server checks is queue. If there is a REQUEST in its queue,the server dequeues the REQUEST at the head of the queue, sends a GRANT to the corresponding client and stays in the locked state. Otherwise (queue is empty), the server becomes unlocked.</li>

    </ol></li>

   <li><em>S</em><sub>0 </sub>brings the entire distributed computation to an end once its has received <em>completion notification </em>from all the clients.</li>

  </ul></li>

 <li>There are reliable socket connections (TCP) between each pair of nodes. The messages pertaining to the mutualexclusion algorithm are sent over these connections.</li>

</ol>

<h1>2          Data Collection</h1>

For your implementation of the mutual exclusion algorithm report the following (either show it on the screen or write it to a file):

<ol>

 <li>The total number of messages sent by each node from the beginning until it sends the <em>completion notification</em>.</li>

 <li>The total number of messages received by each node from the beginning until it sends the <em>completion notification</em>.</li>

 <li>For each node, report the following for each of its attempts to enter the critical section:

  <ul>

   <li>The number of messages exchanged.</li>

   <li>The elapsed time between making a request and being able to enter the critical section (latency).</li>

  </ul></li>

 <li>Rerun your experiment with other values of: (a) time between a client exiting its critical section and issuing itsnext request, and (b) time spent in the critical section. Report what impact do these changes have on performance, specifically latency. Also, report if you come across any deadlock situation.</li>

</ol>





