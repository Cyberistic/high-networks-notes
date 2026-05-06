These are the questions which came in the midterm *as I remember them*, they are _NOT_ verbatim. 

All questions asked in the midterm were included in the previous notes except for *F) SDN* as I did not know it was included as a topic.

<div style="page-break-after: always;"></div>

## A) Slotted aloha for n = 4, 

Question: 
1. Find the optimal probability

2. What is the probability for user 4 to enter slot 5?

This question is answered in [[12 - Slotted ALOHA Performance]], except we do not take the limit as n approaches infinity and instead sub n = 4.

#### Solution

##### Part 1
For **Slotted ALOHA**, if there are $n$ users and each transmits with probability $p$ in a slot:

- success probability for **one specific user**:

$$
P_{\text{success,user}} = p(1-p)^{n-1}
$$

- success probability for the **system** (exactly one user succeeds in the slot):

$$
P_s = np(1-p)^{n-1}
$$

For this question, $n=4$, so:

$$
P_s = 4p(1-p)^3
$$

To find the optimal probability, differentiate and set to zero:

$$
\frac{d}{dp}\left(4p(1-p)^3\right)=0
$$

This gives the standard Slotted ALOHA result:

$$
p^* = \frac{1}{n} = \frac{1}{4}
$$

So the **optimal transmission probability** is:

$$
\boxed{p^* = \frac{1}{4}}
$$

##### Part 2
Since every slot is identical in Slotted ALOHA, the probability is just the one-slot success probability for user 4:

$$
P(\text{A succeeds in slot 5}) = p(1-p)^3
$$

Using the optimal probability $p=\frac{1}{4}$:

$$
P(\text{A succeeds in slot 5}) = \frac{1}{4}\left(\frac{3}{4}\right)^3 = \frac{27}{256} \approx 0.1055
$$




<div style="page-break-after: always;"></div>

## B) Memoryless derivation

Question: Given you're in a poisson distributed train station, if you want to know how long you have to wait until the train arrives, does it matter if you know you've been waiting for 15 minutes?

This is basically asking you to prove the _Memoryless_ property of poisson. 

The full solution is at [[2 - Review#Derivation of the Memoryless Property]]



## C) Erlang B recursion derivation 

Exactly the same as [[8 - Erlang Recursive Form]]



## D) CDMA 
Question: given 4 nodes with their codes of length n = 8
1. Prove node A and B are ortho

2. Given final code, decode and specify what bit each node sent, or if a node didn't transmit

Different numbers, otherwise exactly the same as [[11 - CDMA Derivation]]



<div style="page-break-after: always;"></div>

## E) Fading
1. Definition of small vs large scale fading
2. What is each affected by?
3. Disadvantages of each?
4. Give one example of a protocol for each
5. An application of one of the protocols mentioned above

### Solution

Most are pulled from [[3 - Physical Layer#Propagation Mechanisms in Wireless Channels]], this question is open-ended and accepts different answers

#### 1. Definition of small vs large-scale fading

**Large-scale fading** describes the gradual change in the average received signal strength over **large distances**. As the receiver moves farther from the base station, the signal generally becomes weaker because of path loss.

It is also affected by the surrounding environment, such as buildings, hills, trees, and terrain elevation, which can block or weaken the signal.

In short, large-scale fading is the long-range variation in signal power caused by **distance** and **shadowing from large objects**.

**Small-scale fading** refers to rapid, short-distance fluctuations in signal strength caused by multipath interference, where several reflected or delayed versions of the signal add together constructively or destructively, causing multiple signals to occur.

#### 2. What is each affected by?

**Large-scale fading** is affected by:

- distance from the base station / transmitter
- path loss
- shadowing from large objects
- buildings, hills, trees, terrain elevation

**Small-scale fading** is affected by:

- multipath interference
- reflection
- diffraction
- scattering
- constructive / destructive summation of delayed copies

<div style="page-break-after: always;"></div>

#### 3. Disadvantages of each

**Large-scale fading** disadvantage:

- some areas have much weaker reception than others, even in the same cell
- signal strength drops gradually with distance

**Small-scale fading** disadvantage:

- rapid signal fluctuations
- can cause severe distortion and fading
- can lead to **time dispersion** and **ISI** if multipath copies overlap later symbols
- in a **frequency-selective fading** channel, different frequency components are affected differently, so distortion is more severe
- in **frequency-flat fading**, the whole signal sees nearly the same channel gain, so it mostly becomes weaker/stronger without as much waveform distortion

#### 4. Give one example of a protocol / technique for each


uhhh idk tbh very ambiguous question, even Mr. Jippity doesn't know, so my guess is this

For **small-scale fading**:
- **FDM*

For **large-scale fading**:
- **tower handoff**


#### 5. An application of one of the protocols mentioned above

FDM -> **OFDM** which ADSL2 uses




### Mr. Jippity's answer:

- **Large-scale fading**: gradual signal variation over large distances due to path loss and shadowing
- **Small-scale fading**: rapid fluctuations over short distances due to multipath
- **Small-scale fading technique**: OFDM / multicarrier transmission
- **Application**: ADSL2, 802.11, or 4G



<div style="page-break-after: always;"></div>

## F) SDN:

1. What is SDN?
2. Architecture of SDN
3. 3 benefits of SDN
4. How to simulate SDN

### Solution

#### 1. What is SDN?

**SDN** stands for **Software-Defined Networking**.
it is a networking approach where control is done by software in a central controller instead of being embedded separately inside every switch/router.

The main idea is to separate the **control plane** from the **data plane**.
- **control plane** = decides where traffic should go
- **data plane** = actually forwards packets

#### 2. Architecture of SDN

In traditional networking, both control plane and data plane are usually built into each router or switch, whereas in SDN:
- the **SDN controller** acts as the control plane
- switches mainly act as forwarding devices in the data plane
- the controller communicates with switches using control messages such as **OpenFlow**


#### 3. 3 benefits of SDN

You can mention any 3 of these:

- **centralized control**
- **programmability**
- **improved traffic management**:
- **scalability**
- **cost reduction**

#### 4. How to simulate SDN

From the SDN paper note:

- **Mininet** = network emulator
- **Ryu** or **ONOS** = SDN controllers

simulate SDN using **Mininet** with a controller such as **Ryu** or **ONOS**


<div style="page-break-after: always;"></div>

## G) TCP/IP

1. All layers Definition
2. Protocol example for each layer
3. Keyword hint for each layer
4. One of them has sublayer, which?

### Solution

Pulled from [[0 & 1 - Intro]].

#### 1. All layers definition

##### Physical layer

- implements a digital communication link that delivers bits

##### Data link layer

- implements a packet delivery service between nodes that are attached to the same physical link

##### Network layer

- guides the packets from their source to their destination, along a path that may comprise a number of links

##### Transport layer

- supervises the end-to-end transmission of packets
- may arrange for retransmission of erroneous packets

##### Session layer

- uses the transport layer services to set up and supervise connections between end systems

##### Presentation layer

- takes care of data compression, security, and format conversions so that nodes that use different representations of information can communicate efficiently and securely

##### Application layer

- implements commonly used communication services including file transfer, directory services, virtual terminal


<div style="page-break-after: always;"></div>

#### 2. Protocol example for each layer


- **Physical**: **OFDM**, Ethernet physical signaling, fiber / radio transmission
- **Data link**: **Ethernet**, Wi-Fi MAC, bridges
- **Network**: **IP**, routing, routers
- **Transport**: **TCP**, **UDP**
- **Session**: **RPC**, session setup / dialog control
- **Presentation**: **TLS**, compression, encryption, format translation
- **Application**: **HTTP**, **FTP**, directory service, virtual terminal

#### 3. Keyword hint for each layer

- **Physical** -> bits / signal / modulation
- **Data link** -> frames / node-to-node delivery
- **Network** -> packets / routing / addressing
- **Transport** -> end-to-end / reliability / retransmission
- **Session** -> connection setup / supervision
- **Presentation** -> encryption / compression / format conversion
- **Application** -> user services / file transfer / web 

#### 4. One of them has sublayer, which?


- **Application layer** in TCP/IP includes what OSI splits into:
  - **Application**
  - **Presentation**
  - **Session**



---


> [!Note] Sorry if I missed some parts or messed up the wording of the questions, this is all from memory and I tried my best :(
