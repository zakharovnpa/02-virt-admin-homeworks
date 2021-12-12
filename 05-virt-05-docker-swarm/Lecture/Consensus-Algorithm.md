In Search of an Understandable Consensus Algorithm
(Extended Version)
Diego Ongaro and John Ousterhout
Stanford University

### Abstract
Raft is a consensus algorithm for managing a replicated
log. It produces a result equivalent to (multi-)Paxos, and
it is as efficient as Paxos, but its structure is different
from Paxos; this makes Raft more understandable than
Paxos and also provides a better foundation for build-
ing practical systems. In order to enhance understandabil-
ity, Raft separates the key elements of consensus, such as
leader election, log replication, and safety, and it enforces
a stronger degree of coherency to reduce the number of
states that must be considered. Results from a user study
demonstrate that Raft is easier for students to learn than
Paxos. Raft also includes a new mechanism for changing
the cluster membership, which uses overlapping majori-
ties to guarantee safety.


### 1 Introduction
Consensus algorithms allow a collection of machines
to work as a coherent group that can survive the fail-
ures of some of its members. Because of this, they play a
key role in building reliable large-scale software systems.
Paxos [15, 16] has dominated the discussion of consen-
sus algorithms over the last decade: most implementations
of consensus are based on Paxos or influenced by it, and
Paxos has become the primary vehicle used to teach stu-
dents about consensus.
Unfortunately, Paxos is quite difficult to understand, in
spite of numerous attempts to make it more approachable.
Furthermore, its architecture requires complex changes
to support practical systems. As a result, both system
builders and students struggle with Paxos.
After struggling with Paxos ourselves, we set out to
find a new consensus algorithm that could provide a bet-
ter foundation for system building and education. Our ap-
proach was unusual in that our primary goal was under-
standability: could we define a consensus algorithm for
practical systems and describe it in a way that is signifi-
cantly easier to learn than Paxos? Furthermore, we wanted
the algorithm to facilitate the development of intuitions
that are essential for system builders. It was important not
just for the algorithm to work, but for it to be obvious why
it works.
The result of this work is a consensus algorithm called
Raft. In designing Raft we applied specific techniques to
improve understandability, including decomposition (Raft
separates leader election, log replication, and safety) and
state space reduction (relative to Paxos, Raft reduces the
degree of nondeterminism and the ways servers can be in-
consistent with each other). A user study with 43 students
at two universities shows that Raft is significantly easier
to understand than Paxos: after learning both algorithms,
33 of these students were able to answer questions about
Raft better than questions about Paxos.
Raft is similar in many ways to existing consensus al-
gorithms (most notably, Oki and Liskov’s Viewstamped
Replication [29, 22]), but it has several novel features:
• Strong leader: Raft uses a stronger form of leader-
ship than other consensus algorithms. For example,
log entries only flow from the leader to other servers.
This simplifies the management of the replicated log
and makes Raft easier to understand.
• Leader election: Raft uses randomized timers to
elect leaders. This adds only a small amount of
mechanism to the heartbeats already required for any
consensus algorithm, while resolving conflicts sim-
ply and rapidly.
• Membership changes: Raft’s mechanism for
changing the set of servers in the cluster uses a new
joint consensus approach where the majorities of
two different configurations overlap during transi-
tions. This allows the cluster to continue operating
normally during configuration changes.
We believe that Raft is superior to Paxos and other con-
sensus algorithms, both for educational purposes and as a
foundation for implementation. It is simpler and more un-
derstandable than other algorithms; it is described com-
pletely enough to meet the needs of a practical system;
it has several open-source implementations and is used
by several companies; its safety properties have been for-
mally specified and proven; and its efficiency is compara-
ble to other algorithms.
The remainder of the paper introduces the replicated
state machine problem (Section 2), discusses the strengths
and weaknesses of Paxos (Section 3), describes our gen-
eral approach to understandability (Section 4), presents
the Raft consensus algorithm (Sections 5–8), evaluates
Raft (Section 9), and discusses related work (Section 10).

### 2 Replicated state machines
Consensus algorithms typically arise in the context of
replicated state machines [37]. In this approach, state ma-
chines on a collection of servers compute identical copies
of the same state and can continue operating even if some
of the servers are down. Replicated state machines are
used to solve a variety of fault tolerance problems in dis-
tributed systems. For example, large-scale systems that
have a single cluster leader, such as GFS [8], HDFS [38],
and RAMCloud [33], typically use a separate replicated
state machine to manage leader election and store config-
uration information that must survive leader crashes. Ex-
amples of replicated state machines include Chubby [2]
and ZooKeeper [11].
- Figure 1: Replicated state machine architecture. The con-
sensus algorithm manages a replicated log containing state
machine commands from clients. The state machines process
identical sequences of commands from the logs, so they pro-
duce the same outputs.

Replicated state machines are typically implemented
using a replicated log, as shown in Figure 1. Each server
stores a log containing a series of commands, which its
state machine executes in order. Each log contains the
same commands in the same order, so each state ma-
chine processes the same sequence of commands. Since
the state machines are deterministic, each computes the
same state and the same sequence of outputs.
Keeping the replicated log consistent is the job of the
consensus algorithm. The consensus module on a server
receives commands from clients and adds them to its log.
It communicates with the consensus modules on other
servers to ensure that every log eventually contains the
same requests in the same order, even if some servers fail.
Once commands are properly replicated, each server’s
state machine processes them in log order, and the out-
puts are returned to clients. As a result, the servers appear
to form a single, highly reliable state machine.
Consensus algorithms for practical systems typically
have the following properties:
• They ensure safety (never returning an incorrect re-
sult) under all non-Byzantine conditions, including
network delays, partitions, and packet loss, duplica-
tion, and reordering.
• They are fully functional (available) as long as any
majority of the servers are operational and can com-
municate with each other and with clients. Thus, a
typical cluster of five servers can tolerate the failure
of any two servers. Servers are assumed to fail by
stopping; they may later recover from state on stable
storage and rejoin the cluster.
• They do not depend on timing to ensure the consisency 
of the logs: faulty clocks and extreme message
delays can, at worst, cause availability problems.
• In the common case, a command can complete as
soon as a majority of the cluster has responded to a
single round of remote procedure calls; a minority of
slow servers need not impact overall system perfor-
mance.
