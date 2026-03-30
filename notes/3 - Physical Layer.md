
First OSI layer:
Foundation on which other layers build

* Properties of wires, fiber, wireless limit what the network can do. Other limitations include 1. Fourier analysis 2. Bandwidth-limited signals 3. Maximum data rate of a channel

* Modulation: Key problem is to send (digital) bits using only (analog) signals



# Physical Layer Notes

## Fourier Series Representation

The physical layer utilizes Fourier series to represent signals. The general representation of a function $f(x)$ using a Fourier series is:

- $f(x)=a_{0}+\sum_{n=1}^{N}[a_{n}\cos(\frac{n\pi}{L}x)+b_{n}\sin(\frac{n\pi}{L}x)]$
    

When the period $P=2L$, the coefficients are calculated as follows:

- $a_{n}=(\frac{1}{L})\int_{-L}^{L}f(x)\cos(\frac{n\pi}{L}x)dx$
    
- $b_{n}=\frac{1}{L}\int_{-L}^{L}f(x)\sin(\frac{n\pi}{L}x)dx$
    

### Example 1: Square Wave Function

For a specific alternating function where $L=\pi$:

- **Finding $a_0$**: $a_{0}=\frac{1}{2\pi}\int_{-\pi}^{\pi}f(x)dx=\frac{1}{2\pi}[\int_{-\pi}^{0}(-c)dx+\int_{0}^{\pi}c~dx]=0$
    
- **Finding $b_1$**: $b_{1}=\frac{1}{\pi}\int_{-\pi}^{\pi}f(x)\sin(\frac{\pi}{\pi}x)dx$. This evaluates to $\frac{4c}{\pi}$.
    
- **Finding $b_2$**: Even harmonics calculate to 0.
    
- **Finding $b_3$**: Evaluates to $\frac{4C}{3\pi}$.
    
- **Resulting Series**: $f(x)=\frac{4c}{\pi}\sin(x)+\frac{4c}{3\pi}\sin(3x)+\frac{4c}{5\pi}\sin(5x)+\frac{4c}{7\pi}\sin(7x)\dots$
    

### Example 2: 8-bit ASCII "b"

Sending the 8-bit ASCII character "b" translates to the binary signal **01100010**.

- The period $P=T=8$.
    
- **Finding $a_0$**: $a_{0}=\frac{1}{P}\int_{0}^{T}g(t)dt=\frac{1}{8}\int_{1}^{3}1dt+\int_{6}^{7}1dt$. This equals $\frac{3}{8}$.
    
- **Root Mean Square Amplitude**: The value $\sqrt{a_{n}^{2}+b_{n}^{2}}$ is critical because its square is proportional to the energy transmitted at that specific frequency.
    
- **Signal Approximation**: Adding more harmonics (e.g., 1, 2, 4, 8) creates successive approximations that get closer to the original square binary signal.
    

---

## Data Rate and Channel Harmonics

Signals can generally be classified as either baseband or passband signals.

- Given a data rate of **b bits/sec**, the time required to send 8 bits is $8/b$ seconds.
    
- The frequency of the first harmonic (minimum) is $b/8$ Hz.
    
- A voice-graded line has a bandwidth of 3000 Hz (3 kHz).
    
- The maximum number of harmonics that can be sent through is calculated by dividing 3000 Hz by the first harmonic.
    

### Data Rate vs. Harmonics Table

|**Bps**|**T (msec)**|**First harmonic (Hz)**|**# Harmonics sent**|
|---|---|---|---|
|**300**|26.67|37.5|80|
|**600**|13.33|75|40|
|**1200**|6.67|150|20|
|**2400**|3.33|300|10|
|**4800**|1.67|600|5|
|**9600**|0.83|1200|2|
|**19200**|0.42|2400|1|
|**38400**|0.21|4800|0|
|||||

---

## Channel Capacity Theorems

### Nyquist Capacity (1924, AT&T)

Defines the maximum data rate for a **noiseless** channel.

- **Formula**: Maximum data rate $= 2B \log_{2}(V)$ bits/sec.
    
- **Variables**: $V$ represents the number of levels in a signal.
    
- **Example**: Over a noiseless channel with a 3 kHz bandwidth using a binary (2-level) signal, the maximum data rate is 6000 bps.
    

### Shannon Capacity (1948)

Defines the maximum data rate for a **noisy** channel.

- **Formula**: Capacity $= B \log_{2}(1+\text{SNR})$.
    
- **Signal-to-Noise Ratio (SNR)**: Measured in decibels (dB), calculated as $10 \log_{10}(\text{SNR})$.
    
- **Example**: An ADSL line with a bandwidth of 1 MHz and an SNR of 40 dB (where SNR = 10000) has a line capacity of $(10^6) \log_{2}(1+10000) = 13$ Mbps.
    

---

Would you like me to clarify any of the mathematical breakdowns for the Fourier series, or adjust the Markdown formatting to match a specific Obsidian theme or structure you use?