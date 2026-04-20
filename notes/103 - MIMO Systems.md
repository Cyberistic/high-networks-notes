![[AaaaaAAAAA.jpeg | 300]]
aaaaAAAAAAA gleglegleglooopy 
boss i'm tired #no_mercy 

This note is a continuation of [[10 - OFDMA]]. 

## MIMO Systems

![[mimo-systems-overview.png | 500]]

**MIMO** stands for **Multiple Input Multiple Output**.

The basic idea is to use **multiple transmit antennas** and **multiple receive antennas** instead of just one antenna on each side.

This lets the system improve one or both of these:

- **quality** of communication, such as better BER
- **data rate**, by sending more information at the same time

<div style="page-break-after: always;"></div>

### Antenna System Types

The slide compares a few antenna setups:

- **SISO** = Single Input / Single Output
  - one transmit antenna
  - one receive antenna
  - this is the basic old setup

- **SIMO** = Single Input / Multiple Output
  - one transmit antenna
  - multiple receive antennas
  - helps mainly at the receiver side

- **MISO** = Multiple Input / Single Output
  - multiple transmit antennas
  - one receive antenna
  - helps mainly at the transmitter side

- **MIMO** = Multiple Input / Multiple Output
  - multiple transmit antennas
  - multiple receive antennas
  - gives the most flexibility and the biggest performance gains

The slide also shows the MIMO channel model:

$$
y(k) = Hx(k) + v(k)
$$

where:

- $x(k)$ = transmitted signal vector at time/sample $k$
- $H$ = channel matrix between transmit and receive antennas
- $y(k)$ = received signal vector
- $v(k)$ = noise


- with one antenna, there is basically one path from transmitter to receiver
- with many antennas, each transmit antenna can affect each receive antenna
- so the channel becomes a **matrix**, not just one number

<div style="page-break-after: always;"></div>

## MIMO Basics


- MIMO improves **BER / quality** and/or **data rate**
- it does this by using multiple TX/RX antennas

**BER** = **Bit Error Rate**, meaning the fraction/probability of transmitted bits that are received incorrectly.

### Core Scheme: Space-Time Coding

**space-time coding (STC)**:

The name already tells you the idea:

- **space** = use multiple antennas
- **time** = spread or organize symbols across different time instants too

to make transmission more robust or more efficient.

### Two Main Functions of STC



#### 1. Diversity

This is about **reliability**.

The same information is sent in a smarter redundant way across different antennas and/or times so that fading or noise hurts it less.

Goal:

- improve BER
- make the link more robust

#### 2. Multiplexing

This is about **rate**.

Different data streams are sent in parallel from different antennas.

Goal:

- increase bits/sec
- exploit the antenna dimension to carry more data


tl;dr:
- **diversity** -> better reliability
- **multiplexing** -> higher throughput

<div style="page-break-after: always;"></div>

## MIMO with OFDMA

![[mimo-ofdma.png | 400]]

MIMO can be combined with OFDMA.


- **OFDMA** handles sharing resources across subcarriers, time, users, and power
- **MIMO** uses multiple antennas to improve quality and/or rate


At the transmitter side:


- QAM (**Quadrature Amplitude Modulation**, recall constellation diagrams) symbols enter
- `S/P` converts serial data to parallel
- `IFFT` creates the OFDM symbol
- cyclic prefix is inserted. Cyclic prefix (CP) is a small copy of the end of an OFDM symbol that is pasted at the beginning before transmission.it helps absorb delayed echoes from multipath and reduce inter-symbol interference (ISI)
- signals are transmitted from multiple antennas

At the receiver side:

- cyclic prefix is removed
- data is converted back into parallel form
- `FFT` recovers the subcarriers
- **equalization** helps undo the channel effect and remove distortion

### Why combine them?

Because the two techniques solve different problems:

- OFDMA is very good for frequency-selective wireless channels and multi-user scheduling
- MIMO adds spatial diversity or spatial multiplexing

So together they can give:

- better robustness
- better throughput
- better overall wireless performance
- OFDMA gives many little frequency lanes
- MIMO gives many antenna paths
- using both means we are using the channel in **frequency**, **time**, and **space**



<div style="page-break-after: always;"></div>

## Multiple Choice Questions

1. What does MIMO stand for?
   A. Multiple Input Multiple Output
   B. Multi-Interval Multi-Operator
   C. Maximum Input Minimum Output
   D. Modulated Input Modulated Output
   **Answer: A**

2. Which antenna configuration uses one transmit antenna and multiple receive antennas?
   A. SISO
   B. SIMO
   C. MISO
   D. MIMO
   **Answer: B**


3. What is the main purpose of diversity in MIMO?
   A. Increase routing speed
   B. Improve reliability / BER
   C. Eliminate FFT
   D. Reduce the number of users
   **Answer: B**

4. What is the main purpose of multiplexing in MIMO?
   A. Increase data rate
   B. Reduce antenna count
   C. Eliminate fading completely
   D. Replace OFDM
   **Answer: A**

5. In the MIMO channel model $y(k) = Hx(k) + v(k)$, what does $H$ represent?
   A. Header bits
   B. Channel matrix
   C. Hamming distance
   D. Harmonic number
   **Answer: B**

6. In a MIMO-OFDMA transmitter, which block creates the OFDM symbol?
   A. FFT
   B. IFFT
   C. Equalizer
   D. Router
   **Answer: B**

7. Why combine OFDMA with MIMO?
   A. Because both do exactly the same job
   B. Because OFDMA uses frequency/time resources while MIMO adds spatial gains
   C. Because MIMO removes the need for subcarriers
   D. Because OFDMA only works in wired networks
   **Answer: B**

## True / False

1. MIMO uses multiple transmit and multiple receive antennas. — **True**
2. SISO means Single Input / Single Output. — **True**
3. Space-time coding uses only time and not multiple antennas. — **False** (space-time coding uses both the antenna dimension and the time dimension)
4. Diversity and multiplexing are two main functions of space-time coding. — **True**
5. Diversity is mainly used to improve reliability, while multiplexing is mainly used to increase data rate. — **True**
6. In SIMO, the system has multiple transmit antennas and one receive antenna. — **False** (SIMO means one transmit antenna and multiple receive antennas)
7. MIMO can be combined with OFDMA to improve performance. — **True**
8. Wireless channels suffer from both large-scale fading and small-scale fading. — **True**
