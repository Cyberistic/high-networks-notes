
First OSI layer:
Foundation on which other layers build

* Properties of wires, fiber, wireless limit what the network can do. Other limitations include 1. Fourier analysis 2. Bandwidth-limited signals 3. Maximum data rate of a channel

* Modulation: Sending (digital) bits using only (analog) signals




## Fourier Series Representation

The physical layer utilizes Fourier series to represent signals. A time-varying signal can be represented by *harmonics*, which are a series of frequency components.


The general representation of a function $f(x)$ using a Fourier series is:

   $$g(t) = \frac{1}{2}c + \sum_{n=1}^{\infty} a_n \sin(2\pi nft) + \sum_{n=1}^{\infty} b_n \cos(2\pi nft)$$



![[harmonics-1.png | center | 400]]


- **Bandwidth-Limited Signals**: Removing harmonics (having less bandwidth) degrades the quality of the signal.

The more harmonics you have, the better your signal representation will be

![[harmonics-2.png| center | 400]]

    
<div style="page-break-after: always;"></div>
    
- **Nyquist's Theorem (Noiseless Channel)**: Relates the maximum data rate to the bandwidth ($B$) and the number of signal levels ($V$).

Gives the maximum theoretical data rate of a channel when we assume there is **no noise**. In this ideal case, the limit depends on two things: how much bandwidth the channel has, and how many distinct signal levels the receiver can reliably distinguish. More bandwidth allows more symbol changes per second, and more signal levels allow each symbol to carry more bits.

 $$
    \text{Maximum data rate} = 2B \log_{2}(V) \text{ bits/sec}
$$
        
- **Shannon's Theorem (Noisy Channel)**: Relates the maximum data rate to the bandwidth ($B$) and the signal strength ($S$) relative to the noise ($N$).

Gives the maximum theoretical data rate of a channel when **noise is present**, which is the realistic case for actual communication systems. It shows that capacity depends not only on bandwidth, but also on how strong the signal is compared to the background noise. Even if bandwidth is large, heavy noise limits how much information can be transmitted reliably.
    $$
    \text{Maximum data rate} = B \log_{2}\left(1 + \frac{S}{N}\right) \text{ bits/sec}
    $$

> [!Note]
> These are fundamental limits; real systems can only approach them.
>
> $S/N$ is called the **signal-to-noise ratio (SNR)**, and it is commonly measured in **decibels (dB)** on a logarithmic scale. For example, `10 dB` means the signal power is `10x` the noise power, `20 dB` means it is `100x`, and `30 dB` means it is `1000x`.
>
> The logarithmic scale is useful because signal strengths can vary over a very wide range. Every increase of `10 dB` multiplies the signal-to-noise ratio by `10`, so a higher SNR means the signal stands out more clearly from the noise and the channel can support a higher data rate.


<div style="page-break-after: always;"></div>



### Propagation Mechanisms in Wireless Channels

Wireless signals usually reach the receiver through multiple paths instead of one single straight path.

![[propogation.png | 400]]

- **Reflection**: The signal bounces off large surfaces such as walls, the ground, or buildings.
- **Diffraction**: The signal bends around edges and corners when there is an obstacle in the path.
- **Scattering**: The signal spreads in many directions after hitting small objects or rough surfaces.

These effects occur in both indoor and outdoor wireless channels, which is why the receiver may get several delayed copies of the same signal. This can cause fading, interference, and changes in signal strength over time. 

In general, wireless communication works better in an open field because there are fewer obstacles to reflect, diffract, or scatter the signal. Better Line-Of-Sight (LOS) == better signal.


- The disadvantage of 'Wireless Channels' is **Fading**: Channels suffer from both large-scale fading and small-scale fading (due to coherent, incoherent, or partly-coherent summation of multipaths).
    

*Large Scale Fading*: 

Large-scale fading describes the gradual change in the average received signal strength over **large distances**. As the receiver moves farther from the base station, the signal generally becomes weaker because of path loss.

It is also affected by the surrounding environment, such as buildings, hills, trees, and terrain elevation, which can block or weaken the signal. This is why coverage maps show some areas with stronger reception and other areas with weaker reception even within the same cell.

In short, large-scale fading is the long-range variation in signal power caused by **distance** and **shadowing from large objects**.
![[large scale.png | 500]]

*vs small scale:* Small-scale fading refers to rapid, short-distance fluctuations in signal strength caused by multipath interference, where several reflected or delayed versions of the signal add together constructively or destructively, causing multiple signals to occur.

![[smol.png | 500]]


<div style="page-break-after: always;"></div>

### Channel Sounding

Channel sounding is used to measure and characterize an unknown propagation channel. A known test signal is sent by the transmitter, and the receiver observes how the channel changes it. From this, we can estimate the **channel impulse response**, delay spread, and the effect of multipath propagation.


The measured channel depends on several factors:

- **Frequency**: Different frequencies propagate differently and experience different amounts of attenuation.
- **Line-of-sight (LOS) vs non-line-of-sight (NLOS)**: A clear direct path usually gives a stronger and less distorted signal.
- **Environment**: Indoor, outdoor, urban, and open areas all produce different propagation behavior.
- **Transmitter-receiver separation**: Increasing distance generally increases path loss and delay.
- **Human presence**: People can absorb, block, or reflect signals.
- **Floor area**: The size of the space affects how many reflected paths can exist.
- **Extent of clutter**: Furniture, walls, machines, and other objects increase scattering and reflections.
- **Detection threshold**: Weak paths below the receiver threshold may not be detected.

![[sounding.png | 500]]

<div style="page-break-after: always;"></div>

**Skipping all the mumbo-jumbo above:**

Ex: Signal is estimated to be 50 bits:
1. Send more than 50 bits of 1111111...
2. See the result, from it you can infer the strength, noise, etc


The key practical idea is that the channel-sounding setup must be **wide enough in bandwidth** to capture the whole transmitted signal. In other words, the "black box" representing the propagation channel should be wider than the signal bandwidth, otherwise part of the signal will be missed and the measured response will not represent the full channel behavior.

One simple example is to send a known pattern such as **all 1s** and then observe the received waveform. Because the transmitted signal is already known, any spreading, delay, attenuation, or distortion seen at the receiver is caused by the channel itself.

<div style="page-break-after: always;"></div>

### Channel Impulse Response

The **channel impulse response** describes how the channel spreads one transmitted pulse over time because of multipath. Instead of receiving one clean copy of the signal, the receiver gets several delayed copies, each with a different strength.

**tl;dr:** If you send one very short pulse at one instant, you do not receive *one* perfect short pulse back.

**Multipath** means the same transmitted signal reaches the receiver through multiple physical paths, usually because of reflection, diffraction, and scattering.

This is commonly modeled as:

$$
|h(\tau_{ex})|^2 = \sum_{n=1}^{N} |a_n|^2 \, \delta(\tau_{ex} - \tau_n)
$$

Where:

- $|h(\tau_{ex})|^2$ = the channel power profile at excess delay $\tau_{ex}$, i.e. how much received power appears at that delay
- $N$ = total number of detected multipath components
- $a_n$ = amplitude of the $n$-th multipath component
- $|a_n|^2$ = received power of the $n$-th multipath component
- $\tau_n$ = delay of the $n$-th multipath component
- $\tau_{ex}$ = excess delay, meaning how much later a path arrives compared to the first arriving path
- $\delta(\tau_{ex} - \tau_n)$ = impulse located at the delay of that path

> [!caution] Not sure if we're supposed to memorize this formula and apply it.. I don't remember 


So the measured response is a set of spikes in time: each spike represents one path, its horizontal position gives the **delay**, and its height gives the **received power**.

What this is really doing is breaking the received signal into a collection of separate arrivals. Instead of saying "the channel distorted the signal somehow," we describe the channel as a list of paths:

- one path may arrive first and be strong
- another path may arrive a little later after bouncing off a wall
- another may arrive even later and be much weaker

So the equation is not generating the signal from scratch; it is **describing how the channel responds to a very short transmitted pulse**. Once we know that response, we can predict how a longer transmitted signal will be smeared out in time.

**Example:** suppose the receiver detects 3 paths:

- Path 1 arrives at $0$ ns with power $1.0$
- Path 2 arrives at $40$ ns with power $0.5$
- Path 3 arrives at $90$ ns with power $0.2$

Then the channel impulse response would look like 3 spikes: a tall spike at `0 ns`, a smaller spike at `40 ns`, and an even smaller one at `90 ns`. This means one copy of the signal arrives immediately, another delayed copy arrives `40 ns` later, and another weaker copy arrives `90 ns` later.

If the symbol duration is large compared to these delays, the copies may not cause much trouble. But if symbols are very short, these delayed copies can overlap with the next symbol and create **ISI**.

**Inter-Symbol Interference (ISI)** means part of one symbol spills into the time interval of the next symbol. This happens when delayed multipath copies arrive so late that the receiver is still seeing energy from the previous symbol while trying to detect the current one. As a result, the symbols blur together and the receiver makes more errors.

On the plot, paths above the **receiver detection threshold** are considered detectable. The latest significant path above that threshold gives the **maximum excess delay**:

$$
\tau_{max} = \max(\tau_n \text{ of detectable paths})
$$

This matters because a larger $\tau_{max}$ means the channel spreads the signal over a longer time, which increases the chance of **inter-symbol interference (ISI)**.

![[channel impulse.png | 400 ]]
> [!Note]
> In practice, the blue curve is the measured received power versus excess delay. The yellow spikes represent the individual multipath components extracted from that measurement. Anything below the detection threshold is usually ignored because it is too weak to reliably distinguish from noise.


<div style="page-break-after: always;"></div>

### Convolution and Channel Output

> [!caution] Again, any class during month of Ramadan is a blur to me.. not sure how in-depth we went into this

We can use *channel sounding* from above to estimate the channel impulse response $h(t)$.

Once we know the channel impulse response $h(t)$, we can determine the received signal $y(t)$ for any transmitted signal $x(t)$ using **convolution**:

$$
y(t) = \, \int_{-\infty}^{\infty} h(v)x(t-v)\,dv
$$

This equation means the output is found by combining the input signal with the channel response over all time shifts.

- $x(t)$ = transmitted signal
- $h(t)$ = channel impulse response
- $y(t)$ = received signal after passing through the channel
- $v$ = dummy time variable of integration, used to slide across all possible delays while computing the output at time $t$

The main idea is:

1. The channel response $h(t)$ tells us what happens to one very short pulse.
2. A real transmitted signal is made of many signal values over time, not just one pulse.
3. Convolution adds up the contribution of all those delayed pieces to produce the final received signal.

<div style="page-break-after: always;"></div>

Graphically, convolution can be understood as:

1. Flip and shift one signal, usually written as $x(t-v)$.
2. Multiply it by $h(v)$.
3. Integrate the overlap area.
4. The result at that instant is $y(t)$.

So convolution is the mathematical tool that turns the **channel description** into the **actual received waveform**.

**Example:** if the channel has two paths, one arriving immediately and another delayed by a small amount, then each transmitted symbol appears twice at the receiver: one main copy and one delayed weaker copy. The received signal is the sum of these copies, which is exactly what convolution computes.

In wireless communication, this is why multipath causes spreading and possibly ISI: the output is the sum of many delayed versions of the transmitted signal.

> [!important] Fun fact..
> If you know:
>	- the received signal y(t)
>	- the channel impulse response h(t)
> then you can try to recover the transmitted/original signal x(t) using deconvolution
> In communications, this is basically what an *equalizer* does: it tries to undo the channel and recover the original transmitted signal.


<div style="page-break-after: always;"></div>

### Frequency-Selective vs Frequency-Flat Fading



This distinction depends on how the **symbol duration** compares to the **channel delay spread**, or equivalently how the **signal bandwidth** compares to the **channel bandwidth**.

![[fading.png | 500]]

#### Frequency-Selective Fading

If the symbol duration is **very small** compared to the channel spread,

$$
T_s << \tau_{max}
$$



Here, the **channel spread** means the time span over which the channel spreads one transmitted symbol because of multipath delay.

then delayed copies of one symbol extend into later symbols, which causes **time dispersion** and **ISI**.

In frequency terms, this corresponds to the signal bandwidth being larger than the effective channel bandwidth:

$$
B_s >> B_w
$$

This means different frequency components of the signal experience different fading, so the channel does **not** affect the whole signal equally. Some frequency components may be attenuated more than others, which distorts the signal shape.


> [!Note] tl;dr:
> $T_s$ is the time width of one symbol, while $\tau_max$ is how long the channel keeps producing delayed copies of that symbol. If $T_s$ is much smaller than $\tau_{max}$, then one symbol can finish before all of its multipath copies have arrived.
> So what happens is:
>	1. symbol 1 is transmitted
>	2. its first copy arrives
>	3. later copies of symbol 1 are still arriving
>	4. but symbol 2 has already started
> Now the receiver sees:
>	- current symbol energy
>	- leftover delayed energy from the previous symbol
> That overlap is *time dispersion*, and when it interferes with the next symbol it becomes *ISI*. 

#### Frequency-Flat Fading

If the symbol duration is **much larger** than the channel spread,

$$
T_s >> \tau_{max}
$$

then the delayed copies arrive within the same symbol interval, so there is little or no time dispersion and much less ISI.


In frequency terms, this corresponds to the signal bandwidth being much smaller than the effective channel bandwidth:

$$
B_s << B_w
$$

This means the whole signal sees nearly the same channel gain, so the signal may become weaker or stronger, but its overall shape is not distorted much.


> [!Note] tl;dr:
> $T_s$ is the time width of one symbol, while $\tau_{max}$ is how long the channel keeps producing delayed copies of that symbol. If $T_s$ is much larger than $\tau_{max}$, then the delayed copies of one symbol usually arrive before that symbol interval ends.
> So what happens is:
> 	1. symbol 1 is transmitted
> 	2. its first copy arrives
> 	3. the later copies also arrive soon after
> 	4. but they still arrive before symbol 2 starts
> Now the receiver mostly sees energy from only the current symbol.
> That means little or no *time dispersion* into the next symbol, and much less *ISI*.



**Intuition:**

- **Frequency-selective fading** = the channel treats different parts of the signal spectrum differently, so distortion is more severe.
- **Frequency-flat fading** = the channel affects the whole signal almost uniformly, so it mostly changes amplitude/phase without strongly smearing symbols.

<div style="page-break-after: always;"></div>

### Multicarrier Transmission

![[Multicarrier.png | 500]]

Multicarrier transmission is a way to deal with a **frequency-selective channel** by splitting one wideband signal into many narrower sub-signals, each sent on a different carrier.

The problem in the top row of the slide is that when the transmitted signal bandwidth $B_s$ is larger than the channel's relatively flat bandwidth, different parts of the signal spectrum are filtered differently by the channel. As a result, the received signal becomes distorted.

If we transmit only one very narrowband signal, as in the middle row, its bandwidth is small enough that the channel looks almost flat over that small range. That signal experiences much less distortion, but sending data this way alone would give a low data rate.

The multicarrier idea is to combine many such narrowband signals in parallel. Each subcarrier has a small bandwidth, so each one sees an almost flat channel, but together they still occupy the full overall bandwidth and support a high total data rate.

So instead of sending one wide signal that suffers **frequency-selective fading**, we send many narrow signals that each experience approximately **frequency-flat fading**.

This is the basic idea behind systems such as **OFDM**: split the data across many subcarriers so the channel becomes easier to handle and equalization becomes much simpler.

<div style="page-break-after: always;"></div>

### History of Multicarrier Transmission

![[dft.png | 300]]

The idea of sending data over many subchannels in parallel is old and was proposed long before it became common in real systems. The main reason it took time to implement is that multicarrier transmission requires a large number of modulation and demodulation operations, which was too complex and expensive with older hardware.

What made it practical later was the use of the **DFT/FFT**, which allowed many subcarriers to be generated and separated efficiently in digital form. In short, the concept was known early, but practical implementation had to wait until digital signal processing became powerful enough.

tl;dr: ...skill issue?

### What is OFDM?

**OFDM** stands for **Orthogonal Frequency Division Multiplexing**.

It is a multicarrier transmission method that splits one high-rate wideband data stream into many lower-rate **narrowband** sub-streams, then transmits them in parallel on different subcarriers.

Normally, if many carriers are placed too close together, they interfere with each other. OFDM avoids this by making the subcarriers **orthogonal**, which means they are mathematically arranged so that one subcarrier does not interfere with another at the sampling instant used for detection.

> [!Note] We'll go in detail over OFDM in later notes, there is an entire note dedicated to OFDM.

<div style="page-break-after: always;"></div>

### Orthogonality of Subcarriers


![[orthogonality.png | 500]]

In OFDM, the subcarriers overlap in frequency, but they are spaced carefully so that the peak of one subcarrier occurs at the zero crossings of the others. Because of this, the receiver can still separate them even though their spectra overlap.

The key spacing rule is:

$$
\Delta f = \frac{1}{T_{sym}}
$$

where:

- $\Delta f$ = spacing between adjacent subcarriers
- $T_{sym}$ = OFDM symbol duration

This is what gives the subcarriers their orthogonality.

<div style="page-break-after: always;"></div>

### Orthogonal Carrier Spacing


![[carrier spacing.png | 500]]

If the spacing is chosen as $1/T_{sym}$, the carriers can be packed very closely while still remaining separable at the receiver. This gives OFDM high spectral efficiency, because the subcarriers overlap in frequency without causing the same adjacent-channel interference that ordinary closely spaced carriers would cause.

<div style="page-break-after: always;"></div>

### OFDM System Model

![[OFDM.png | 500]]

Ima be honest.. it's a bit too complex for my *timy brain*, I will try my best.......

The basic OFDM transmitter/receiver chain is:

1. **Serial-to-Parallel (S/P)**: Split the input bit stream into many parallel streams.
2. **IDFT / IFFT**: Convert the frequency-domain subcarrier symbols into one time-domain OFDM symbol.
3. **Add Guard / Cyclic Prefix**: Add a guard interval to reduce ISI caused by multipath.
4. **Parallel-to-Serial (P/S) and D/A**: Convert the samples into a continuous-time waveform for transmission.
5. **Channel**: The signal passes through the wireless channel.
6. **A/D and S/P**: Sample the received signal and split it into parallel branches.
7. **Remove Guard**: Remove the cyclic prefix.
8. **DFT / FFT**: Recover the symbols sent on each subcarrier.
9. **Parallel-to-Serial (P/S)**: Recombine the recovered parallel streams into the output data stream.

> [!Note]
> The IFFT/FFT is what makes OFDM practical. Instead of generating and detecting each subcarrier one by one using separate oscillators and filters, we create and recover all subcarriers together using digital signal processing.

    


<div style="page-break-after: always;"></div>

## Digital Modulation and Multiplexing

Modulation schemes dictate how bits are sent as signals, while multiplexing dictates how a channel is shared among multiple users.

### Baseband Transmission

Line codes send symbols that represent one or more bits.

![[baseband.png | 500]]
- **NRZ (Non-Return to Zero)**: The simplest line code where +1V = "1" and -1V = "0".
- **NRZI (Non-Return to Zero Invert)**: Only invert the signal when both stream signal and internal clock is *1*. ignore on 0.
- **Manchester**: XOR clock with stream.
- **Bipolar/AMI**: a type of return-to-zero (RZ) line code, where two nonzero values are used, so that the three values are +, −, and zero. Consecutive 1's alternate between - and +, while 0 stays 0.


<div style="page-break-after: always;"></div>

### **Clock Recovery**: 

![[clock reco.png | 500]]

To properly decode symbols, the receiver must know **where one bit period ends and the next begins**. It often infers this timing from **transitions** in the received waveform. If the signal stays constant for too long, such as a long run of `0000000` or `1111111`, the receiver may lose track of the clock and no longer know exactly where to sample the bits.

So clock-recovery methods try to ensure the signal has enough transitions. The common strategies go from **simplest but least bandwidth-efficient** to **more efficient but more complex**:

- **Manchester coding**: The simplest idea. Every bit contains a built-in transition, so the clock is embedded directly into the signal. This makes timing recovery easy, but it uses about **2x the bandwidth** of the original data signal. (1 for clock, 1 for signal)
- **4B/5B encoding**: Map each 4 data bits into 5 coded bits chosen so that there are never too many consecutive zeros. This is usually used together with **NRZI**, where a `1` causes a transition and a `0` means no transition. In that setting, avoiding long runs of `0`s guarantees enough transitions for clock recovery while using only **1.25x the bandwidth**. It is more efficient than Manchester, but less direct.
- **Scrambler**: XOR the data with a pseudorandom sequence before transmission, and XOR again at the receiver to recover the original data. This does **not require extra bandwidth**, since the bit rate stays the same. However, it does not strictly guarantee transitions; it only makes long runs of `0`s or `1`s **unlikely**- transmitter and receiver both know the same scrambler rule. often this is a fixed linear-feedback shift register (LFSR) or agreed polynomial/seed. Both sides agree to the same seed and generate the random thingy themselves

<div style="page-break-after: always;"></div>

**Example of 4B/5B:**

Suppose the data is:

`0000 0101`

Using the standard 4B/5B table:

- `0000 -> 11110`
- `0101 -> 01011`

So the transmitted coded bits become:

`11110 01011`

Notice what happened: the original data had `8` bits, but the coded version has `10` bits, which is why the bandwidth increases by a factor of `5/4 = 1.25`. By itself, this does not automatically fix flat signal levels. The benefit appears when the coded bits are sent using **NRZI**: long runs of `1`s create many transitions, and 4B/5B prevents long runs of `0`s, so the receiver keeps getting timing information for clock recovery.

For example, the codeword `11110` in **NRZI** means:

- `1` -> transition
- `1` -> transition
- `1` -> transition
- `1` -> transition
- `0` -> no transition

So even though the bit pattern contains several `1`s in a row, the waveform does **not** stay flat. Instead, it keeps changing, which helps the receiver track the clock.

**Example of a bad long run:** if raw data contains `00000000` and it is sent directly with **NRZI**, then every `0` means "no transition," so the waveform stays flat for a long time and the receiver can lose timing. With **4B/5B**, that same data is first mapped into valid codewords such as `11110 11110`, which in NRZI produces many transitions instead of one long flat region.

> [!Note]
> Tradeoff:
> - **Manchester**: easiest clock recovery, worst bandwidth efficiency
> - **4B/5B**: good compromise
> - **Scrambler**: best bandwidth efficiency, but only probabilistically avoids long runs
     

<div style="page-break-after: always;"></div>

### Passband Transmission

Bits are sent in a non-zero frequency range by modulating the amplitude, frequency, or phase of a carrier signal.

![[passband1.png | 500]]

In **baseband** transmission, the bit pattern itself is sent directly as a waveform whose spectrum starts near `0 Hz`. For example, a sequence of bits can be represented by voltage levels that go high and low over time.

So a **baseband signal** is just the original low-frequency data waveform before shifting it to a higher frequency band.

Example:
- on a wire, sending 1 as high voltage and 0 as low voltage
- that is baseband transmission

In **passband** transmission, we first generate a sinusoidal **carrier** at some higher frequency, then modify that carrier so it represents the data. In other words, the bits are not sent as raw pulses near `0 Hz`; instead, they are carried by changes in the carrier's **amplitude, frequency, or phase**.

The **carrier** itself is just a high-frequency sine wave used to carries the information.

By itself, the carrier has no data in it.  
We put data onto it by changing one of its properties:
- amplitude -> ASK
- frequency -> FSK
- phase -> PSK
So instead of sending raw bits directly, we send a waveform like:

$A \cos(2\pi f_c t + \phi)$

where:
- A = amplitude
- $f_c$ = carrier frequency
- $\phi$ = phase

This is useful because many real channels do not carry low-frequency or DC signals well, but they do carry signals efficiently in some band away from `0 Hz`. Radio systems are a clear example: antennas radiate high-frequency electromagnetic waves, not slow DC-like pulses. Similarly, some telephone channels are designed to pass signals only within a certain frequency range, so the data must be shifted into that supported band before transmission.

The main modulation methods are:

- **Amplitude Shift Keying (ASK)**: Change the **amplitude** of the carrier to represent symbols.
- **Frequency Shift Keying (FSK)**: Change the **frequency** of the carrier to represent symbols.
- **Phase Shift Keying (PSK)**: Change the **phase** of the carrier to represent symbols.

So the same bit stream can be represented by changing different properties of the sinusoidal carrier.

<div style="page-break-after: always;"></div>

### Constellation Diagrams

![[passband2.png | 500]]

A **constellation diagram** is a map of the allowed transmitted symbol states. Each point represents one possible amplitude/phase combination that the transmitter is allowed to send during one symbol interval. Basically a fancy image of the different waveform values the transmitter can choose for one symbol in 1 channel 

So it is like:
- a single time slice
- of the signal on one channel
- showing the possible values that could be sent in that slice

For 64-QAM:
- at each symbol time, the transmitter picks one of 64 allowed amplitude/phase values
- that one choice represents 6 bits

Here:
- a symbol is one allowed waveform choice during one time slot
- each point in the diagram corresponds to one such choice
- the point’s position tells you the signal’s amplitude and phase

<div style="page-break-after: always;"></div>

So when we say it shows the "possible symbols" of a modulation scheme, we mean it shows the exact signal states the transmitter can choose from.

- In **BPSK (Binary Phase Shift Keying)**, there are `2` possible symbols, so it carries `1 bit/symbol`.
- In **QPSK (Quadrature Phase Shift Keying)**, there are `4` possible symbols, so it carries `2 bits/symbol`.
- In **16-QAM (16-point Quadrature Amplitude Modulation)**, there are `16` possible symbols, so it carries `4 bits/symbol`.
- In **64-QAM (64-point Quadrature Amplitude Modulation)**, there are `64` possible symbols, so it carries `6 bits/symbol`.

In general, if a modulation has $M$ symbols, then each symbol carries:

$$
\log_2(M) \text{ bits/symbol}
$$

**BPSK** and **QPSK** vary mainly **phase** only, while **QAM** varies both **amplitude and phase**.

The benefit of using more constellation points is that each symbol can carry more bits. The downside is that the points get closer together, so noise can make the receiver confuse one symbol for another more easily.

<div style="page-break-after: always;"></div>

### Gray Coding

![[passband3.png | 450]]

Gray coding is just a smart way to assign bit labels to constellation points.

The rule is simple: **points that are close to each other should have bit labels that differ by only one bit**.


Without Gray coding, a small movement to a nearby point might change several bits at once.

![[gray-coding.png | 500]]

Compare the two images, while the layout of the left, *non-gray-coded* one, makes more sense, neighboring points differ by more than 1 bit sometimes. As such, mistaking a point and its neighbor would result in more than 1 bit of error.

With Gray coding, that same small mistake usually changes only **one bit**.

**Simple example:**

- suppose the correct symbol is labeled `1101`
- noise moves it to a nearby point
- if that nearby point is labeled `1100`, then only the last bit changed

So the receiver made a **symbol mistake**, but only **one bit** was decoded incorrectly.

      

### Multiplexing Techniques

> [!Note]
> We will go over these multiplexing methods in more detail in later notes. For now, the goal is just to understand the main idea of how multiple users can share the same channel.

#### Frequency Division Multiplexing (FDM)

![[fdm1-1.png | 500]]

**FDM** shares one physical channel by assigning different users different **frequency bands**. So several users can transmit at the same time, as long as each one stays in its own part of the spectrum.

The main idea is:

- User 1 gets one frequency band
- User 2 gets another frequency band
- User 3 gets another frequency band

Then these separate bands are combined into one larger overall channel.

So in FDM, users are separated in **frequency**.

<div style="page-break-after: always;"></div>

#### Orthogonal Frequency Division Multiplexing (OFDM)

![[fdm2.png | 500]]

**OFDM** is a more efficient version of FDM (used for 802.11, 4G). Instead of leaving larger gaps between channels, it packs the subcarriers very closely together.

This works because the subcarriers are made **orthogonal**, so even though their spectra overlap, the receiver can still separate them correctly.

So the main idea of OFDM is:

- many tightly packed subcarriers
- overlap in frequency
- still separable because of orthogonality

The basic idea at the receiver is:

- sample the received OFDM symbol over one symbol interval
- use FFT/DFT to project the signal onto each subcarrier
- because the subcarriers are orthogonal, the desired subcarrier adds up strongly while the others cancel at that detection point

This gives better spectral efficiency than ordinary FDM.

<div style="page-break-after: always;"></div>

#### Time Division Multiplexing (TDM)

![[tdm.png | 500]]

**TDM** shares the channel in **time** instead of frequency. Users take turns transmitting according to a fixed schedule.

So rather than giving each user a different frequency band, we give each user a different **time slot**.

Example:

- time slot 1 -> user 1
- time slot 2 -> user 2
- time slot 3 -> user 3
- then repeat

So in TDM, users are separated in **time**.

<div style="page-break-after: always;"></div>

#### Code Division Multiple Access (CDMA)

![[cdma.png | 500]]

**CDMA** shares the channel by giving each user a different **code** instead of a different time slot or frequency band. Used in *3G*.

All users can transmit at the **same time** and over the **same frequency range**, but the receiver separates them using their orthogonal codes.

So in CDMA, users are separated by **code**.

The basic idea is:

- each user multiplies data by its own code
- signals are added together in the channel
- receiver uses the matching code to recover one user's data and cancel the others

We already looked at the CDMA idea in more detail in the separate derivation note, so here this is just the high-level multiplexing picture.
     


<div style="page-break-after: always;"></div>


## Guided Transmission

Dr Awad said these are included as general knowledge. Up to you to figure out how in depth you want to be. This is why I put it at the end of the note. I leave this *mostly* as reference. Go back to the slides if you want lol



## Guided Transmission Media


### Link Terminology

- **Full-duplex link**: Transmission happens in both directions simultaneously. e.g., use different twisted pairs for each direction
    
- **Half-duplex link**: Transmission happens in both directions, but they must take turns. e.g., senders take turns on a wireless channel
    
- **Simplex link**: Transmission occurs in only one fixed direction at all times.

> [!important] In ESP32 terms..
> Full-duplex: *SPI (in general)* or *UART*
> Half-duplex: *i2c*
> Simplex: any single *GPIO pin* 


Guided media have different physical properties that affect network performance and transmission distance.

- **Storage Media**: Physically sending data (e.g., tapes or DVDs) provides an extremely high bandwidth link (e.g., 70 Gbps) but suffers from very poor message delay. (have to literaly ship the disk yourself lol)
    
- **Twisted Pair Wires**: Very common in LANs and telephone lines; the twists help reduce radiated signal interference.
![[twister.png | 300]]

> [!Note] unfun fact: This is the garden variety cable used in most offices, e.g., as gigabit Ethernet cables. It is also the old-fashioned telephone line that reaches into your home. The twists reduce interference because the signal radiated from the wire at one location is largely canceled by the signal from the nearby twist; tighter twisting gives higher quality wires. UTP = unshielded twisted pair. STP = shielded twisted pair: exists to shield the wire from external noise for more demanding uses (higher data rates) but is it more expensive and difficult to work with.

<div style="page-break-after: always;"></div>
    
- **Coaxial Cable**: Provides better shielding and higher bandwidth for longer distances and higher data rates compared to twisted pairs. Commonly used for video, e.g., cable TV, because it needs larger bandwidth.

![[coax.png | 300]]

- **Power Lines**: Convenient to use due to existing infrastructure, but horrible for sending data signals. It is horrible because it carries power signals at the same time and the wiring was not designed for data communications, e.g., it is not tightly twisted like twisted pair, and its electrical properties change as devices that are plugged in turn on and off. But it is convenient because it is already installed and many devices are plugged in to get power, so people are starting to use it.
![[power lines.png | 300]]


<div style="page-break-after: always;"></div>

### Fiber Optic Cables
Deserve their own section because they have tons of slides..

![[fiber1.png | 400]]
- **Fiber Optic Cables**: Carries light in a thin strand of glass via total internal reflection. It has enormous bandwidth (in THz) and tiny signal loss, making it ideal for high rates over long distances.

Examples include the backbone links between ISP facilities, and 'fiber runs to the home' (FTTH) that provide much higher bandwidth home connectivity than ADSL (copper telephone lines) aka Asymmetric Digital Subscriber Line. 



![[fibrosis.png | 400]]

This slide shows why fiber runs for high rates and long distances – attenuation is very low (can go 10km before the signal has lost 3dB or half its power) for enormous regions of bandwidth (30 *Terahertz* when wavelength is converted to frequency).

**Don't forget to eat your fibers**


fiber vs wire:

| Property | Wires | Fiber |
| --- | --- | --- |
| Distance | Short (100s of m) | Long (tens of km) |
| Bandwidth | Moderate | Very High |
| Cost | Inexpensive | Less cheap |
| Convenience | Easy to use | Less easy |
| Security | Easy to tap | Hard to tap |
 

![[fiberberb.png | 300]]

- **Single-mode Fiber**: The core is so narrow (10 μm) that light cannot bounce; used with lasers for long distances (e.g., 100 km).
         
- **Multi-mode Fiber**: Features a wider core (50 μm) where light bounces; used with LEDs for cheaper, shorter-distance links.




<div style="page-break-after: always;"></div>

## Wireless Transmission

![[magnets.png | 500]]

Wireless signals are transmitted through the electromagnetic spectrum, with different bands allocated for different uses (e.g., Radio for wide-area, Microwave for LANs/cellular, Infrared/Light for line-of-sight). Signal propagation mechanisms include reflection, diffraction, and scattering.

![[radio-1.png | 500]]
- **Radio Transmission**: Signals can follow the curvature of the earth (LF/MF), bounce off the ionosphere (HF), and penetrate buildings well.

> [!caution] The path loss makes the signal fall of at least as fast as 1/d^2 due to the RF energy being spread out over a greater region.
> idk what this means tbh ¯\\_(ツ)_/¯ 


![[microwave.png | 500]]
- **Microwave Transmission**: Offers high bandwidth and is widely used for WiFi outdoors and indoors. Signals are attenuated or reflected by everyday objects and are subject to multipath fading.
The variation in signal strength as the sender/receiver move is a key hallmark of wireless. It means that data rates over wireless links can change dramatically; they are not fixed like a wire.

and I thought microwaves were for sandwiches


![[lights.png | 500]]
    
- **Light Transmission**: Highly directional and offers immense bandwidth, utilizing lasers and photodetectors, but requires strict line-of-sight.

> [!important] Fun fact.. some cool tech is in development to send data to the moon or satellites through light/lasers as you get speed of light transfer speed.. issue is it requires continuous LOS so you have to set up multiple stations around the earth and deal with clouds/weather..

<div style="page-break-after: always;"></div>


![[spectrum.png | 500]]
TV, cellular, satellite frequencies are heavily regulated.. cuz of capitalism?

> [!important] Fun fact.. you're on the spectrum bahahah


![[free.png | 500]]
- **ISM Bands**: Unlicensed frequency bands that are free for low-power use, commonly utilized for WiFi, Bluetooth, and Zigbee. 


- These bands are free for use at low power; devices manage interference. Used for WiFi, etc., not for cellular.

> [!important] Fun fact.. your spectrum also ends with ism hahah


<div style="page-break-after: always;"></div>

## Wireless vs Wires

### Wireless:

+Easy and inexpensive to deploy

+Naturally supports mobility

+Naturally supports broadcast

−Transmissions interfere and must be managed

−Signal strengths hence data rates vary greatly

### Wires/Fiber:

+Easy to engineer a fixed data rate over point-to-point links

−Can be expensive to deploy, esp. over distances

−Doesn’t readily support mobility or broadcast

## Communication Satellites

Satellites are effective for broadcast distribution and anywhere/anytime communication. They vary by their orbital altitude:

- **Geostationary (GEO)**: Orbit at 35,000 km. They have a high latency (e.g., 270 ms), and only 3 satellites are needed for global coverage. They communicate with VSATs (Very Small Aperture Terminals) using various GHz bands (L, S, C, Ku, Ka).
    
- **Medium-Earth Orbit (MEO)**: Orbit below the upper Van Allen belt, latency around 35-85 ms. 10 needed for global coverage. *MEO is used for navigation systems such as the GPS (Global Positioning System) rather than data communications.*
    
- **Low-Earth Orbit (LEO)**: Orbit below the lower Van Allen belt. Have very low latency (1-7 ms), but require many satellites (e.g., 50+) for global coverage. Systems like Iridium route communications directly through these satellites.

![[iridium.png | 400]]
Since the satellites are LEO, it does not take long for signals from the Earth to go up and down compared to GEO satellites.

## Satellite vs Fiber

### Satellite:

+Can rapidly set up anywhere/anytime communications (after satellites have been launched)

+Can broadcast to large regions

−Limited bandwidth and interference to manage

### Fiber:

+Enormous bandwidth over long distances

−Installation can be more expensive/difficult

<div style="page-break-after: always;"></div>

## The Public Switched Telephone Network (PSTN)



![[telephone-system.png | 500]]

The **PSTN** is a hierarchical telephone system originally built for carrying voice calls. Structure of the Telephone System is as follows:

- **Local loops**: the access links from homes to the nearest **end office**, usually old analog twisted-pair telephone lines
- **Trunks**: high-capacity digital links, usually fiber, that carry many calls between offices
- **Switching offices**: offices that connect calls from one trunk to another so the call can reach the destination

Ex: Telephone -> local loop -> end office -> trunks / toll offices / intermediate offices -> end office -> local loop -> telephone


<div style="page-break-after: always;"></div>

### Local Loop (1): Modems

![[local-loop-modems.png | 500]]

The traditional local loop was designed for **voice**, not for high-speed digital data.

Telephone **modems** send digital data over roughly a **3.3 kHz analog voice channel** that interfaces to the **POTS** network.

- **POTS** = **Plain Old Telephone Service**, meaning the traditional analog voice telephone service in the PSTN
- the modem converts digital computer bits into an analog waveform that can pass through the voice channel
- local-loop rates were typically **less than 56 kbps**, which is why dial-up Internet was slow (as if we have better rates now lol)

The big limitation was not the whole telephone network, but the old analog local loop and its narrow voice-band channel.

<div style="page-break-after: always;"></div>

### Local Loop (2): Digital Subscriber Lines (DSL)

![[local-loop-dsl.png | 400]]

**DSL** improves the local loop by sending data over the same old telephone line using **frequencies that ordinary POTS voice service does not use**.


- the same twisted pair can carry both **voice** and **data** at the same time
- **splitters** separate the low-frequency voice part from the higher-frequency data part
- at the telephone company side, a **DSLAM** (Digital Subscriber Line Access Multiplexer) collects many DSL lines and connects them toward the ISP/network

Rates vary with line quality and distance, but for **ADSL2** they can reach about **12 Mbps**.

- **ADSL** = **Asymmetric DSL**
- **asymmetric** means **more bandwidth is allocated to downstream than upstream**, because home users usually download more than they upload

For ADSL2, **OFDM** is used up to about **1.1 MHz**, split into many small subchannels. Most of that bandwidth is assigned to **downstream** traffic, with a smaller part used for **upstream**.

> [!Note]
> DSL is clever because it reuses the same old copper telephone line instead of replacing it immediately. Voice stays in the low-frequency part, while Internet data is pushed into higher frequencies.

<div style="page-break-after: always;"></div>

### Local Loop (3): Fiber To The Home (FTTH)

![[local-loop-ftth.png | 500]]

**FTTH** replaces the copper local loop with **fiber optic cable** all the way to the customer, giving much higher data rates.

The idea is:

- fiber runs from the end office toward a neighborhood
- an **optical splitter/combiner** shares the connection among multiple homes
- one wavelength can be used for **downstream** and another for **upstream**
- the fiber plant is often **passive**, meaning there are no powered amplifiers in the distribution path

So compared to DSL, FTTH removes the main bottleneck of the old copper local loop and takes advantage of the huge bandwidth of fiber.

### Trunks and Multiplexing

![[trunks-multiplexing.png | 500]]

**Trunks** are the high-capacity digital links that carry many calls between telephone offices, usually over fiber.

Calls on PSTN trunks are carried digitally using **TDM (Time Division Multiplexing)**.

- one voice call is represented by an **8-bit PCM sample every `125 us`**
- that means `8000` samples/second
- so one call needs `8 x 8000 = 64 kbps`

<div style="page-break-after: always;"></div>

The traditional **T1 carrier** combines **24 call channels** into one digital stream.

- every `125 us`, the system sends one sample from each of the `24` channels
- that gives a frame of `24 x 8 = 192` bits
- plus `1` extra framing bit, for a total of `193` bits per frame
- `193 bits / 125 us = 1.544 Mbps`

The line symbols on a classic T1 are based on **AMI (Alternate Mark Inversion)**.

> [!Note]
> The important idea is that the trunk does not carry one call alone. It carries many separate voice channels by giving each one its own time slot in a repeating frame.
> If all 24 T1 channels are already in use, a new call cannot be given a time slot on that trunk.
So one of these happens:
> - the call is blocked on that trunk
> - the switching system tries another available trunk/route
> - if no route is available, the caller gets a busy signal / call setup fails
> 
> This lays out the foundation for future notes:
> - in circuit switching, capacity is reserved in advance
> - so if all channels are full, you usually cannot “squeeze in” one more call
> - unlike packet switching, the new traffic does not just wait in a queue and share bandwidth dynamically

<div style="page-break-after: always;"></div>

### Switching (1): Circuit vs Packet Switching

![[switching-1.png | 500]]

**Switching offices** connect trunks so communication can reach the correct destination.

- **PSTN** mainly uses **circuit switching**
- the **Internet** mainly uses **packet switching**

**circuit switching**:

- a dedicated end-to-end path is set up when the call is made
- resources along that path are reserved for the whole call
- all data follows that same path in order
- this works well for continuous voice, but unused reserved capacity is wasted

**packet switching**:

- no dedicated physical path is reserved in advance for normal traffic
- packets are treated independently
- routers queue and forward packets as links become available
- delay can vary because of **queueing** and congestion

<div style="page-break-after: always;"></div>

### Switching (2): Setup and Delay

![[switching-2.png | 400]]

Circuit switching requires **connection setup** before the actual data flows smoothly.

- first, the network searches for and reserves a route
- then the call is accepted and data can flowSetu continuously
- after the communication ends, the circuit is torn down

Packet switching works differently:

- there is usually **no setup phase** before sending ordinary packets
- each packet is forwarded separately
- the tradeoff is **variable queueing delay** at routers

Why those delays appear:

- **Propagation delay**: even after a packet is transmitted immediately, it still takes time for the signal to physically travel across the link from one router to the next
- **Queueing delay**: when packets arrive at a router faster than the outgoing link can send them, they must wait in a buffer until earlier packets are transmitted

So the big tradeoff is:

- **circuit switching**: setup delay first, then steady transfer
- **packet switching**: little/no setup, but variable delays during transfer

<div style="page-break-after: always;"></div>

### Circuit vs Packet Switching Table

| Item | Circuit switched | Packet switched |
| --- | --- | --- |
| Call setup | Required | Not needed |
| Dedicated physical path | Yes | No |
| Each packet follows the same route | Yes | No |
| Packets arrive in order | Yes | No |
| Is a switch crash fatal | Yes | No |
| Bandwidth available | Fixed | Dynamic |
| Time of possible congestion | At setup time | On every packet |
| Potentially wasted bandwidth | Yes | No |
| Store-and-forward transmission | No | Yes |
| Charging | Per minute | Per packet |

- **Is a switch crash fatal**:
  In a **circuit-switched** network, if one switch on the dedicated path fails, the call is broken because that exact reserved path was required. In a **packet-switched** network, packets can often be rerouted through other paths, so one router/switch failure is usually not immediately fatal to the whole communication.

- **Store-and-forward transmission**:
  In a **packet-switched** network, a router usually receives a packet, stores it briefly in memory, then forwards it on the next link. This is why queueing can happen. In **circuit switching**, once the circuit is set up, bits flow along the reserved path without each switch needing to store whole packets first.
    


<div style="page-break-after: always;"></div>

## Mobile Telephone System

### Generations of Mobile Telephone Systems

Mobile systems evolved in generations, mainly by changing how voice/data are represented and how the radio channel is shared.

- **1G**: analog voice *only*
  - example: **AMPS** (*Advanced Mobile Phone System*)
  - deployed starting in the **1980s**
  - modulation based on **FM**, similar to analog radio
- **2G**: digital mobile systems, carrying *analog* voice and limited *digital* data
  - example: **GSM** (*Global System for Mobile communications*)
  - deployed starting in the **1990s**
  - modulation based on **QPSK** (to be explained)
- **3G**: *digital* voice and data with higher data capability
  - example: **UMTS** (*Universal Mobile Telecommunications System*)
  - deployed starting in the **2000s**
  - based on **CDMA**
- **4G**: digital data network that also carries voice (voice is now data)
  - example: **LTE** (*Long Term Evolution*)
  - deployed starting in the **2010s**
  - based on **OFDM**

The big trend is that systems moved from mostly analog voice to fully digital data-centric networks.

<div style="page-break-after: always;"></div>

### Cellular Mobile Phone Systems

![[cellular-mobile-systems.png | 400]]

Cellular networks divide the coverage area into spatial regions called **cells**.

The main idea is:

- each mobile communicates with the base station of the cell it is currently in
- when the user moves to another cell, the connection is transferred using a **handoff**
- frequencies are **reused** in non-adjacent cells so the same spectrum can support many users across a large area

To support more users in a dense area, the network can use **smaller cells**.

Why this helps:

- smaller cells mean each base station covers less area
- so the same frequencies can be reused more often
- which increases total system capacity

> [!Note]
> The whole cellular idea is basically a spectrum-reuse trick: instead of one giant transmitter serving everyone, we split the area into many smaller regions and reuse the same frequencies far enough apart.

<div style="page-break-after: always;"></div>

### GSM Architecture

![[gsm-1.png | 500]]

In **GSM**, the mobile device is logically split into:

- the **handset** itself
- the **SIM card** (*Subscriber Identity Module*), which stores subscriber identity/credentials

Location management is important because users move.

- the mobile updates the **HLR** (*Home Location Register*) with information about its current whereabouts for incoming calls
- the local area/network keeps track of visiting users in the **VLR** (*Visitor Location Register*)

The rough path is:

`Mobile -> air interface -> base station / cell tower -> BSC -> MSC -> PSTN/network`

where:

- **BSC** = Base Station Controller
- **MSC** = Mobile Switching Center 
(or our degrees inshallah)

GSM is not just radio transmission. It also includes subscriber identity and location tracking so calls can find the user. Basically advanced tracking lol gg.

<div style="page-break-after: always;"></div>

**GSM uses QPSK, go back to the passband transmission section above, but to recap:**

**QPSK** stands for **Quadrature Phase Shift Keying**. Instead of sending one bit by choosing between only `2` carrier phases, it uses `4` possible phase states. That means one symbol can represent `2` bits instead of `1`.

You can think of it like this: the carrier is still the same sinusoidal wave, but at each symbol time the transmitter is allowed to rotate its phase to one of `4` allowed positions.

Example mapping:

- `00 -> 45°`
- `01 -> 135°`
- `11 -> 225°`
- `10 -> 315°`

So if the next bits are `11`, the transmitter sends the carrier with the phase assigned to `11`. If the next bits are `00`, it sends the phase assigned to `00`.

The receiver looks at the phase of the received symbol, decides which of the `4` phase states it is closest to, and from that recovers the `2` bits.

**QPSK carries twice as many bits per symbol as binary phase signaling**, which improves spectral efficiency.

<div style="page-break-after: always;"></div>

### GSM Air Interface

![[gsm-2.png | 500]]

The GSM air interface combines **FDM** and **TDM**.

- the spectrum is divided into **200 kHz frequency channels** using **FDM**
- each frequency channel is further divided into an **8-slot TDM frame** every **4.615 ms**
- each mobile is assigned uplink and downlink time slots to use
- each slot is **148 bits** long, giving a rate of about **27.4 kbps**

We do this to let many mobiles share the same limited radio spectrum in an organized way, instead of giving every user a completely separate dedicated frequency all the time.

So GSM shares the radio channel in two dimensions:

- by **frequency** first
- then by **time slots** within each frequency channel

