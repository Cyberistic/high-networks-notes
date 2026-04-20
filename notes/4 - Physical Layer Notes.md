
## Fourier Series Representation

![[fourier.png | 200]] ![[fourier2.png | 200]]
The Fourier series is used to represent signals in the physical layer. The general representation of a function $f(x)$ is defined as:

- $f(x)=a_{0}+\sum_{n=1}^{N}[a_{n}\cos(\frac{n\pi}{L}x)+b_{n}\sin(\frac{n\pi}{L}x)]$

When the period is $P=2L$, the coefficients are calculated as follows:

- $a_{0}=\frac{1}{2L}\int_{-L}^{L}f(x)dx$
- $a_{n}=(\frac{1}{L})\int_{-L}^{L}f(x)\cos(\frac{n\pi}{L}x)dx$
- $b_{n}=\frac{1}{L}\int_{-L}^{L}f(x)\sin(\frac{n\pi}{L}x)dx$

<div style="page-break-after: always;"></div>


## Square Wave Function and Fourier Approximation



### Example 1: Square Wave Function

**Problem:** Find the Fourier series coefficients for a square wave function with period $P=2\pi$ (where $L=\pi$).

![[square waves.png | 200]]
![[negcos.png | 200]]
**Answer:**

**Finding $a_1$:**

$$\begin{align}
a_{1} &= \frac{1}{\pi}\int_{-\pi}^{\pi}f(x)\cos(x)dx 
&= \frac{1}{\pi}\left[\int_{-\pi}^{0}(-c)\cos(x)dx+\int_{0}^{\pi}c\cos(x)dx\right] \quad \text{(Split intervals)} 
&= \frac{1}{\pi}\left[-c\int_{-\pi}^{0}\cos(x)dx+c\int_{0}^{\pi}\cos(x)dx\right] \quad \text{(Factor constants)} 
&= \frac{1}{\pi}\left[-c[\sin(x)]_{-\pi}^{0}+c[\sin(x)]_{0}^{\pi}\right] \quad \text{(Integrate)} 
&= \frac{1}{\pi}[-c(0-0) + c(0-0)] \quad \text{(Evaluate)} 
&= 0
\end{align}$$

> [!note] **Result:** $a_1 = 0$ (All $a_n$ coefficients are 0 due to odd symmetry)



**Finding $b_1$:**

$$\begin{align}
b_{1} &= \frac{1}{\pi}\int_{-\pi}^{\pi}f(x)\sin(x)dx 
&= \frac{1}{\pi}\left[\int_{-\pi}^{0}(-c)\sin(x)dx+\int_{0}^{\pi}c\sin(x)dx\right] \quad \text{(Split intervals)} 
&= \frac{1}{\pi}\left[(-c)[-\cos(x)]_{-\pi}^{0}+c[-\cos(x)]_{0}^{\pi}\right] \quad \text{(Integrate $\sin(x)$)} 
&= \frac{1}{\pi}\left[c[\cos(x)]_{-\pi}^{0}-c[\cos(x)]_{0}^{\pi}\right] 
&= \frac{1}{\pi}\left[c(1-(-1)) - c(-1-1)\right] \quad \text{(Evaluate)} 
&= \frac{1}{\pi}[2c + 2c] 
&= \frac{4c}{\pi}
\end{align}$$

> [!note] **Result:** $b_1 = \frac{4c}{\pi}$


<div style="page-break-after: always;"></div>

**Finding $b_2$:**

$$\begin{align}
b_{2} &= \frac{1}{\pi}\left[\int_{-\pi}^{0}(-c)\sin(2x)dx+\int_{0}^{\pi}c\sin(2x)dx\right] 
&= \frac{1}{\pi}\left[(-c)\left(-\frac{1}{2}\right)[\cos(2x)]_{-\pi}^{0}+c\left(-\frac{1}{2}\right)[\cos(2x)]_{0}^{\pi}\right] \quad \text{(Integrate)} 
&= \frac{1}{2\pi}\left[c[\cos(2x)]_{-\pi}^{0}-c[\cos(2x)]_{0}^{\pi}\right] 
&= \frac{1}{2\pi}\left[c(1-1) - c(1-1)\right] \quad \text{(Evaluate: $\cos(0)=\cos(\pm 2\pi)=1$)} 
&= \frac{1}{2\pi}[0 - 0] 
&= 0
\end{align}$$

> [!note] **Result:** $b_2 = 0$ (All even harmonics are 0)

![[even-harmm.png | 200]]


**Finding $b_3$:**

$$\begin{align}
b_{3} &= \frac{1}{\pi}\left[\int_{-\pi}^{0}(-c)\sin(3x)dx+\int_{0}^{\pi}(c)\sin(3x)dx\right] 
&= \frac{1}{\pi}\left[(-c)\left(-\frac{1}{3}\right)[\cos(3x)]_{-\pi}^{0}+c\left(-\frac{1}{3}\right)[\cos(3x)]_{0}^{\pi}\right] \quad \text{(Integrate)} 
&= \frac{1}{3\pi}\left[c[\cos(3x)]_{-\pi}^{0}-c[\cos(3x)]_{0}^{\pi}\right] 
&= \frac{1}{3\pi}\left[c(1-(-1)) - c(-1-1)\right] \quad \text{(Evaluate: $\cos(0)=1, \cos(\pm 3\pi)=-1$)} 
&= \frac{1}{3\pi}[2c + 2c] 
&= \frac{4c}{3\pi}
\end{align}$$

> [!note] **Result:** $b_3 = \frac{4c}{3\pi}$

**Pattern:** Even harmonics $b_4, b_6, b_8$, etc., evaluate to $0$.

**Resulting Series:**
$$f(x)=\frac{4c}{\pi}\sin(x)+\frac{4c}{3\pi}\sin(3x)+\frac{4c}{5\pi}\sin(5x)+\frac{4c}{7\pi}\sin(7x)+\dots$$
    

<div style="page-break-after: always;"></div>

### Example 2: 8-bit ASCII "b"

**Problem:** Find the Fourier series representation of the 8-bit ASCII character "b" which translates to the binary signal **01100010**.

**Signal Waveform:**

```
Bit:    0   1   2   3   4   5   6   7
        0   1   1   0   0   0   1   0
        
            _______         ___
           |       |       |   |
   1       |       |       |   |
           |       |       |   |
   0_______|       |_______|   |_______
       0   1   2   3   4   5   6   7   8
                           Time →
```

**Answer:**

**Given:**
- The period is $P=T=8$.

**Finding $a_0$:**

$$\begin{align}
a_{0} &= \frac{1}{P}\int_{0}^{T}g(t)dt 
&= \frac{1}{8}\left[\int_{1}^{3}1dt+\int_{6}^{7}1dt\right] 
&= \frac{1}{8}(2+1) 
&= \frac{3}{8}
\end{align}$$

**Finding $a_n$:**

$$\begin{align}
a_n &= \frac{2}{P}\int_{0}^{T}g(t)\cos\left(\frac{2\pi nt}{P}\right)dt 
&= \frac{2}{8}\left[\int_{1}^{3}\cos\left(\frac{\pi nt}{4}\right)dt+\int_{6}^{7}\cos\left(\frac{\pi nt}{4}\right)dt\right] 
&= \frac{1}{4}\cdot\frac{4}{\pi n}\left[\sin\left(\frac{3\pi n}{4}\right)-\sin\left(\frac{\pi n}{4}\right)+\sin\left(\frac{7\pi n}{4}\right)-\sin\left(\frac{6\pi n}{4}\right)\right]
\end{align}$$

**Finding $b_n$:**
$$b_n = \frac{1}{\pi n}\left[\cos\left(\frac{\pi n}{4}\right)-\cos\left(\frac{3\pi n}{4}\right)+\cos\left(\frac{6\pi n}{4}\right)-\cos\left(\frac{7\pi n}{4}\right)\right]$$


<div style="page-break-after: always;"></div>

## RMS & Harmonics

**Root Mean Square Amplitude:** The value $\sqrt{a_{n}^{2}+b_{n}^{2}}$ is important because its square is proportional to the energy transmitted at the corresponding frequency.

**Signal Approximation:** Adding more harmonics (increasing $n$) makes the plotted series closer to the original signal.

![[harmonics-3.png | 500]]


<div style="page-break-after: always;"></div>

## Signal Transmission Through Channel

```
          Transmitted                  Channel                    Received

              ^                            ^                            ^
              |--------                    |-------                     |--------
              |        |                   |       \                    |        |
              |        |                   |        \                   |        |
--------------+        |---------   ------+         |---------   ------+        |
              |-------> f                  |-------> f                  |-------> f
                     f_s                          f_c                          f_R
```

## Two Types of Signals

### Baseband Signal

```
Amplitude
    |
    |      _______
    |     |       |
    |_____|       |___________
    |
    +-----|-------|------------> Frequency (Hz)
          0      fs
```

*Signal transmitted at original frequency, starting from 0 Hz*

### Passband Signal

```
Amplitude
    |
    |            _______
    |           |       |
    |___________|       |_____
    |
    +-----|-----|-------|----> Frequency (Hz)
          0    fa       fb
```

*Signal shifted to higher frequency band for transmission*


<div style="page-break-after: always;"></div>

## Data Rate and Channel Harmonics

Signals can generally be classified as either baseband signals or passband signals.

**Problem:** Given a data rate of $b$ bits/sec, how many harmonics can be transmitted through a voice-grade line with bandwidth 3000 Hz?

**Answer:**

**Step 1:** Calculate the time to send 8 bits:
$$T = \frac{8}{b} \text{ seconds}$$

**Step 2:** Calculate the frequency of the first harmonic:
$$f_1 = \frac{1}{T} = \frac{b}{8} \text{ Hz}$$

**Step 3:** Calculate the maximum number of harmonics in a 3 kHz bandwidth:
$$\text{Number of harmonics} = \frac{3000}{f_1} = \frac{3000}{b/8} = \frac{24000}{b}$$
    

### Relation Between Data Rate and Harmonics

**How is data rate related to harmonics?**

Given a data rate of $b$ bits/sec, the time required to send 8 bits is:
$$T = \frac{8}{b} \text{ seconds}$$

The frequency of the first harmonic (minimum) is:
$$f_1 = \frac{1}{T} = \frac{b}{8} \text{ Hz}$$

A voice-grade line has a bandwidth of 3000 Hz (3 kHz). This means that the largest number of harmonics that can be sent through is:
$$\text{Max harmonics} = \frac{3000}{f_1} = \frac{3000}{b/8} = \frac{24000}{b}$$

**Example Calculation (300 bps):**

$$\begin{align}
T &= \frac{8}{300} = 26.67 \text{ msec} 
f_1 &= \frac{300}{8} = 37.5 \text{ Hz} 
\text{Max harmonics} &= \frac{3000}{37.5} = 80
\end{align}$$

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


<div style="page-break-after: always;"></div>

## Channel Capacity Theorems

### Nyquist Capacity (1924, AT&T)

Defines the maximum data rate for a **noiseless channel**.

**Formula:**
$$\text{Maximum data rate} = 2B \log_{2}(V) \text{ bits/sec}$$

**Variables:**
- $B$ = bandwidth in Hz
- $V$ = number of discrete levels in the signal

**Problem:** What is the maximum data rate over a noiseless channel with a 3 kHz bandwidth using a binary (two levels) signal?

**Answer:**

$$\begin{align}
\text{Maximum data rate} &= 2B \log_{2}(V) 
&= 2 \times 3000 \times \log_{2}(2) 
&= 6000 \text{ bps}
\end{align}$$
    

### Shannon Capacity (1948)

Defines the maximum data rate for a **noisy channel**.

**Formula:**
$$\text{Maximum data rate} = B \log_{2}(1+\text{SNR}) \text{ bits/sec}$$

**Signal-to-Noise Ratio (SNR):**
- SNR is measured in decibels (dB)
- $\text{SNR}_{\text{dB}} = 10 \log_{10}(\text{SNR})$
- **Example:** An SNR of 1000 equates to $10 \log_{10}(1000) = 30$ dB

**Problem:** What is the line capacity of an ADSL line with a bandwidth of 1 MHz and an SNR of 40 dB?

**Answer:**

**Step 1:** Convert SNR from dB to linear scale:
$$\begin{align}
40 &= 10 \log_{10}(\text{SNR}) 
\text{SNR} &= 10^4 = 10000
\end{align}$$

**Step 2:** Calculate line capacity:
$$\begin{align}
C &= B \log_{2}(1+\text{SNR}) 
&= 10^6 \times \log_{2}(1+10000) 
&= 10^6 \times \log_{2}(10001) 
&\approx 10^6 \times 13.29 
&\approx 13 \text{ Mbps}
\end{align}$$
