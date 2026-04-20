This is a continuation of OFDM from the Physical Layer note, but now the focus is on how OFDM is used for **multiple access**, not just one user's transmission.

## Quick refresher on OFDM

### What is OFDM?

![[what-is-ofdm.png | 300]]
![[carrier spacing.png | 300]]

**OFDM** stands for **Orthogonal Frequency Division Multiplexing**.

It is a way to split one high-rate **wideband** data stream into many lower-rate **narrowband** streams, then send them in parallel on many subcarriers.

Main ideas:

- many narrowband subcarriers are used instead of one big wideband carrier
- this makes the channel easier to handle, especially in multipath environments
- the subcarriers are packed very closely in frequency
- they can still be separated at the receiver because they are **orthogonal**

Normally, if carriers are placed too close, they interfere with each other.

<div style="page-break-after: always;"></div>

OFDM avoids that by choosing the subcarrier spacing carefully:

$$
\Delta f = \frac{1}{T_{sym}}
$$

where:

- $\Delta f$ = spacing between adjacent subcarriers
- $T_{sym}$ = OFDM symbol duration

So the practical takeaway is:

- ordinary FDM needs guard gaps between channels
- OFDM lets the subcarriers overlap in frequency in a controlled way
- this gives better spectral efficiency

> [!Note]
> In the Physical Layer note, OFDM was the idea of splitting **one user's** data across many orthogonal subcarriers. In this note, we go one step further and ask: how do we share those subcarriers among **multiple users**?
> - **FDMA** is a **multiple-access** idea: different users are given different frequency bands
> - **OFDM** is a **modulation / multiplexing** idea: one transmission is split across many orthogonal subcarriers

<div style="page-break-after: always;"></div>

## OFDM-TDMA MAC


![[ofdma-tdma-mac.png | 500]]

One simple way to let multiple users share an OFDM system is **OFDM-TDMA**.


- keep the OFDM physical layer
- but in each time slot, give the whole OFDM symbol to only **one user**
- then the next user gets the next time slot


- the sharing is mostly in **time**
- one user may use many or all subcarriers during its turn
- other users wait for their own turns

This is simple and organized, but not always efficient.

Advantages:

- easy implementation
- simple resource allocation
- low processing requirement
- low signaling overhead (channel gain)

Disadvantages:

- **high latency** when the number of users is large, because each user waits for a turn
- **inefficient power usage** 
- **inefficient frequency utilization**, because the system does not fully exploit which user is strongest on which subcarrier



<div style="page-break-after: always;"></div>

## Applications

![[ofdma-applications.png | 300]]

slopslopslopslopignore

OFDM and OFDMA appear in many practical systems.

The slides mention examples across several areas:

- **DVB-T** for digital video broadcasting
- **WLAN** systems such as `802.11a` / HiperLAN
- **BWA** such as `802.16`
- **cellular systems**, especially as systems evolved toward `4G`


<div style="page-break-after: always;"></div>

## Multi-user Diversity

![[multi-user-diversity.png | 500]]

**multi-user diversity**: Different users do **not** see the same channel conditions at the same time.

For example:

- one user may currently have a very strong channel on some subcarriers
- another user may be in a fade on those same subcarriers
- a third user may have better conditions on a different part of the spectrum

The key idea is:

- if the base station knows the channel quality of different users
- it does **not** have to treat everyone identically at every instant
- it can assign each subcarrier to the user who can use it best at that moment
- OFDMA works well because the wireless channel is not the same for everyone. If every user saw exactly the same channel all the time, there would be much less benefit from dynamic subcarrier assignment.



<div style="page-break-after: always;"></div>

## Time-Varying Channel

![[time-varrying-channel.png | 400]]

Wireless channels signal strength and conditions change over time. If your data was strong at 5AM in uni, it might be weak at 11AM at home, so can't rely on old sample data, must calculate continuously.
- the user moves
- objects move between transmitter and receiver
- reflectors and blockers in the environment change

The "best" user for a given subcarrier is not fixed forever.

At one moment:

- user `1` may have the strongest channel on a subcarrier

Later:

- user `2` may become the better choice

This is why OFDMA usually uses **dynamic** allocation rather than static allocation. The scheduler keeps adapting resource assignments as channel conditions change.

<div style="page-break-after: always;"></div>

## OFDMA

![[ofdma-overview.png | 300]]

**OFDMA** stands for **Orthogonal Frequency Division Multiple Access**.

This is the multiple-user version of OFDM.

In OFDMA:

- the system still uses orthogonal OFDM subcarriers
- but now different subcarriers can be assigned to different users
- each subcarrier is assigned exclusively to one user at a given time

So the sharing now happens in **both frequency and time**.

Instead of giving one whole OFDM symbol to one user, we can divide the time-frequency grid among many users at once.

### Why OFDMA is better than plain OFDM-TDMA

OFDMA fixes several weaknesses of OFDM-TDMA:

- lower latency, because many users can be served in the same OFDM symbol
- better frequency utilization, because different users can use different subcarriers at the same time
- better use of multi-user diversity, because the system can match subcarriers to the users who currently see them best

tl;dr:
- don't just ask "whose turn is it?"
- also ask "who is the best user for this specific subcarrier right now?"

### OFDM-TDMA vs OFDMA

| Scheme | How resources are shared | Main idea |
| --- | --- | --- |
| OFDM-TDMA | By time | One user uses the OFDM symbol at a time |
| OFDMA | By time and frequency | Different users can use different subcarriers in the same symbol |

<div style="page-break-after: always;"></div>

## OFDMA Resource Allocation

![[ofdma-resource-allocation.png | 400]]


The base station does more than just say "user 1 goes now". The base station is solving a resource-allocation problem again and again over time.

It must decide:

- which user gets which subcarriers
- how much transmit power to place on those subcarriers
- how to satisfy system goals such as throughput and QoS

The slides highlight these scheduling inputs:

- **channel gain**: a measure of how well the channel carries the signal from transmitter to receiver. **high channel gain** = the signal gets through well. if user `1` has higher channel gain than user `2` on some subcarrier, that usually means user `1` can use that subcarrier more efficiently.

- **QoS** requirements such as rate, dropping rate, etc.


And these goals:

- maximize throughput
- keep total transmit power below the allowed maximum
- assign each subcarrier exclusively
- guarantee QoS when needed

> [!important] midterm question btw
> given a paragraph, turn it into a math equation of one of the goals above




<div style="page-break-after: always;"></div>



At the MAC level, OFDMA is cool because it gives the scheduler much more freedom.

Advantages of OFDMA:

- resource-allocation flexibility
- adaptation to channel characteristics in adaptive schemes
- better BER performance in adaptive schemes
- multiple users can be served simultaneously in one OFDM symbol

Disadvantages of OFDMA:

- resource allocation becomes more complicated
- adaptive operation increases signaling overhead
- the base station needs up-to-date channel information to make good decisions

tl;dr:
- **OFDMA is smarter**
- but the price is **more scheduling complexity**

> [!Note]
> A lot of OFDMA's gain comes from making good scheduling decisions. If the scheduler is bad or the channel information is outdated, some of the advantage is lost.

<div style="page-break-after: always;"></div>

## Space Diversity

![[space-diversity.png | 500]]

Another way to fight fading is **space diversity**.

The idea is simple:

- use two receiving antennas separated by several wavelengths
- the two antennas will usually not experience deep fades at exactly the same time
- or they will not experience the same amount of fade

if one antenna sees a bad signal right now, the other one may still see a decent signal.

This gives the receiver options:

- choose the better antenna
- switch between antennas
- or combine both signals

TALEB DO U HAVE GAMING ROUTER TALEB THE 8 WINGED GAMING ROUTER TALEB ARE U PRO GAMER TALEB
