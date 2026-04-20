# LEAKED MIDTERM QUESTIONS?!?!?!!?!?


This note will be divided into 3 categories:
1. Confirmed Questions: for questions dr. awad said *will* come. Examples of what they might look like.
2. Most-likely Questions: given how many classes and lecture time spent, they are most likely to come
3. Multiple-choice Questions: a curated multiple-choice/true-false test-bank of questions from the notes






<div style="page-break-after: always;"></div>

# Confirmed Questions

## 1. General knowledge / networking questions
A curated list will be added to the end of this note

## 2. Performance Evaluation of Aloha + variations of Aloha

Refer to [[12 - Slotted ALOHA Performance]], the derivation, calculating the performance, what happens if he changes one of the variables, etc..




## 3. Pseudocode
Write down the protocol in pseudocode.

### Example 1: Slotted Aloha

```js
function SlottedAloha(lambda, n, p):
    poisson_prob = poisson_dist(lambda, n)

    wait_until_slot_boundary()

    if has_frame_to_send() == false:
        return "idle slot", poisson_prob

    if random() > poisson_prob:
        return "do not transmit in this slot", poisson_prob

    transmit()

    if collision_detected() == true:
        if random() < p:
            schedule_retransmission_at_future_slot()
            return "collision -> retry later", poisson_prob
        else:
            return "collision -> wait", poisson_prob

    return "success", poisson_prob
```

<div style="page-break-after: always;"></div>

### Example 2: Pure Aloha

```js
function PureAloha(lambda, n):
    poisson_prob = poisson_dist(lambda, n)

    if has_frame_to_send() == false:
        return "no transmission", poisson_prob

    if random() > poisson_prob:
        return "do not transmit now", poisson_prob

    transmit_immediately()

    if collision_detected() == true:
        backoff_time = random_backoff()
        wait(backoff_time)
        return "collision -> retry later", poisson_prob

    return "success", poisson_prob
```


### Example 3: Token Passing

```js
function TokenPassing(token = false):
    wait_for_token()

    if has_frame_to_send() == true:
        transmit_for_allowed_time()

    pass_token_to_next_node()

    return "token processed"
```



## 4. Resource-allocation Problem to Math Form
Given a paragraph about networking, need to define variables and convert it to a mathematical equation with constraints.
Refer to the examples in the papers in [[100 - awad's first paper]] and [[101 - awad's second paper]], though they are a bit complex. 

- first identify the **thing to optimize**: throughput, power, fairness, delay, etc.
- then identify the **limits**: power, bandwidth, one-user-per-subcarrier, minimum QoS, flow conservation, etc.
- finally define clean symbols for each quantity before writing equations

Common constraint patterns:

- one resource to one user: $\sum x \le 1$
- total power budget: $\sum p \le P_{max}$
- minimum user requirement: $r_k \ge R_k^{min}$



### Example 1: 

**Paragraph version:**

An OFDMA base station serves $K$ users using $N$ subcarriers. Each subcarrier can be assigned to only one user at a time. The base station wants to maximize total throughput, but the total transmit power must stay below $P_{max}$.

**Step 1: Define variables**

- $x_{k,n} \in \{0,1\}$: equals `1` if subcarrier $n$ is assigned to user $k$, otherwise `0`
- $p_{k,n}$: power allocated to user $k$ on subcarrier $n$
- $r_{k,n}$: achievable rate of user $k$ on subcarrier $n$

**Step 2: Objective**

Maximize total throughput:

$$
\max \sum_{k=1}^{K} \sum_{n=1}^{N} x_{k,n} r_{k,n}
$$

**Step 3: Constraints**

Each subcarrier goes to at most one user:

$$
\sum_{k=1}^{K} x_{k,n} \le 1, \quad \forall n
$$

Total power must not exceed the maximum:

$$
\sum_{k=1}^{K} \sum_{n=1}^{N} p_{k,n} \le P_{max}
$$

Binary assignment variable:

$$
x_{k,n} \in \{0,1\}
$$

<div style="page-break-after: always;"></div>


### Example 2: 

**Paragraph version:**

The base station wants every user to get at least a minimum required rate, while still keeping total power below a maximum.

**Step 1: Define variables**

- $r_k$: total rate given to user $k$
- $R_k^{min}$: minimum required rate for user $k$
- $p_{k,n}$: power allocated on subcarrier $n$ for user $k$

**Step 2: Objective**

Minimize total power:

$$
\min \sum_{k=1}^{K} \sum_{n=1}^{N} p_{k,n}
$$

**Step 3: Constraints**

Each user must get its required rate:

$$
r_k \ge R_k^{min}, \quad \forall k
$$

Total power limit:

$$
\sum_{k=1}^{K} \sum_{n=1}^{N} p_{k,n} \le P_{max}
$$

<div style="page-break-after: always;"></div>

# Most-likely Questions


## 1. Shannon/Nyquist & Taylor Series & Probability

For probability, check [[2 - Review]] examples. Focus on PMF, CDF.

For Taylor Series, I expect a question similar to ### Example 2: 8-bit ASCII "b" in [[4 - Physical Layer Notes]] 

For Shannon/Nyquist, focus on [[4 - Physical Layer Notes]] end of note, especially SNR and line capacity.



## 2. Baseband/Passband transmission

### Baseband
![[baseband.png | 400]]
Given a bit stream, draw the resulting wave using X. (NRZ, Manchester, etc)

### Passband
![[passband1.png | 400]]
"what type is this?" questions


### Clock Recovery

Maybeee he gives you the 4b/5b table and asks you to map a bitstream? idk

Most likely general questions about why clock recovery


<div style="page-break-after: always;"></div>

## 3. OFDM and CDMA

1. Given a diagram, how many times packets were blocked, what's the approx success rate
2. CDMA questions using codes in [[11 - CDMA Derivation]]. Given 3 codes, are they orthogonal? 

### Example of CDMA: 


Given the following three CDMA chipping sequences (codes) assigned to User A, User B, and User C, determine if they are mutually orthogonal.

- **Code A:** `[1, 1, 1, 1]`
    
- **Code B:** `[1, -1, 1, -1]`
    
- **Code C:** `[1, 1, -1, -1]`
    



we must calculate the inner-product for every possible pair. If the inner-product of all three pairings equals exactly zero, the entire set is mutually orthogonal.

**Step 1: Check Pair A and B**

Multiply the corresponding elements of Code A and Code B, then add the results:

- $A \cdot B = (1 \times 1) + (1 \times -1) + (1 \times 1) + (1 \times -1)$
    
- $A \cdot B = 1 - 1 + 1 - 1$
    
- **Result:** $0$
    
    _(Code A and Code B are orthogonal)_
    

**Step 2: Check Pair A and C**

Multiply the corresponding elements of Code A and Code C, then add the results:

- $A \cdot C = (1 \times 1) + (1 \times 1) + (1 \times -1) + (1 \times -1)$
    
- $A \cdot C = 1 + 1 - 1 - 1$
    
- **Result:** $0$
    
    _(Code A and Code C are orthogonal)_
    

**Step 3: Check Pair B and C**

Multiply the corresponding elements of Code B and Code C, then add the results:

- $B \cdot C = (1 \times 1) + (-1 \times 1) + (1 \times -1) + (-1 \times -1)$
    
- $B \cdot C = 1 - 1 - 1 + 1$
    
- **Result:** $0$
    
    _(Code B and Code C are orthogonal)_
    
Because the inner-product of every single pairing (A&B, A&C, and B&C) is exactly zero, these three codes are mutually orthogonal and can be successfully used together in a CDMA network.


<div style="page-break-after: always;"></div>

## 4. Erlang B

Either of these:
1. Derivation to recursive form from [[8 - Erlang Recursive Form]]
2. Questions which use the Erlang Formula
3. From the graph, if the offered load is $\rho$ Erlangs, our target is X%, how many trunks would we need? or variations where 2 of the 3 variables are given.
![[trunks and erlang.png | 300]]

### Erlang Formula: Example 1

Suppose call arrivals are Poisson, the offered load is $\rho = 2$ Erlangs, and the system has $c = 3$ trunks. Write the Erlang B formula for the blocking probability.

$$
P_b = \frac{\frac{\rho^c}{c!}}{\sum_{j=0}^{c} \frac{\rho^j}{j!}}
$$

Substitute the numbers:

$$
P_b = \frac{\frac{2^3}{3!}}{\sum_{j=0}^{3} \frac{2^j}{j!}}
$$


### Erlang Formula: Example 2

Suppose calls arrive at rate $\lambda = 2$ calls/sec and the average holding time is $E(X) = 3$ sec.

Step 1: compute offered load:

$$
\rho = \lambda E(X) = 2 \times 3 = 6
$$

So the system offers `6 Erlangs` of traffic.

If the question then gives a number of trunks $c$, substitute $\rho = 6$ into Erlang B:

$$
P_b = \frac{\frac{6^c}{c!}}{\sum_{j=0}^{c} \frac{6^j}{j!}}
$$
<div style="page-break-after: always;"></div>

![[trunks and erlang.png | 500]]

### Erlang Graph: Example 1

If the graph gives:

- offered load $\rho = 5$ Erlangs
- target blocking probability = `1%`

Then from the graph, we need about:

- $c \approx 11$ trunks



### Erlang Graph: Example 2

If the graph gives:

- offered load $\rho = 10$ Erlangs
- number of trunks $c = 18$

Then from the graph, we estimate the blocking probability to be about:

- $P_b \approx 100\%$




<div style="page-break-after: always;"></div>

# Multiple Choice Questions



## Notes 0 & 1 - Intro

### Multiple Choice

1. Which network device operates at the Physical layer and copies ALL bits between networks?
   A. Bridge
   B. Router
   C. Repeater
   D. Gateway
   **Answer: C**

2. In the OSI model, which layer is responsible for routing packets from source to destination?
   A. Data Link layer
   B. Network layer
   C. Transport layer
   D. Physical layer
   **Answer: B**

3. IPv6 addresses are how many bytes?
   A. 4
   B. 8
   C. 16
   D. 32
   **Answer: C**

4. A VPN is best described as:
   A. A PAN using Bluetooth
   B. A LAN using Wi-Fi
   C. A WAN built from virtual links
   D. A MAN using fiber optics
   **Answer: C**

5. In the TCP/IP model, which OSI layers are combined into the Application layer?
   A. Physical and Data Link
   B. Network and Transport
   C. Session and Presentation
   D. Data Link and Network
   **Answer: C**

6. Which OSI layers are present in the OSI model but not explicitly present in the TCP/IP model?
   A. Network and Data Link
   B. Session and Presentation
   C. Physical and Transport
   D. Transport and Application
   **Answer: B**

7. Communication between two modules at the **same layer** on different machines is called:
   A. A service
   B. A protocol
   C. A socket
   D. A frame
   **Answer: B**

8. Communication between two modules in **different layers** inside the same machine is provided through:
   A. A service
   B. A protocol
   C. Routing
   D. Multiplexing
   **Answer: A**


### True / False

1. A socket links two processes together — **True**
2. A router operates at the Data Link layer — **False** (routers operate at the Network layer)
3. A bridge filters frames by examining headers — **True**
4. The Presentation layer handles data compression and security — **True**
5. RFID refers to a logical port connection — **False** (RFID is a chip/tag identification technology, not a logical port connection)




## Note 2 - Review

### Multiple Choice

1. For a discrete random variable, what function defines Prob(X = x)?
   A. CDF
   B. PDF
   C. PMF
   D. MGF
   **Answer: C**

2. For an Exponential random variable with mean $E[X] = 10$, what is $\mu$?
   A. 0.1
   B. 1
   C. 10
   D. 100
   **Answer: A**

3. Var(X) equals:
   A. E(X) − E(X²)
   B. E(X²) − (E(X))²
   C. (E(X))² − E(X²)
   D. E(X²) + (E(X))²
   **Answer: B**

4. The Poisson distribution is commonly used to model:
   A. Battery lifetimes
   B. Network inter-arrival times
   C. Continuous signal amplitudes
   D. Physical layer bit errors
   **Answer: B**

5. According to Bayes' Rule, P(A|B) equals:
   A. P(A) × P(B) / P(A)
   B. P(B|A) × P(A) / P(B)
   C. P(A,B) / P(B)
   D. P(A) / P(B)
   **Answer: B**

### True / False

1. The CDF defines the probability that a variable equals a specific value — **False** (for a discrete variable, the PMF gives the probability of an exact value)
2. For Exponential distribution, $\mathrm{Var}(X) = \frac{1}{\mu^2}$ — **True**
3. The Exponential distribution is memoryless — **True**
4. For a Poisson RV, $E[X] = \lambda$ and $\mathrm{Var}(X) = \lambda$ — **True**
5. The inter-arrival time of a Poisson process follows an Exponential distribution — **True**


## Note 3 - Physical Layer

### Multiple Choice

1. According to Nyquist's Theorem, what determines the maximum data rate of a noiseless channel?
   A. Signal-to-noise ratio only
   B. Bandwidth and signal-to-noise ratio
   C. Bandwidth and number of signal levels
   D. Frequency and amplitude
   **Answer: C**

2. What type of fading occurs when delayed multipath copies of a symbol overlap with the next symbol?
   A. Large-scale fading
   B. Frequency-flat fading
   C. Inter-symbol interference (ISI)
   D. Shadowing
   **Answer: C**

<div style="page-break-after: always;"></div>

2. In OFDM, what property allows subcarriers to overlap in frequency without interfering with each other?
   A. Orthogonality
   B. Guard intervals
   C. Parallel transmission
   D. FFT processing
   **Answer: A**
3. For the diagram below:
![[graycoded.png | 400]]
   A. A is gray-coded
   B. B is gray-coded
   C. Both are gray-coded
   D. None are gray-coded
   **Answer: A**
   


4. Which line code embeds the clock directly into the signal by XORing the clock with the data stream?
   A. NRZ
   B. NRZI
   C. Manchester
   D. 4B/5B
   **Answer: C**

5. What is the main advantage of Gray coding in constellation diagrams?
   A. Increases the number of constellation points
   B. Reduces errors so that neighboring points differ by only one bit
   C. Improves signal strength
   D. Allows higher bandwidth
   **Answer: B**

6. Which theorem gives the maximum theoretical data rate of a noisy channel?
   A. Nyquist's Theorem
   B. Shannon's Theorem
   C. Erlang B formula
   D. Bayes' Rule
   **Answer: B**

<div style="page-break-after: always;"></div>

7. What does a higher SNR generally imply?
   A. Lower possible data rate
   B. More severe fading
   C. The signal stands out more clearly from noise
   D. Less bandwidth is available
   **Answer: C**

8. Which wireless propagation mechanism refers to signal bouncing off large surfaces such as walls or the ground?
   A. Diffraction
   B. Reflection
   C. Scattering
   D. Refraction
   **Answer: B**

9. What is channel sounding mainly used for?
   A. Encrypting the channel
   B. Measuring and characterizing the propagation channel
   C. Increasing carrier frequency
   D. Preventing routing loops
   **Answer: B**

10. The channel impulse response describes:
   A. How routers queue packets over time
   B. How one transmitted pulse is spread by the channel
   C. How TCP retransmits lost segments
   D. How modulation changes phase only
   **Answer: B**

11. What does **multipath** mean in a wireless channel?
   A. A packet is duplicated by the router
   B. The same transmitted signal reaches the receiver through multiple physical paths
   C. The transmitter uses multiple transport protocols
   D. A user connects to multiple ISPs at once
   **Answer: B**

12. In the convolution expression for channel output, what does `y(t)` represent?
   A. The transmitted signal
   B. The channel impulse response
   C. The received signal
   D. The noise power
   **Answer: C**

13. Large-scale fading is mainly caused by:
   A. Rapid constructive and destructive addition of multipath components over very short distances
   B. Distance and shadowing from large objects such as buildings or hills
   C. FFT processing errors
   D. Adjacent channel interference only
   **Answer: B**

14. Small-scale fading is mainly caused by:
   A. Long-distance path loss only
   B. Multipath interference causing rapid signal fluctuations
   C. Network congestion
   D. Low battery power at the receiver
   **Answer: B**

15. Frequency-selective fading is more likely when:
   A. Symbol duration is very large compared to delay spread
   B. Signal bandwidth is much smaller than channel bandwidth
   C. Different frequency components are affected differently by the channel
   D. There is no multipath
   **Answer: C**

16. In OFDM, the subcarrier spacing rule is:
   A. $\Delta f = T_{sym}$
   B. $\Delta f = 1/T_{sym}$
   C. $\Delta f = 2T_{sym}$
   D. $\Delta f = B/T_{sym}$
   **Answer: B**

17. What makes OFDM practical in real systems?
   A. Replacing all filters with routers
   B. Using FFT/IFFT to generate and separate many subcarriers efficiently
   C. Avoiding digital signal processing
   D. Using only one carrier at a time
   **Answer: B**

18. In QPSK, one symbol represents how many bits?
![[qpsk.png | 150]]
   A. 1
   B. 2
   C. 3
   D. 4
   **Answer: B**

20. Compared to BPSK, QPSK mainly improves:
![[qpsk-bskksks.png | 200]]
   A. Cable length
   B. Spectral efficiency
   C. Packet routing
   D. Clock recovery
   **Answer: B**

22. What is a main advantage of optical fiber over copper for backbone links?
   A. It has lower bandwidth but lower cost
   B. It supports high rates over long distances with low attenuation
   C. It requires no modulation
   D. It only works for analog voice
   **Answer: B**

23. In the PSTN, what is the local loop?
   A. The fiber link between ISPs
   B. The wireless hop between cell towers
   C. The access link between the customer's premises and the local telephone office
   D. The switching fabric inside a router
   **Answer: C**

24. What does POTS stand for?
   A. Packet Oriented Transmission System
   B. Plain Old Telephone Service
   C. Public Office Trunk Service
   D. Primary Optical Transfer System
   **Answer: B**

25. DSL improves the local loop mainly by:
   A. Replacing copper with satellite links
   B. Using higher frequencies on the same old telephone line for data
   C. Using only analog signaling
   D. Reserving a full circuit for web browsing
   **Answer: B**

26. What does ADSL stand for?
   A. Analog DSL
   B. Advanced Digital Subscriber Link
   C. Asymmetric Digital Subscriber Line
   D. Automatic Data Switching Line
   **Answer: C**

27. In FTTH, the main bottleneck removed compared to DSL is:
   A. The IP layer
   B. The old copper local loop
   C. The need for multiplexing
   D. The wireless air interface
   **Answer: B**

28. PSTN trunks usually carry many calls digitally using:
   A. CSMA/CD
   B. Pure ALOHA
   C. TDM
   D. Token passing
   **Answer: C**

<div style="page-break-after: always;"></div>

29. Which statement best describes circuit switching?
   A. Packets are independently routed with no setup
   B. Resources are reserved in advance for the whole call
   C. Packets are stored and forwarded hop by hop
   D. All users share the medium randomly
   **Answer: B**

30. Which statement best describes packet switching?
   A. It always reserves bandwidth before data transfer
   B. It avoids queueing delay completely
   C. It forwards data in packets that may experience variable delay
   D. It requires a dedicated end-to-end channel
   **Answer: C**

31. "Store-and-forward" in packet switching means a router:
   A. Amplifies the signal continuously
   B. Stores a packet briefly before forwarding it on the next link
   C. Reserves a circuit before transmission
   D. Converts every packet into a circuit
   **Answer: B**

32. In GSM architecture, which path best matches the logical flow of communication?
   A. Mobile -> router -> modem -> PSTN
   B. Mobile -> air interface -> base station -> BSC -> MSC -> PSTN/network
   C. Mobile -> DSLAM -> trunk -> ISP only
   D. Mobile -> FFT -> OFDM -> PSTN
   **Answer: B**

33. GSM uses which modulation?
   A. BPSK
   B. QPSK
   C. 16-QAM only
   D. FSK only
   **Answer: B**

34. The GSM air interface combines:
   A. CDMA and OFDMA
   B. FDM and TDM
   C. Circuit switching and packet switching
   D. DSL and FTTH
   **Answer: B**

### True / False

1. Shannon's Theorem applies to noisy channels while Nyquist's Theorem applies to noiseless channels. — **True**
2. Frequency-selective fading occurs when the signal bandwidth is much smaller than the channel bandwidth. — **False** (that condition is more consistent with frequency-flat behavior; frequency-selective fading occurs when different frequency components are affected differently)
3. In CDMA, all users transmit at the same time and over the same frequency range. — **True**
4. Single-mode fiber has a wider core than multi-mode fiber. — **False** (single-mode fiber has a narrower core than multi-mode fiber)
5. Circuit switching reserves dedicated resources for an entire call, while packet switching does not. — **True**
6. Large-scale fading refers to rapid short-distance fluctuations caused by multipath interference. — **False** (that describes small-scale fading; large-scale fading is due to distance and shadowing)
7. Multipath means several delayed copies of the same transmitted signal may arrive at the receiver through different paths. — **True**
8. Large-scale fading is mainly associated with distance and shadowing by large objects. — **True**
9. Small-scale fading refers to rapid short-distance fluctuations caused by multipath. — **True**
10. Small-scale fading changes only over very large distances and is unrelated to multipath. — **False** (small-scale fading varies over short distances and is strongly related to multipath)
11. Channel sounding sends a known signal so the receiver can estimate how the channel changes it. — **True**
12. The channel impulse response can be viewed as a set of delayed paths with different received powers. — **True**
13. Convolution is used to determine the received signal from the transmitted signal and the channel impulse response. — **True**
14. OFDM is the same as FDMA because both simply assign different frequency bands to different users. — **False** (FDMA is a multiple-access scheme, while OFDM is a modulation/multiplexing technique using orthogonal subcarriers)
15. In Gray coding, neighboring constellation points are labeled so a small error usually changes only one bit. — **True**
16. DSL sends data using frequencies that ordinary POTS voice service does not use. — **True**
17. FTTH replaces the copper local loop with fiber all the way to the customer. — **True**
18. Packet switching usually has little or no setup delay, but may experience variable queueing delay. — **True**
19. In circuit switching, once the circuit is set up, resources remain reserved for the duration of the call. — **True**
20. GSM is only about radio transmission and does not include subscriber identity or location tracking. — **False** (GSM also includes subscriber identity and location management)
21. OFDM subcarriers are spaced so that the peak of one occurs at the zero crossings of the others. — **True**

<div style="page-break-after: always;"></div>

## Note 4 - Physical Layer Notes

### Multiple Choice


1. If a data rate is 9600 bps, how many harmonics can be sent through a 3 kHz voice-grade line?
   A. 80
   B. 40
   C. 5
   D. 2
   **Answer: D** (3000 / (9600 / 2) = 3000 / 4800 < 1 full pair, so only about the fundamental fits, i.e. 2 harmonics)

2. What is the maximum data rate for a noiseless channel with 3 kHz bandwidth using a binary signal (V = 2)?
   A. 3000 bps
   B. 6000 bps
   C. 12000 bps
   D. 300 bps
   **Answer: B** (Nyquist: $2B \log_2 V = 2 \times 3000 \times \log_2 2 = 6000$)

3. An SNR of 40 dB is equivalent to what linear value?
   A. 40
   B. 100
   C. 1000
   D. 10000
   **Answer: D** ($10 \log_{10}(S/N) = 40 \Rightarrow S/N = 10^4 = 10000$)

### True / False

1. The RMS amplitude √(aₙ² + bₙ²) is proportional to the energy transmitted at the corresponding frequency. — **True**
2. Baseband signals are transmitted at their original frequency starting from 0 Hz. — **True**
3. A higher data rate results in more harmonics being transmitted through the same channel. — **False** (higher data rate usually means fewer harmonics fit through the same limited-bandwidth channel)
4. Shannon's capacity formula requires knowledge of the channel's bandwidth and SNR. — **True**

<div style="page-break-after: always;"></div>


## Note 6 - Circuit & Packet Switching

### Multiple Choice

1. In packet switching, what information do headers contain to ensure messages are reconstructed correctly?
   A. Only the sender's IP address
   B. Sequence information for reassembly
   C. The total number of routers in the path
   D. Encryption keys only
   **Answer: B**

2. Which of the following is a disadvantage of packet switching?
   A. High availability with no waiting for connections
   B. Resilient to line failures due to redirectable signals
   C. Data packets can get lost or corrupted in transit
   D. Uses available bandwidth to its full potential
   **Answer: C**

3. What are the three phases of circuit switching?
   A. Setup, Transfer, Terminate
   B. Establish, Transfer, Disconnect
   C. Connect, Send, End
   D. Initiate, Communicate, Close
   **Answer: B**

4. In the Erlang B formula, if all trunks are busy and a new call arrives, what happens?
   A. The call waits in a queue
   B. The call is delayed and retried
   C. The call is rejected or blocked
   D. The call is routed to an alternate trunk
   **Answer: C**

5. What does offered load $\rho$ represent in a circuit-switched system?
   A. The number of packets dropped per second
   B. The average amount of traffic users try to place on the system
   C. The number of routers in the path
   D. The propagation delay of one call
   **Answer: B**

6. If calls arrive at rate $\lambda$ and the average call duration is $E(X)$, the offered load is:
   A. $\rho = \lambda + E(X)$
   B. $\rho = \lambda / E(X)$
   C. $\rho = \lambda \cdot E(X)$
   D. $\rho = E(X) / \lambda$
   **Answer: C**

<div style="page-break-after: always;"></div>

7. What does utilization measure in a trunked system?
   A. The fraction of total trunk capacity used on average
   B. The number of blocked users only
   C. The total number of packets in a queue
   D. The ratio of bandwidth to propagation speed
   **Answer: A**

8. If utilization is very high, what is the usual tradeoff?
   A. Lower efficiency and lower blocking
   B. Higher efficiency but more chance of blocking
   C. No effect on blocking
   D. All trunks remain idle
   **Answer: B**

9. Why are more trunks usually provisioned than the offered load alone might suggest?
   A. To increase propagation speed
   B. To guarantee zero noise
   C. To keep the blocking probability below a target
   D. To make packet headers shorter
   **Answer: C**

10. Which statement best describes trunk concentration?
   A. Every line always gets its own dedicated long-distance circuit
   B. Traffic from many lines is concentrated onto fewer shared trunks
   C. Packet switching avoids all blocking by using trunks
   D. Trunks are only used in wireless networks
   **Answer: B**

11. Which model is appropriate when blocked calls are lost immediately?
   A. Erlang A
   B. Erlang B
   C. Erlang C
   D. Slotted ALOHA
   **Answer: B**

12. Which switching approach is usually better at handling rerouting after line failures?
   A. Circuit switching only
   B. Packet switching
   C. Pure ALOHA
   D. Token passing
   **Answer: B**

13. In circuit switching, the setup phase happens:
   A. After all data is transferred
   B. Before steady data transfer begins
   C. Only in packet-switched networks
   D. Only when trunks are idle
   **Answer: B**


<div style="page-break-after: always;"></div>


### True / False

1. In packet switching, all packets of the same message must take the same route to the destination. — **False** (packets may take different routes and still be reassembled at the destination)
2. Circuit switching dedicates an entire channel to a call for its full duration. — **True**
3. The offered load $\rho$ is calculated by dividing arrival rate $\lambda$ by service rate $\mu$. — **False** (the notes define offered load as $\rho = \lambda \cdot E(X)$, which equals $\lambda/\mu$ only when $E(X) = 1/\mu$)
4. Erlang B is used when blocked calls are delayed and wait in a queue. — **False**
5. In circuit switching, traffic surges from events like Mother's Day do not require special management since the dedicated channel handles all traffic. — **False** (traffic surges can still cause blocking because the number of reserved circuits is limited)
6. Utilization tells us how busy each trunk is on average. — **True**
7. If utilization equals $1$, the trunks are busy all the time on average. — **True**
8. In Erlang B, there is effectively no waiting room for blocked calls. — **True**
9. Trunk concentration can still lead to blocking when all shared trunks are busy. — **True**



## Note 8 - Erlang Recursive Form

### Multiple Choice

1. The Erlang B formula $B(p,c)$ is expressed as:
   A. $\left(\frac{p^c}{c!}\right) \times \sum_{j=0}^{c} \frac{p^j}{j!}$
   B. $\left(\frac{p^c}{c!}\right) \Big/ \sum_{j=0}^{c} \frac{p^j}{j!}$
   C. $\sum_{j=0}^{c} \frac{p^j}{j!} \Big/ \left(\frac{p^c}{c!}\right)$
   D. $\frac{p^c}{c! + \sum_{j=0}^{c-1} \frac{p^j}{j!}}$
   **Answer: B**

2. In the recursive Erlang B formula, $B(p,c)$ is expressed in terms of:
   A. $B(p,c-1)$ multiplied by $p/c$
   B. $B(p,c-1)$ with denominator $c + p \cdot B(p,c-1)$
   C. $B(p,c+1)$ with numerator $p$
   D. $B(p-1,c)$ with denominator $c$
   **Answer: B**

3. When deriving the recursive form, what key identity is used to relate $B(p,c-1)$ to the original formula?
   A. $B(p,c-1) = \sum_{j=0}^{c-1} \frac{p^j}{j!}$
   B. $B(p,c-1) = \left(\frac{p^{c-1}}{(c-1)!}\right) \Big/ \sum_{j=0}^{c-1} \frac{p^j}{j!}$
   C. $B(p,c-1) = \left(\frac{p^{c-1}}{(c-1)!}\right) \times \sum_{j=0}^{c-1} \frac{p^j}{j!}$
   D. $B(p,c-1) = c \times \left(\frac{p^{c-1}}{(c-1)!}\right)$
   **Answer: B**

4. What algebraic technique is used to transform the standard Erlang B formula into its recursive form?
   A. Integration by parts
   B. Multiplying by $1$ in the form of $\frac{1/\sum (p^j/j!)}{1/\sum (p^j/j!)}$
   C. Taylor series expansion
   D. Logarithmic transformation
   **Answer: B**

5. In the derivation, the numerator is rewritten as $p/c$ times an expression that represents:
   A. $B(p,c)$ with one fewer trunk
   B. The sum of all traffic load
   C. The factorial of c
   D. The Poisson distribution
   **Answer: A**

### True / False

1. The recursive Erlang B formula allows computation without calculating large factorials. — **True**
2. In the derivation, the expression $\frac{p^c}{c!}$ can be rewritten as $\frac{p}{c} \times \frac{p^{c-1}}{(c-1)!}$. — **True**
3. The recursive form $B(p,c) = \frac{p \cdot B(p,c-1)}{c + p \cdot B(p,c-1)}$ is equivalent to the standard Erlang B formula. — **True**
4. The derivation shows that multiplying by $1$ (in the form of a fraction divided by itself) changes the value of the Erlang B formula. — **False** (multiplying by $1$ does not change the value; it only rewrites the expression)


## Note 9 - Multiple Access

### Multiple Choice

1. In the OSI model, which layer handles routing of datagrams from source to destination?
   A. Application
   B. Transport
   C. Network
   D. Link
   **Answer: C**

2. What is the maximum efficiency of Slotted ALOHA?
   A. 18%
   B. 37%
   C. 50%
   D. 100%
   **Answer: B**

3. In CDMA, what allows multiple users to transmit at the same time and frequency without interfering with each other?
   A. Time slots
   B. Frequency bands
   C. Unique orthogonal codes
   D. Central controller
   **Answer: C**

4. What does CSMA/CD stand for?
   A. Carrier Sense Multiple Access with Collision Avoidance
   B. Carrier Sense Multiple Access with Collision Detection
   C. Code Division Multiple Access with Collision Detection
   D. Channel Partitioning with Collision Detection
   **Answer: B**

5. Which MAC protocol class uses "taking turns" to avoid collisions?
   A. Channel Partitioning
   B. Random Access
   C. Taking Turns Protocols
   D. CSMA
   **Answer: C**

6. Which channel partitioning method gives each station a fixed time slot in each round?
   A. FDMA
   B. CDMA
   C. TDMA
   D. CSMA
   **Answer: C**

<div style="page-break-after: always;"></div>

7. Which channel partitioning method divides the total spectrum into separate frequency bands?
   A. TDMA
   B. FDMA
   C. CDMA
   D. Polling
   **Answer: B**

8. In CDMA, the receiver recovers a user's data by:
   A. Waiting for a time slot boundary
   B. Measuring trunk utilization
   C. Correlating the received signal with that user's code
   D. Reserving a dedicated circuit
   **Answer: C**

9. Which protocol requires time synchronization but no central controller?
   A. Pure ALOHA
   B. Slotted ALOHA
   C. CSMA
   D. Token passing
   **Answer: B**

10. Which protocol transmits immediately when a frame arrives, without slot synchronization?
   A. Slotted ALOHA
   B. Pure ALOHA
   C. TDMA
   D. Polling
   **Answer: B**

11. Why can collisions still happen in CSMA?
   A. Because CSMA uses orthogonal codes
   B. Because there is always a central master
   C. Because propagation delay may prevent a node from hearing another transmission in time
   D. Because all users must transmit in the same slot
   **Answer: C**

12. What is the main benefit of CSMA/CD over plain CSMA?
   A. It prevents all collisions
   B. It aborts transmission early after detecting a collision
   C. It assigns fixed frequency bands
   D. It requires no hardware support
   **Answer: B**

13. In polling, who gives permission to transmit?
   A. A circulating token
   B. A master node
   C. The FFT
   D. A router
   **Answer: B**

<div style="page-break-after: always;"></div>

14. In token passing, what gives a node the right to transmit?
   A. Detecting an idle carrier
   B. Receiving the token
   C. Being closest to the base station
   D. Winning a collision
   **Answer: B**

15. Which protocol family is usually better under high load because it avoids repeated collisions?
   A. Taking-turns protocols
   B. Pure random access only
   C. Packet switching
   D. Baseband signaling
   **Answer: A**

16. Which statement best describes the main downside of channel partitioning at low load?
   A. It always causes collisions
   B. Reserved pieces may sit idle when users have nothing to send
   C. It requires packet retransmission after every frame
   D. It cannot be decentralized
   **Answer: B**

### True / False

1. In Pure ALOHA, no clock synchronization is required. — **True**
2. TDMA requires clock synchronization and is not fully decentralized. — **True**
3. In CSMA/CD, collisions are prevented from ever occurring. — **False** (CSMA/CD detects collisions after they occur and aborts early; it does not prevent them completely)
4. Token passing requires a central master node to coordinate transmissions. — **False** (token passing uses a circulating token, not a central master)
5. Pure ALOHA has worse efficiency than Slotted ALOHA because its vulnerable period is twice as long. — **True**
6. In FDMA, all stations can transmit at the same time as long as each stays in its assigned frequency band. — **True**
7. In TDMA, if a station has nothing to send during its slot, that slot may be wasted. — **True**
8. CDMA separates users by assigning each one a unique code rather than a fixed time slot or frequency band. — **True**
9. Slotted ALOHA is fully free of coordination because it does not require any synchronization. — **False** (Slotted ALOHA still requires time synchronization so everyone agrees on slot boundaries)
10. CSMA requires local carrier sensing but no global clock synchronization. — **True**
11. Polling is decentralized because no special node is needed. — **False** (polling requires a master/controller node)
12. Token passing avoids the need for a central master, but still requires nodes to maintain the token order correctly. — **True**
13. Taking-turns protocols can feel wasteful under low load because the control overhead may exceed the benefit. — **True**


## Note 10 - OFDMA

### Multiple Choice

1. What does OFDMA stand for?
   A. Orthogonal Frequency Division Multiplexing
   B. Orthogonal Frequency Division Multiple Access
   C. OFDM Time Division Multiple Access
   D. Optimized Frequency Division Multiple Access
   **Answer: B**

2. What is the main disadvantage of OFDM-TDMA compared to OFDMA?
   A. High latency when many users are present
   B. Low spectral efficiency
   C. Requires more power
   D. Cannot use subcarriers
   **Answer: A**

3. Multi-user diversity exists because:
   A. All users always see the same channel conditions
   B. Different users see different channel conditions at the same time
   C. Users are allocated fixed frequency bands
   D. The base station assigns subcarriers randomly
   **Answer: B**

4. In OFDMA, what does the base station use to make resource allocation decisions?
   A. Only time slots
   B. Channel gain and QoS requirements
   C. Fixed frequency assignments
   D. Token passing order
   **Answer: B**

5. What is the orthogonal subcarrier spacing rule inherited from OFDM and used in OFDMA systems?
   A. $\Delta f = T_{sym}$
   B. $\Delta f = \frac{1}{T_{sym}}$
   C. $\Delta f = 2T_{sym}$
   D. $\Delta f = \frac{B}{T_{sym}}$
   **Answer: B**

6. Why is the wireless channel described as time-varying?
   A. Because FFT size changes every packet
   B. Because users and surrounding objects can move, changing the channel over time
   C. Because OFDMA requires fixed channels
   D. Because subcarrier spacing is random, and time stretches with space
   **Answer: B**

<div style="page-break-after: always;"></div>

7. Which of the following is listed as a goal of OFDMA resource allocation?
   A. Maximize throughput
   B. Remove all fading permanently
   C. Eliminate the need for QoS
   D. Force all users onto the same subcarrier
   **Answer: A**

8. In OFDMA resource allocation, each subcarrier is:
   A. Shared by all users simultaneously all the time
   B. Exclusively assigned to one user at a given time
   C. Reserved permanently for the base station only
   D. Used only for control signaling
   **Answer: B**

9. Besides channel gain, what else does the base station consider?
   A. Only packet headers
   B. QoS requirements such as rate and dropping rate
   C. Only antenna color
   D. Only user IP addresses
   **Answer: B**

10. What is the basic idea of space diversity?
   A. Use one antenna and increase transmit power forever
   B. Use multiple separated antennas so they do not fade deeply at the same time
   C. Use only frequency diversity
   D. Assign the same subcarrier to every user
   **Answer: B**

11. Why do two antennas separated by several wavelengths help in space diversity?
   A. They always receive identical fades
   B. They usually do not experience deep fades at the same instant
   C. They remove the need for OFDM
   D. They make the channel static
   **Answer: B**

### True / False

1. OFDM is a modulation technique for one user, while OFDMA adds multiple access capability. — **True**
2. In OFDMA, a single subcarrier can be assigned to multiple users simultaneously at the same time. — **False** (each subcarrier is assigned exclusively to one user at a given time)
3. OFDMA shares resources in both time and frequency, unlike OFDM-TDMA which shares only by time. — **True**
4. Space diversity uses a single antenna to combat fading. — **False** (space diversity uses multiple antennas separated in space)
5. OFDMA typically uses static allocation because channel conditions remain constant over time. — **False** (OFDMA benefits from dynamic allocation because wireless channels vary over time)
6. User movement is one reason the wireless channel can vary over time. — **True**
7. Objects moving between transmitter and receiver can change channel conditions. — **True**
8. OFDMA resource allocation may consider both channel gain and QoS. — **True**
9. One goal of OFDMA resource allocation is to keep total transmit power below a maximum. — **True**
10. Space diversity works because multiple separated antennas are unlikely to experience identical fading all the time. — **True**
11. In space diversity, the receiver may choose or combine signals from different antennas. — **True**
12. Time-varying channels mean the best user for a given subcarrier can change over time. — **True**


## Note 11 - CDMA Derivation

### Multiple Choice

1. In CDMA, what does a result of -1 from the detection process indicate?
   A. The user sent bit 1
   B. The user sent bit 0
   C. The user was silent
   D. A collision occurred
   **Answer: B**

2. If two chip sequences are orthogonal, their normalized dot product equals:
   A. 1
   B. -1
   C. 0
   D. The code length m
   **Answer: C**

3. A channel using 8-chip codes can support at most how many mutually orthogonal stations?
   A. 2
   B. 4
   C. 8
   D. 16
   **Answer: C**


4. When decoding using the dot product method, a result of 0 indicates the user:
   A. Sent bit 1
   B. Sent bit 0
   C. Was silent
   D. Sent the complement of their code
   **Answer: C**

<div style="page-break-after: always;"></div>

### True / False

1. In CDMA, orthogonal codes cancel each other out during detection because their dot product equals zero. — **True**
2. A code matched with itself gives a result of 1, while the same code matched with its complement gives -1. — **True**
3. With N-chip codes, CDMA can support more than N mutually orthogonal stations. — **False** (with N-chip codes, the maximum number of mutually orthogonal codes is N)
4. In a lossy/noisy channel, the practical number of CDMA stations is typically greater than N. — **False** (noise and non-ideal conditions usually reduce the practical number of supported stations)
5. The code matched with an orthogonal user's code contributes a total of +1 to the detection result. — **False** (an orthogonal user's code contributes 0 in the ideal dot-product detection)



## Note 12 - Slotted ALOHA Performance

### Multiple Choice

1. What is the optimal probability $p^*$ that maximizes the success probability in slotted ALOHA?
   A. $p^* = 1$
   B. $p^* = 1/n$
   C. $p^* = 1/(2n)$
   D. $p^* = 2/n$
   **Answer: B**

2. What is the maximum throughput efficiency of slotted ALOHA as the number of users becomes very large?
   A. 0.18
   B. 0.37
   C. 0.50
   D. 0.75
   **Answer: B**

3. The capacity of a slotted ALOHA network is calculated as:
   A. $P_s + R$
   B. $P_s / R$
   C. $P_s × R$
   D. $R / P_s$
   **Answer: C**

4. In Pure ALOHA, what is the vulnerable period compared to Slotted ALOHA?
   A. Half as large
   B. The same
   C. Twice as large
   D. Four times as large
   **Answer: C**

5. For Pure ALOHA with a large number of users, what is the approximate maximum efficiency?
   A. 8%
   B. 18%
   C. 37%
   D. 50%
   **Answer: B**

### True / False

1. In slotted ALOHA, the success probability for one specific user is $p(1-p)^(n-1)$. — **True**
2. The capacity per user in slotted ALOHA is calculated as $(P_s × R) / n$. — **True**
3. Pure ALOHA has a higher maximum efficiency than Slotted ALOHA. — **False** (Pure ALOHA has lower maximum efficiency because its vulnerable period is larger)
4. The optimal transmission probability for Pure ALOHA is approximately $1/(2n)$. — **True**
5. As $n \to \infty$, the maximum success probability of slotted ALOHA approaches $e^{-1} \approx 0.37$. — **True**
