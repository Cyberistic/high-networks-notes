

(Also look at the topic in the 'Physical Layer' notes)

## Packet Switching

In packet-based networks, data messages are broken down into small data packets.

- **Routing:** Packets are sent from the source computer and travel across the network seeking the most efficient route as circuits become available. This route is not necessarily the shortest path. Each packet belonging to the same message may take a completely different route to the destination.
    
- **Headers:** Each packet includes a "header address" indicating its final destination. The header also contains sequence information so the packets can be reassembled in the correct order at the destination computer.
    
- **Reliability:** One of the packets contains details regarding the total number of packets expected, allowing the recipient to detect if any are missing. If a packet fails to arrive, the receiving computer sends a message back to the sender requesting the missing packet be resent.
    
- **Protocols:** Packet switching utilizes specific protocols, such as UDP (User Datagram Protocol), to format and handle the data.
    

### Advantages vs. Disadvantages of Packet Switching

|**Advantages**|**Disadvantages**|
|---|---|
|Offers built-in security features.|Delays can occur under heavy network use.|
|Uses available bandwidth to its full potential.|Data packets can get lost or corrupted in transit.|
|Allows devices of different speeds to communicate with each other.|Requires specific protocols to ensure reliable transfer.|
|Resilient to line failures because signals can simply be redirected.|Not ideal for certain data streams (e.g., real-time video can lose frames if packets arrive out of sequence).|
|High availability; there is no waiting for a direct connection to free up.||
|During disasters when public telephone networks fail, emails and texts can often still be transmitted via packet switching.||


<div style="page-break-after: always;"></div>

## Circuit Switching

Circuit switching was originally designed in the 1800's to transmit telephone calls over a dedicated channel.

- **Dedicated Channel:** The established channel remains open and in use for the entire duration of the call, preventing any other data or calls from using it. During a call, no other network traffic can utilize the engaged switches.
    
- **Data Transfer:** The entire telephone message is sent as a continuous stream and is not broken up. The message arrives in the exact order it was originally transmitted. The network resources remain completely dedicated to the circuit throughout the transfer, meaning the entire message follows a single, unbroken path.
    
- **Phases:** The process involves three distinct phases: Establish, Transfer, and Disconnect.
    
- **Modern Use:** While electronic signals pass through multiple switches to establish a connection, circuit switching can be implemented as either analog or digital. Analysts predict a gradual shift away from these networks due to the expansion of internet voice and video , though circuit switching remains excellent for data requiring a constant end-to-end link, such as real-time video.
    

### Advantages vs. Disadvantages of Circuit Switching

|**Advantages**|**Disadvantages**|
|---|---|
|The circuit is entirely dedicated to the call, meaning no interference or sharing occurs.|Highly inefficient; equipment may sit unused for significant portions of the call.|
|Guarantees full bandwidth for the entire duration of the connection.|If no data is being sent, the dedicated line still remains open and unavailable to others.|
|Provides a guaranteed Quality of Service (QoS).|Takes a relatively long time to establish the initial circuit.|
||The network may become unstable or unavailable during crises or disasters.|
||Originally developed primarily for voice traffic, making it less optimal for bursty data traffic.|


<div style="page-break-after: always;"></div>

## Traffic Management and Overload Control

![[6 - Circuit & Packet Switching.png | 300]]

Telephone network traffic fluctuates constantly as calls are initiated and terminated.

- **Human Activity:** Traffic patterns are heavily driven by human activity. Examples include mid-morning and mid-afternoon surges at the office , evening usage at home , and seasonal changes like summer vacations.
    
- **Surges:** "Outlier days" (like Mother’s Day or Christmas) are exceptionally busy. Disasters and other major events also cause sudden, significant traffic surges. Proper traffic management and overload control are necessary to handle this.
    
- **Cost Efficiency:** Providing enough resources so that call requests are _always_ met is prohibitively expensive. Instead, it is more cost-effective to provision resources so that requests are met _most_ of the time.
    
- **Trunk Concentration:** Switches concentrate traffic from many lines onto a fewer number of shared trunks. Because of this consolidation, blocking of connection requests will occasionally occur when all trunks are busy (call is dropped). Traffic engineering provisions these resources to meet specific blocking performance targets.
    


<div style="page-break-after: always;"></div>

## Modeling Traffic Processes

Effective traffic engineering requires analyzing the statistics of $N(t)$, which represents the number of active calls in the system at a given time.

### Variables and The Poisson Model

- **Call requests arrival rate ($\lambda$):** The rate of incoming calls, measured in requests per second.
    
- **Poisson Arrival Process:** The resulting random process is modeled mathematically as a Poisson arrival process. The probability of $k$ arrivals occurring in time $T$ is defined as:
    
    $$P(k \text{ arrivals in time } T) = \frac{(\lambda T)^k e^{-\lambda T}}{k!}$$
    
- **Holding time:** The duration a user maintains a connection (how long the call lasts). It is represented by a random variable $X$ with a mean of $E(X)$. When $X$ is exponential, the service rate is defined as $\mu = 1/E(X)$.
    
- **Offered load ($\rho$):** How much traffic users are trying to place on the system on average. You can think of it as the average number of channels that would be busy if there were enough channels available for everyone. It is calculated by multiplying how often calls arrive by how long they last on average:

    $$\rho = \lambda \cdot E(X) = \frac{\lambda}{\mu}$$

    Example: if calls arrive at a rate of `2 calls/sec` and each call lasts `3 sec` on average, then the offered load is `2 x 3 = 6` Erlangs. Intuitively, the traffic is demanding about `6` channels' worth of service on average.
    

<div style="page-break-after: always;"></div>

### Blocking Probability and Utilization

If $c$ represents the total number of trunks or channels available, blocking occurs when all channels are currently busy (i.e., $N(t)=c$).

- **Erlang B Formula:** If call requests follow a Poisson distribution, the blocking probability ($P_b$) is calculated using the Erlang B formula:
    
    $$P_b = \frac{\frac{\rho^c}{c!}}{\sum_{j=0}^{c} \frac{\rho^j}{j!}}$$
    
- **Recursive Erlang B Formula:** The formula can also be evaluated recursively:
    
    $$P_b(c,\rho) = \frac{\rho P_b(c-1,\rho)}{c + \rho P_b(c-1,\rho)}$$
    
- **Utilization:** The fraction of the total trunk capacity that is actually being used on average. Since some calls are blocked, the carried traffic is not the full offered load $\rho$, but only $(1-P_b)\rho$. Dividing by the number of trunks $c$ gives the average usage per trunk:
     
    $$\text{Utilization} = \lambda(1 - P_b) \frac{E(X)}{c} = \frac{(1 - P_b) \rho}{c}$$

    So utilization tells us how busy each trunk is on average.

    Example intuition:

    - if utilization = `1`, the trunks are busy all the time
    - if utilization = `0.5`, each trunk is busy about half the time on average
    - if utilization is very high, the system is efficient but blocking becomes more likely
    - if utilization is very low, blocking is rare but many trunks sit idle

<div style="page-break-after: always;"></div>

![[trunks and erlang.png | 500]]

- **Example Calculation / Trunk Sizing:** Suppose we want a blocking probability target of only `1%`.

    - if the offered load is $\rho = 5$ Erlangs, we need about `11` trunks
    - if the offered load is $\rho = 10$ Erlangs, we need about `18` trunks

    The number of trunks needed grows with traffic load, but not in a simple one-for-one way. We add extra trunks beyond the offered load itself so that the chance of all trunks being busy stays below the desired blocking target.

> [!Note] Consider a question where he gives you the graph, the desired percentage, and how many Erlands, and asks you how many trunks we need.


<div style="page-break-after: always;"></div>

## Erlang B vs Erlang C

- **Erlang B** is used when blocked calls are **cleared/lost** immediately.
  - If all trunks are busy, the new call is rejected.
  - Typical use: classic telephone trunk sizing.

- **Erlang C** is used when blocked calls are **delayed and wait in a queue**.
  - If all servers are busy, the new request waits instead of being dropped.
  - Typical use: call centers or service systems with waiting lines.

So the key difference is:

- **Erlang B** -> no waiting room, blocked traffic is lost
- **Erlang C** -> waiting room exists, blocked traffic waits

> [!Note]
> Use **Erlang B** for circuit-switched trunk blocking problems, and **Erlang C** for queueing/wait-time problems.
