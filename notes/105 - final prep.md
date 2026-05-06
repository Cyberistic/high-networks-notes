
The final exam follows the same format and questions in [[102 - midterm prep]], and they are expected to come. Main difference is the inclusion of the *Propagation models* slide-set.

This note will cover: 
1. Questions of SDN in [[13 - SDN]], since it came in the midterm exam
2. Detailed propagation model questions, with their note in [[5 - Propagation models]]

3. We __try__ to include all equations mentioned in the course at the end (hopefully we don't forget any)


<div style="page-break-after: always;"></div>


# SDN (short questions)

These are based mainly on [[13 - SDN]] and the SDN question recalled in [[104 - midterm revision#F) SDN:]].



## SDN Multiple Choice Questions

1. What does SDN stand for?
   A. Switched Data Nodes
   B. Software-Defined Networking
   C. Simple Distributed Network
   D. Secure Dynamic Networking
   **Answer: B**

2. What is the main idea of SDN?
   A. Combine modulation and routing in one device
   B. Separate the control plane from the data plane
   C. Remove switches from the network
   D. Replace IP with Ethernet
   **Answer: B**

3. In SDN, which part mainly decides where traffic should go?
   A. Data plane
   B. Controller / control plane
   C. Physical layer only
   D. Modem
   **Answer: B**

4. In SDN, switches mainly act as:
   A. Controllers
   B. Forwarding devices in the data plane
   C. DNS servers
   D. Compilers
   **Answer: B**

5. Which protocol/message is commonly mentioned for controller-to-switch communication in SDN?
   A. FTP
   B. ARP
   C. OpenFlow
   D. Erlang
   **Answer: C**


<div style="page-break-after: always;"></div>


6. Which of the following is an advantage of SDN?
   A. Harder automation
   B. More manual per-device configuration
   C. Programmability
   D. No controller required
   **Answer: C**

7. Which tool is commonly used to emulate an SDN network?
   A. Mininet
   B. Wireshark
   C. MATLAB only
   D. DHCP
   **Answer: A**

8. Which of the following can act as an SDN controller?
   A. Ryu
   B. ONOS
   C. Both A and B
   D. Neither A nor B
   **Answer: C**

## SDN True / False

1. SDN stands for Software-Defined Networking. — **True**
2. In SDN, the control plane and data plane are always embedded together inside each switch. — **False** (SDN separates the control plane from the data plane)
3. In traditional networking, each router or switch usually makes forwarding decisions locally. — **True**
4. OpenFlow is associated with communication between the SDN controller and switches. — **True**
5. One advantage of SDN is improved programmability. — **True**
6. SDN makes network-wide traffic management easier because the controller has a broader view of the network. — **True**
7. Mininet is an SDN controller. — **False** (Mininet is a network emulator, not the controller itself)
8. Ryu and ONOS are examples of SDN controllers. — **True**
9. SDN can help reduce operational cost by automating tasks. — **True**
10. In SDN, the data plane mainly forwards packets according to rules installed by the controller. — **True**



<div style="page-break-after: always;"></div>


# Propagation Models

## Most probable math questions:

sorted by likeliness (I made it up):
1. Last question in the note: [[5 - Propagation models#Example Composite Probability of Service Calculating Fade Margin for Link Budget]]
	- Find Composite Median Loss
	- Find Composite Standard Deviation
	- Find Fade Margin for $75\%$ Service

2. Given one of the model's formulas, sub in values
3. From the graph calculate median standard deviation at X%
4. The [[5 - Propagation models#Log Distance Path Loss Model]] question, sub in values
5. $\lambda = \frac{c}{f}$ formula from [[5 - Propagation models#Frequency and Wavelength Implications]]



## Propagation Models Multiple Choice Questions

1. Which propagation effect means the signal amplitude becomes smaller during propagation?
   A. Scattering
   B. Attenuation
   C. Diffraction
   D. Diversity
   **Answer: B**

2. In multipath propagation, the receiver may get copies of the same signal with different:
   A. Temperatures, voltages, and bandwidths
   B. Times, amplitudes, and phases
   C. Gains, wavelengths, and carrier types
   D. Codes, routes, and ports
   **Answer: B**

3. What is the wavelength formula used in the note?
   A. $\lambda = cf$
   B. $\lambda = \frac{f}{c}$
   C. $\lambda = \frac{c}{f}$
   D. $\lambda = \frac{1}{cf}$
   **Answer: C**

4. At a higher carrier frequency, the wavelength is generally:
   A. Longer
   B. Shorter
   C. Unchanged
   D. Infinite
   **Answer: B**

5. Rayleigh fading is commonly used when:
   A. One strong LOS path dominates
   B. Many multipath components combine without one dominant LOS path
   C. The antenna height is zero
   D. Only attenuation exists
   **Answer: B**

6. Why is space diversity classically more practical at the base station than at the handset?
   A. Base stations have room for well-separated antennas
   B. Handsets never experience fading
   C. Base stations do not use RF
   D. Handsets have larger wavelengths
   **Answer: A**

7. Which type of propagation model is mainly used for early system dimensioning and estimating cell counts?
   A. Point-to-point models
   B. General area models
   C. Knife-edge models only
   D. Local variability models only
   **Answer: B**

8. In area models, the predicted curve is best described as:
   A. The exact signal on every street
   B. A smooth average trend
   C. A worst-case obstruction path
   D. A near-field pattern
   **Answer: B**

9. In the log-distance path loss model, the extra loss due to increased distance in dB is:
   A. $10n\log(d/d_0)$
   B. $n/d_0$
   C. $P_t - P_r$
   D. $\sigma^2 d$
   **Answer: A**

10. In the log-distance model, $d_0$ is:
   A. The maximum cell radius
   B. The close-in reference distance
   C. The shadowing variance
   D. The rooftop diffraction term
   **Answer: B**

11. Why should the reference distance $d_0$ be chosen in the far field?
   A. To maximize transmitted power
   B. To avoid near-field effects
   C. To force $n=2$
   D. To eliminate shadowing
   **Answer: B**


<div style="page-break-after: always;"></div>


11. In the log-normal shadowing model, $X_\sigma$ represents:
   A. Base-station height
   B. Random variation due to shadowing/clutter
   C. The free-space wavelength
   D. The reference distance
   **Answer: B**


13. The Hata model is mainly:
   A. A fully ray-tracing model
   B. A simplified empirical formula derived from Okumura
   C. A fading distribution
   D. A transport-layer model
   **Answer: B**

14. The COST-231 model mainly extends Hata to:
   A. Lower antenna heights only
   B. Higher frequencies around $1500-2000\ \text{MHz}$
   C. Satellite frequencies
   D. Optical fiber systems
   **Answer: B**

15. Which pair appears as extra site-specific correction terms in the MSI Planet model?
   A. Clutter and street orientation
   B. TCP and UDP
   C. Queueing delay and throughput
   D. Fading margin and BER only
   **Answer: A**

16. The Walfisch-Betroni / Walfisch-Ikegami path loss expression is:
   A. $L = L_{FS} + L_{RT} + L_{MS}$
   B. $L = L_{FS} - L_{RT} - L_{MS}$
   C. $L = A + B\log R$
   D. $L = L_{COST} + X_\sigma$
   **Answer: A**

17. For a cell with about 90% overall location probability, the typical probability of service at the cell edge is about:
   A. 50%
   B. 60%
   C. 75%
   D. 100%
   **Answer: C**


<div style="page-break-after: always;"></div>


18. Which expression gives the composite standard deviation?
   A. $\sigma_{composite} = \sigma_{outdoor} + \sigma_{penetration}$
   B. $\sigma_{composite} = \sigma_{outdoor} - \sigma_{penetration}$
   C. $\sigma_{composite} = \sqrt{\sigma_{outdoor}^2 + \sigma_{penetration}^2}$
   D. $\sigma_{composite} = \sigma_{outdoor}\sigma_{penetration}$
   **Answer: C**

19. With $\sigma_{outdoor}=8\ \text{dB}$ and $\sigma_{penetration}=8\ \text{dB}$, the required fade margin for 75% service is approximately:
   A. $5.4\ \text{dB}$
   B. $7.63\ \text{dB}$
   C. $8\ \text{dB}$
   D. $11.31\ \text{dB}$
   **Answer: B**

## Propagation Models True / False

1. Attenuation is often the single most important factor in propagation. — **True**
2. Time variability can happen because users or objects move. — **True**
3. In the note, larger frequency means larger wavelength. — **False** (from $\lambda = c/f$, higher frequency means shorter wavelength)
4. Rayleigh fading refers to fast local fluctuations around the large-scale average signal level. — **True**
5. Good decorrelation for classical space diversity is typically achieved with spacing of about $10\lambda$ to $20\lambda$. — **True**
6. Transmitting the same signal from two antennas automatically creates receive diversity at a given observation point. — **False** (the transmitted waves still combine into one resulting signal at that point)
7. General area models are mainly based on measured data over an area. — **True**
8. Point-to-point models are mainly used for detailed specific-link analysis. — **True**
9. In the log-distance model, a larger path loss exponent $n$ means the signal decays more slowly with distance. — **False** (larger $n$ means path loss increases faster with distance)
10. The reference distance $d_0$ should be chosen in the near field. — **False** (it should be in the far field to avoid near-field effects)
11. In log-normal shadowing, two receivers at the same distance can still experience different path losses. — **True**
12. The Hata model is a simplified empirical formula derived from Okumura. — **True**
13. COST-231 is mainly intended for frequencies below $1\ \text{GHz}$. — **False** (it extends Hata to about $1500-2000\ \text{MHz}$)
14. In the Okumura model, a larger $G_{area}$ generally reduces predicted path loss because it is subtracted. — **True**
15. Morphological zones describe land use and building density, which affect propagation corrections. — **True**
16. The MSI Planet model includes correction factors for clutter and street orientation. — **True**
17. Walfisch-type models are especially aimed at built-up urban areas where rooftop diffraction and street reflections matter. — **True**
18. Designing exactly on the median curve already guarantees better-than-50% reliability. — **False** (the median curve is roughly the 50% level)
19. Median outdoor loss and median penetration loss add directly when forming composite median loss. — **True**
20. Composite standard deviation is found by directly adding the two standard deviations. — **False** (the note uses root-sum-square)



<div style="page-break-after: always;"></div>


# All Course Formulas

1. **Probability Mass Function (PMF)** — [[2 - Review]]:
$$P_X(x) = \text{Prob}(X=x)$$

2. **Cumulative Distribution Function (CDF)** — [[2 - Review]]:
$$P_X(x) = \text{Prob}(X \le x)$$

3. **Expectation (Mean) — discrete** — [[2 - Review]]:
$$E(X) = \sum_{i} x_i \cdot P_X(x_i)$$

4. **Variance** — [[2 - Review]]:
$$\text{Var}(X) = \sigma_x^2 = E(X^2) - (E(X))^2$$

5. **Standard Deviation** — [[2 - Review]]:
$$\text{Std}(X) = \sigma_x = \sqrt{\sigma_x^2}$$

6. **CDF complement** — [[2 - Review]]:
$$P(X > x) = 1 - P_X(x)$$

7. **CDF interval** — [[2 - Review]]:
$$P(a \le X \le b) = P_X(b) - P_X(a)$$

8. **Expectation — continuous** — [[2 - Review]]:
$$E(X) = \int_{-\infty}^{\infty} x \cdot P_X(x) dx$$

9. **Variance — continuous** — [[2 - Review]]:
$$\text{Var}(X) = \int_{-\infty}^{\infty} x^2 P_X(x) dx - \left(\int_{-\infty}^{\infty} x P_X(x) dx\right)^2$$

10. **Product Rule (Conditional Probability)** — [[2 - Review]]:
$$P(A|B) = \frac{P(A,B)}{P(B)} \Rightarrow P(A,B) = P(A|B) \cdot P(B)$$

11. **Bayes' Rule** — [[2 - Review]]:
$$P(A|B) = \frac{P(B|A)P(A)}{P(B)}$$

12. **Conditional Expectation** — [[2 - Review]]:
$$E[X] = E[X|A]P(A) + E[X|B]P(B)$$


<div style="page-break-after: always;"></div>


13. **Exponential PDF** — [[2 - Review]]:
$$f_X(x) = \mu e^{-\mu x} \quad (x \ge 0)$$
where $\mu$ = rate parameter

14. **Exponential CDF** — [[2 - Review]]:
$$F_X(x) = 1 - e^{-\mu x} \quad (x \ge 0)$$

15. **Exponential Mean** — [[2 - Review]]:
$$E[X] = \frac{1}{\mu}$$

16. **Exponential Variance** — [[2 - Review]]:
$$\text{Var}(X) = \frac{1}{\mu^2}$$

17. **Memoryless Property** — [[2 - Review]]:
$$P(X > x+t \| X > t) = P(X > x)$$

18. **Poisson PMF** — [[2 - Review]]:
$$P(X=k) = e^{-\lambda} \frac{\lambda^k}{k!}$$
where $\lambda$ = average rate, $k$ = number of events

19. **Poisson Mean & Variance** — [[2 - Review]]:
$$E[X] = \text{Var}(X) = \lambda$$

20. **Poisson → Exponential** — [[2 - Review]]:
$$P(T \le s) = 1 - e^{-\lambda s}$$
where $T$ = inter-arrival time

21. **Fourier Series** (useless?) — [[3 - Physical Layer]]:
$$g(t) = \frac{1}{2}c + \sum_{n=1}^{\infty} a_n \sin(2\pi nft) + \sum_{n=1}^{\infty} b_n \cos(2\pi nft)$$

22. **Nyquist Capacity (noiseless)** — [[3 - Physical Layer]], [[4 - Physical Layer Notes]]:
$$\text{Maximum data rate} = 2B \log_{2}(V) \text{ bits/sec}$$
where $B$ = bandwidth, $V$ = signal levels

23. **Shannon Capacity (noisy)** — [[3 - Physical Layer]], [[4 - Physical Layer Notes]]:
$$\text{Maximum data rate} = B \log_{2}\left(1 + \frac{S}{N}\right) \text{ bits/sec}$$
where $B$ = bandwidth, $S/N$ = signal-to-noise ratio


<div style="page-break-after: always;"></div>


24. **Channel Impulse Response** (useless?) — [[3 - Physical Layer]]:
$$\|h(\tau_{ex})\|^2 = \sum_{n=1}^{N} \|a_n\|^2 \, \delta(\tau_{ex} - \tau_n)$$

25. **Maximum Excess Delay** (useless?) — [[3 - Physical Layer]]:
$$\tau_{max} = \max(\tau_n \text{ of detectable paths})$$

26. **Convolution** (useless?) — [[3 - Physical Layer]]:
$$y(t) = \int_{-\infty}^{\infty} h(v)x(t-v)\,dv$$

27. **Frequency-Selective Fading** — [[3 - Physical Layer]]:
$$T_s << \tau_{max}, \quad B_s >> B_w$$
where $T_s$ = symbol duration, $B_s$ = signal bandwidth, $B_w$ = channel bandwidth

28. **Frequency-Flat Fading** — [[3 - Physical Layer]]:
$$T_s >> \tau_{max}, \quad B_s << B_w$$

29. **OFDM Subcarrier Spacing** — [[3 - Physical Layer]], [[10 - OFDMA]]:
$$\Delta f = \frac{1}{T_{sym}}$$
where $\Delta f$ = subcarrier spacing, $T_{sym}$ = symbol duration

30. **Passband Carrier** (useless?) — [[3 - Physical Layer]]:
$$A \cos(2\pi f_c t + \phi)$$
where $A$ = amplitude, $f_c$ = carrier frequency, $\phi$ = phase

31. **Bits per Symbol** — [[3 - Physical Layer]]:
$$\log_2(M) \text{ bits/symbol}$$
where $M$ = constellation points

32. **Fourier Series (general)**  — [[4 - Physical Layer Notes]]:
$$f(x)=a_{0}+\sum_{n=1}^{N}[a_{n}\cos(\frac{n\pi}{L}x)+b_{n}\sin(\frac{n\pi}{L}x)]$$

33. **Fourier Coefficients**  — [[4 - Physical Layer Notes]]:
$$a_{0}=\frac{1}{2L}\int_{-L}^{L}f(x)dx, \quad a_{n}=\frac{1}{L}\int_{-L}^{L}f(x)\cos(\frac{n\pi}{L}x)dx, \quad b_{n}=\frac{1}{L}\int_{-L}^{L}f(x)\sin(\frac{n\pi}{L}x)dx$$

34. **SNR in dB** — [[4 - Physical Layer Notes]]:
$$\text{SNR}_{\text{dB}} = 10 \log_{10}(\text{SNR})$$

35. **Wavelength** — [[5 - Propagation models]]:
$$\lambda = \frac{c}{f}$$
where $\lambda$ = wavelength, $c \approx 3 \times 10^8$ m/s = speed of light, $f$ = frequency in Hz

36. **Antenna Size** — [[5 - Propagation models]]:
$$\lambda/4 \text{ to } \lambda/2$$

37. **Space Diversity Separation** — [[5 - Propagation models]]:
$$10\lambda \text{ to } 20\lambda$$

38. **Log-Distance Path Loss (linear)** — [[5 - Propagation models]]:
$$\overline{PL(d)} \propto \left(\frac{d}{d_0}\right)^n$$
where $d$ = distance, $d_0$ = reference distance, $n$ = path loss exponent

39. **Log-Distance Path Loss (dB)** — [[5 - Propagation models]]:
$$\overline{PL(dB)} = \overline{PL(d_0)} + 10n \log\left(\frac{d}{d_0}\right)$$
where $\overline{PL(d_0)}$ = path loss at reference distance

40. **Log-Normal Shadowing** — [[5 - Propagation models]]:
$$PL(d) = \overline{PL(d)} + X_\sigma$$
where $X_\sigma$ = zero-mean Gaussian random variable (shadowing)

41. **Log-Normal Shadowing (dB)** — [[5 - Propagation models]]:
$$PL(d)\,(dB) = \overline{PL(d_0)} + 10n \log\left(\frac{d}{d_0}\right) + X_\sigma$$

42. **Received Power** — [[5 - Propagation models]]:
$$P_r(d)\,(dB) = P_t(d)\,(dB) - PL(d)\,(dB)$$
where $P_r$ = received power, $P_t$ = transmitted power

43. **Okumura Model** (useless?) — [[5 - Propagation models]]:
$$L = L_{FS} + A_{mu}(f,d) - G(H_b) - G(H_m) - G_{area}$$
where $L_{FS}$ = free-space loss, $A_{mu}$ = median attenuation, $G$ = gain terms

44. **Okumura Height Gains** (useless?) — [[5 - Propagation models]]:
$$G(H_b) = 20 \log\left(\frac{H_b}{200}\right), \quad G(H_m) = 10 \log\left(\frac{H_m}{3}\right)$$
where $H_b$ = base-station height (m), $H_m$ = mobile height (m)

45. **Hata Model** (useless?) — [[5 - Propagation models]]:
$$A + B \log R$$
where $R$ = distance (km), $A$ and $B$ depend on frequency and antenna height

46. **COST-231 Model** (useless?) — [[5 - Propagation models]]:
$$L_{COST} = 46.3 + 33.9\log(f) + [44.9 - 6.55\log(h_b)]\log(d) + C_m - 13.82\log(h_b) - A(h_m)$$
where $f$ = frequency (MHz), $h_b$ = base height (m), $d$ = distance (km), $C_m$ = city correction


<div style="page-break-after: always;"></div>


47. **MSI Planet Model** (useless?) — [[5 - Propagation models]]:
$$P_r = P_t + K_1 + K_2\log(d) + K_3\log(H_b) + K_4 DL + K_5\log(H_b)\log(d) + K_6\log(H_m) + K_c + K_o$$
where $K_i$ = correction factors, $DL$ = diffraction loss

48. **Walfisch-Ikegami Model** (useless?) — [[5 - Propagation models]]:
$$L = L_{FS} + L_{RT} + L_{MS}$$
where $L_{FS}$ = free-space loss, $L_{RT}$ = rooftop diffraction, $L_{MS}$ = multiscreen reflection

49. **Indoor Total Loss** — [[5 - Propagation models]]:
$$\text{total loss} = \text{outdoor path loss} + \text{building penetration loss}$$

50. **Composite Median Loss** — [[5 - Propagation models]]:
$$L_{\text{composite}} = L_{\text{outdoor}} + L_{\text{penetration}}$$

51. **Composite Standard Deviation** — [[5 - Propagation models]]:
$$\sigma_{\text{composite}} = \sqrt{\sigma_{\text{outdoor}}^2 + \sigma_{\text{penetration}}^2}$$

52. **Poisson Arrivals** — [[6 - Circuit & Packet Switching]]:
$$P(k \text{ arrivals in } T) = \frac{(\lambda T)^k e^{-\lambda T}}{k!}$$
where $\lambda$ = arrival rate, $T$ = time interval, $k$ = number of arrivals

53. **Service Rate** — [[6 - Circuit & Packet Switching]]:
$$\mu = 1/E(X)$$
where $E(X)$ = mean holding time (call duration)

54. **Offered Load (Erlangs)** — [[6 - Circuit & Packet Switching]]:
$$\rho = \lambda \cdot E(X) = \frac{\lambda}{\mu}$$
where $\rho$ = offered load in Erlangs

55. **Erlang B (blocking)** — [[6 - Circuit & Packet Switching]], [[8 - Erlang Recursive Form]]:
$$P_b = \frac{\rho^c/c!}{\sum_{j=0}^{c} \rho^j/j!}$$
where $P_b$ = blocking probability, $\rho$ = offered load, $c$ = number of channels

56. **Erlang B (recursive)** — [[6 - Circuit & Packet Switching]], [[8 - Erlang Recursive Form]]:
$$P_b(c,\rho) = \frac{\rho P_b(c-1,\rho)}{c + \rho P_b(c-1,\rho)}$$

57. **Trunk Utilization** — [[6 - Circuit & Packet Switching]]:
$$\text{Utilization} = \frac{(1 - P_b) \rho}{c}$$

<div style="page-break-after: always;"></div>


58. **CDMA Encoding** — [[9 - Multiple Access]]:
$$\text{encoded signal} = (\text{original data}) \times (\text{chipping sequence})$$

59. **Slotted ALOHA Max Efficiency** — [[9 - Multiple Access]], [[12 - Slotted ALOHA Performance]]:
$$\frac{1}{e} \approx 0.37$$

60. **Pure ALOHA Success** — [[9 - Multiple Access]]:
$$P(\text{success}) = p(1-p)^{2(N-1)}$$
where $p$ = transmission probability, $N$ = number of nodes

61. **Pure ALOHA Max Efficiency** — [[9 - Multiple Access]], [[12 - Slotted ALOHA Performance]]:
$$\frac{1}{2e} \approx 0.18$$

62. **CDMA Orthogonality** — [[11 - CDMA Derivation]]:
$$S \cdot T = \frac{1}{m}\sum_{i=1}^{m} S_i T_i = 0$$
where $S, T$ = chip sequences, $m$ = number of chips

63. **CDMA Auto-correlation** — [[11 - CDMA Derivation]]:
$$S \cdot S = \frac{1}{m}\sum_{i=1}^{m} S_i^2 = 1$$

64. **Max CDMA Stations** — [[11 - CDMA Derivation]]:
$$\text{Max stations} = N$$
where $N$ = code length (chips)

65. **Slotted ALOHA Success** — [[12 - Slotted ALOHA Performance]], [[104 - midterm revision]]:
$$P_s = np(1-p)^{n-1}$$
where $n$ = number of nodes, $p$ = transmission probability

66. **Slotted ALOHA Optimal $p$** — [[12 - Slotted ALOHA Performance]]:
$$p^* = \frac{1}{n}$$

67. **Network Capacity** — [[12 - Slotted ALOHA Performance]]:
$$\text{Capacity} = \frac{P_s \cdot L}{T_{\text{slot}}} \text{ bits/sec}$$
where $L$ = bits per successful slot, $T_{slot}$ = slot duration


<div style="page-break-after: always;"></div>


67. **Capacity per User** — [[12 - Slotted ALOHA Performance]]:
$$\text{Capacity per user} = \frac{P_s \cdot R}{n}$$
where $R = L/T_{slot}$ = transmission rate

68. **Pure ALOHA Success** — [[12 - Slotted ALOHA Performance]]:
$$P_s = np(1-p)^{2(n-1)}$$

70. **Pure ALOHA Optimal $p$** — [[12 - Slotted ALOHA Performance]]:
$$p^* \approx \frac{1}{2n}$$

71. **MIMO Channel** (useless?) — [[103 - MIMO Systems]]:
$$y(k) = Hx(k) + v(k)$$
where $x(k)$ = transmitted vector, $H$ = channel matrix, $y(k)$ = received vector, $v(k)$ = noise

---

so long and thanks for all the fish