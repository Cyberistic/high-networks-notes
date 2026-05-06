Propagation models are mathematical or empirical ways to estimate how a radio signal behaves as it travels from transmitter to receiver.

In practice, they are used to predict things like:

- path loss
- received signal strength
- coverage area
- how the environment affects the link


## Physical Principles of Propagation

Propagation is the heart of every radio link.

When a radio signal travels from transmitter to receiver, many different processes act on it. These processes decide whether the receiver gets a strong clean signal, a weak distorted signal, or sometimes almost nothing useful at all.

### Main Propagation Effects

#### 1. Attenuation

**Attenuation** means the signal amplitude becomes smaller during propagation.

- the signal loses strength because of natural propagation mechanisms, the farther or harder the path, the weaker the signal usually becomes
- if attenuation is too large, the received signal falls below the reliable detection threshold
- this is often the **single most important factor** in propagation


#### 2. Multipath and Group Delay Distortion

This topic was already introduced in [[3 - Physical Layer#Propagation Mechanisms in Wireless Channels]] and [[3 - Physical Layer#Channel Impulse Response]].

The signal does not always travel along one clean straight path.

- it can reflect off objects
- it can diffract around edges
- it can scatter from rough surfaces or small objects

So the receiver may get many copies of the same signal arriving at different *times* with different *amplitudes* and different *phases*, causing pulse blurring,  cancellation and reinforcement, distortion, fading

One previously mentioned way to fight fading is [[10 - OFDMA#Space Diversity]].



#### 3. Time Variability

Signal strength and quality can vary with **time**, sometimes dramatically.

This was also linked earlier to fading in [[3 - Physical Layer#Propagation Mechanisms in Wireless Channels]].

Why?

- users move
- objects move
- the environment changes

So a signal that is strong now may become weak later.

#### 4. Space Variability

Signal strength and quality also vary with **location and distance**.

This was covered in [[3 - Physical Layer#Propagation Mechanisms in Wireless Channels]] and the distinction between **large-scale** and **small-scale fading**.

- moving a large distance changes average received power
- moving even a small distance can also change the signal because of multipath

#### 5. Frequency Variability

Signal strength and quality can be different on different frequencies.

This was covered in  [[3 - Physical Layer#Frequency-Selective vs Frequency-Flat Fading]].

- some frequencies may be attenuated more than others
- this is one reason why wideband signals may become distorted


### To Master Propagation

According to the slides, to understand and design wireless systems properly, you need 4 things:

1. **Physics**: understand the basic propagation processes
2. **Measurement**: obtain data on propagation behavior in the area of interest
3. **Statistics**: analyze known data and use it to predict unknown behavior
4. **Model Making**: turn the physical understanding and measurements into useful mathematical models


<div style="page-break-after: always;"></div>

## Frequency and Wavelength: Implications

![[radio-3.png | 300]]

Radio waves in the atmosphere travel at almost the speed of light, so wavelength depends directly on frequency:

$$
\lambda = \frac{c}{f}
$$

Where:

- $\lambda$ = wavelength
- $c$ = speed of light $\approx 3 \times 10^8\ \text{m/s}$
- $f$ = frequency in Hz

Examples from the slides:

- at $870\ \text{MHz}$:

$$
\lambda = \frac{3 \times 10^8}{870 \times 10^6} \approx 0.345\ \text{m}
$$

- at $1960\ \text{MHz}$:

$$
\lambda = \frac{3 \times 10^8}{1960 \times 10^6} \approx 0.153\ \text{m}
$$

The wavelength determines propagation stats:

- antenna size is usually on the order of about $\lambda/4$ to $\lambda/2$
- objects larger than a wavelength can significantly reflect or block RF energy
- openings around one wavelength or larger can let energy enter buildings or vehicles more easily


<div style="page-break-after: always;"></div>

## Local Variability: Multipath Effects

![[5 - Propagation models.png | 150]]
![[rayleghghg.png | 200]]
The small-fading mechanisms introduced in [[3 - Physical Layer#Propagation Mechanisms in Wireless Channels]] explain the general behavior of wireless signals (reflect, diffract, scatter), but THERE ARE MORE MECHANISMS!! 

### Slow Fading vs Rapid Fading

- **Slow fading** happens over hundreds of wavelengths and is mainly caused by shadowing from local obstructions.
- **Rapid fading** happens when many received paths move in and out of phase, so the signal can rise or drop suddenly



Rapid fading mumbo-jumbo from the slides:

- fades are roughly $\lambda/2$ apart in space
- at about $800\ \text{MHz}$, this can mean only a few inches of movement changes the signal a lot
- fades also appear across **frequency** and **time**, not only space
- typical fade depth is around **10-15 dB**, sometimes deeper

This is essentially the same small-scale fading idea already introduced in [[3 - Physical Layer#Propagation Mechanisms in Wireless Channels]].

> [!Note] I looked for the difference between Slow/Rapid fading vs Fast/Small fading as they appear to be the same thing, some references do use  *small = rapid* vs *large = slow* interchangeably, but it appears in this context that:
> - Large: describes the *average* signal variation over *large* distances
> - Slow: signal changes that happen slowly with *movement/time* due to shadowing
> - Small: changes over very short distances, like a fraction of a wavelength
> - Rapid: changes very quickly as the user moves or the channel changes
> Though i'm not really sure. They sound the same to me. 



### Rayleigh Fading

When many multipath components combine without one strong dominant LOS path, the envelope of the received signal is often modeled by a **Rayleigh distribution**.

These deep short fades are often called **Rayleigh fades**.

Short version:

- large-scale fading changes the average signal over long distance
- Rayleigh fading causes fast local fluctuations around that average



## Combating Rayleigh Fading: Space Diversity

![[relghhg antennas.png | 150]]

This was already introduced briefly in [[10 - OFDMA#Space Diversity]].

- idea is to use two receiving antennas
- separate them by several wavelengths
- because of that separation, both antennas usually will **not** be in a deep fade at the same instant

So the receiver can:

- choose the stronger antenna
- switch between antennas
- or combine both signals

This improves reliability because Rayleigh fades are usually very short in space and time.

The slides state that good decorrelation often needs antenna separation of about **$10\lambda$ to $20\lambda$**.

Brief calculation (present in the slides):

- at $800\ \text{MHz}$, $\lambda = \dfrac{3 \times 10^8}{800 \times 10^6} = 0.375\ \text{m}$
- so $10\lambda$ to $20\lambda = 3.75$ to $7.5\ \text{m}$ or **12-24 ft**

- at $1900\ \text{MHz}$, $\lambda = \dfrac{3 \times 10^8}{1900 \times 10^6} \approx 0.158\ \text{m}$
- so $10\lambda$ to $20\lambda \approx 1.58$ to $3.16\ \text{m}$ or ~**5-10 ft**


<div style="page-break-after: always;"></div>

## Space Diversity Application Limitations

Space diversity is mainly applied at the **receiving side** of the link.

Why not simply transmit the same signal from two antennas?

- the two transmitted waves still combine into just one resulting signal at any observation point
- this does **not** create receive diversity at that point
- it can also create unwanted radiation nulls in some directions

So in classical cellular design, space diversity is mainly used on the **uplink / reverse path** at the base station.

Why the uplink specifically?

- the base station has physical room for two well-separated antennas
- a handset (mobile, laptop) usually does not have enough space to separate antennas by several wavelengths




<div style="page-break-after: always;"></div>

## Types Of Propagation Models And Their Uses

Propagation models are not all used for the same purpose. Some are meant to explain a single path physically, while others are meant to estimate average coverage over a whole area.

### 1. Simple Analytical Models

Used for understanding and predicting **individual paths** and **specific obstruction cases**.

Typical examples (slides)::

- free-space model using the Friis formula
- reflection cancellation
- knife-edge diffraction

These models are useful when you want to understand the physical mechanism itself.

### 2. General Area Models

These are mainly **statistical** models.

They are used for:

- early system dimensioning: getting a first estimate of how large the network should be before detailed design
- estimating cell counts: approximating how many base stations or cells are needed to serve the target area
- rough coverage planning over a region: predicting the general coverage footprint before doing detailed path-by-path analysis

Typical examples (slides):

- Okumura-Hata
- COST-231
- Walfisch-Ikegami

<div style="page-break-after: always;"></div>

### 3. Point-to-Point Models

These are mainly **analytical** models.

They are used for:

- detailed coverage analysis: checking signal behavior more accurately for a specific link or site
- cell planning: choosing better base-station locations and coverage boundaries
- studying one specific transmitter-receiver path more carefully: modeling one path in more detail instead of averaging over a whole area

Typical examples (slides):

- ray tracing
- Longley-Rice

### 4. Local Variability Models

These are also mainly **statistical**.

They describe microscopic fluctuations in signal level within a local area and help estimate **probability of service**, meaning the chance that the received signal is good enough for reliable operation at a location.

Typical examples (slides):

- Rayleigh distribution
- normal distribution
- joint probability techniques

Short version:

- analytical models explain specific paths and mechanisms
- area models estimate average coverage over a region
- local variability models describe random fluctuations around that average

<div style="page-break-after: always;"></div>

## General Principles Of Area Models


Area models try to mimic an **average path** inside a defined area.

They are based mainly on **measured data**, not on detailed analysis of each reflection, obstruction, or diffraction event on a specific path.

Typical inputs include:

- frequency
- distance between transmitter and receiver
- actual or effective base-station height
- mobile-station height
- average terrain elevation
- morphology correction loss such as urban, suburban, or rural

![[area-models.png | 300]]

- the **green trace** is the real measured signal, so it goes up and down because real propagation is messy
- the **red trace** is the Okumura-Hata model prediction, so it looks smoother and shows the average trend
-

tl;dr:

- the model gives a smooth average prediction
- real measured signal values around that curve can be much higher or much lower

So area models are good for **average planning**, but they do not fully capture what happens on one exact street or one exact path. 

> [!Note] We'll see how they evolve slowly:
اكو مرة تحاططت على لابتوب سعره ٢٣١ يورو من msi وما دفعت ولا فلس لاني بطران 
> okumura -> hata -> Euro Cost-231 -> MSI Planet -> Walfisch-Betroni


<div style="page-break-after: always;"></div>

## Log Distance Path Loss Model
The slides are very confusing so I will try my best to explain how it works.
 
The main idea is that average received power decreases **logarithmically** with distance.
This model is widely used for both indoor and outdoor propagation and is a standard **large-scale path loss model**.

*Path loss*: the reduction in signal power as the signal travels from transmitter to receiver.

In simple words, the model says:

- pick a known reference point at distance $d_0$
- measure or calculate the path loss there
- then estimate how much more loss appears when the receiver moves farther away to distance $d$

The average path loss can be written as:

$$
\overline{PL(d)} = \frac{P_r(d)}{P_t(d)} \propto \left(\frac{d}{d_0}\right)^n
$$

Here:

- $\dfrac{P_r(d)}{P_t(d)}$ means the fraction of transmitted power that is still received at distance $d$
- $\propto$ means "is proportional to", so the ratio follows the same trend as the distance term 
- the path loss at distance $d$ depends on how far $d$ is compared with the reference distance $d_0$
- if $d$ becomes larger, path loss increases
- the exponent $n$ controls how fast that increase happens

In dB form:

$$
\overline{PL(dB)} = \overline{PL(d_0)} + 10n \log\left(\frac{d}{d_0}\right)
$$

This dB form is usually the more practical one.

It says:

- start with the known path loss at the reference distance, $\overline{PL(d_0)}$
- then add an extra loss term, $10n \log\left(\frac{d}{d_0}\right)$, to account for moving farther away

<div style="page-break-after: always;"></div>

**path loss at new distance** = **path loss at reference distance** + **extra loss caused by the increased distance**


notation:

- $P_t(d)$ = transmitted power
- $P_r(d)$ = received power at distance $d$
- $\overline{PL(d)}$ = average path loss at distance $d$
- $\overline{PL(d_0)}$ = average path loss at the reference distance
- $d_0$ = close-in reference distance, often determined empirically
- $d$ = transmitter-receiver separation
- $n$ = path loss exponent

Meaning of $n$:

- it tells us how fast path loss increases with distance
- larger $n$ means the signal decays faster

Quick intuition:

- if the environment is open, $n$ is smaller
- if the environment has more walls, clutter, or obstacles, $n$ is larger
- so the same increase in distance causes more loss in a difficult environment than in free space

This is a **large-scale average** model, so it gives the trend, not the exact received power at every point.

But how do we know the reference point path loss?!?! stay tuned for the next page

<div style="page-break-after: always;"></div>

## Free Space Reference Distance, $d_0$

The reference distance $d_0$ is used as the starting point for the log-distance model.

In simple words, we first choose one **known reference location** close to the transmitter, then use that point as the baseline for predicting path loss farther away.

Important rules:

- $d_0$ should be in the antenna **far field**
- this avoids near-field effects in the reference path
- the value of $d_0$ depends on the environment

Definitions:

- **Near field**: the region very close to the antenna, where the electromagnetic field is still complicated and does not behave like a clean radiating wave yet
- **Far field**: the region far enough from the antenna that the wave behaves more regularly, so standard propagation formulas become reliable
- **Reference path**: the baseline path used as the starting point for the model
- **Empirically**: chosen or confirmed from real measurements, not only from theory

Why this matters:

- if $d_0$ is chosen in the near field, the measured path loss can be misleading
- if $d_0$ is in the far field, it becomes a more stable and meaningful starting point

Typical values from the slides:

- large cellular: $d_0 \approx 1\ \text{km}$
- microcell: $d_0 \approx 1\text{ m to }10\text{ m}$

The reference path loss $PL(d_0)$ can be obtained using either:

- **free-space path loss** = ideal theoretical loss (signal loss you would expect in an ideal open environment with no walls, buildings, reflections, or other obstacles.)
- **field measurement at $d_0$** = real measured loss in the actual environment


<div style="page-break-after: always;"></div>

### Path Loss Exponent, $n$

The path loss exponent depends strongly on the environment.

- lower $n$ means propagation is easier
- higher $n$ means obstacles and clutter make the signal decay faster

Notice the values (don't memorize, just note how they change in. certain settings):

- free space: $n = 2$
- urban cellular: $n = 2.7$ to $3.5$
- shadowed urban cellular: $n = 3$ to $5$
- in-building LOS: $n = 1.6$ to $1.8$
- obstructed in building: $n = 4$ to $6$
- obstructed in factories: $n = 2$ to $3$




<div style="page-break-after: always;"></div>

## Log Normal Shadowing

The plain log-distance model gives only the **average** path loss. It does not directly account for shadowing/clutter (nearby buildings, walls, trees, cars, and other obstacles that affect the signal).

So even if two receivers are at the same distance from the transmitter, they may not see exactly the same path loss.

In simple words, this model says:

- the log-distance model gives the average expected loss
- real locations are usually a little better or worse than that average
- we treat that extra difference as a random variation caused by the environment

the measured path loss is treated as a random variable around the average value:

$$
PL(d) = \overline{PL(d)} + X_\sigma
$$

Meaning in words:
*actual path loss at distance $d$ *= *average path loss at that distance* + *a random extra term caused by shadowing and clutter*

Using the log-distance model in dB:

$$
PL(d)\,(\text{dB}) = \overline{PL(d_0)} + 10n \log\left(\frac{d}{d_0}\right) + X_\sigma
$$

This says:

- start with the reference path loss at $d_0$
- add the normal distance-based loss term
- then add one more random term to represent real environmental variation

The received power is then:

$$
P_r(d)\,(\text{dB}) = P_t(d)\,(\text{dB}) - PL(d)\,(\text{dB})
$$

Meaning in words:

- received power = transmitted power - total path loss


notation:

- $X_\sigma$ = the random shadowing term in dB
- **zero-mean** means it is centered around 0, so sometimes the actual loss is above the average and sometimes below it
- **Gaussian random variable** means it follows a normal distribution in dB
- $\sigma$ = the standard deviation, which tells us how spread out the shadowing values are around the average
- antenna gains are included in $PL(d)$

Why it is called **log-normal shadowing**:

- in dB, the variation is modeled as a normal distribution
- in linear scale, that corresponds to a log-normal distribution


Short version:

- log-distance model gives the average trend
- log-normal shadowing adds random variation around that trend due to clutter and shadowing

<div style="page-break-after: always;"></div>

## The Okumura Model


![[okamura.png | 350]]

The **Okumura model** is a large-scale empirical propagation model based on extensive drive-test measurements made in **Tokyo and its suburbs** in the late 1960s and early 1970s.
it was built from **real measured data**, then turned into curves that engineers could use for coverage prediction.

### General Idea

Okumura analyzed measurements over many different conditions, including:

- different frequencies
- different antenna heights
- different environments
- different propagation distances

From that data, the model provides:

- an additional median attenuation term, $A_{mu}(f,d)$: the extra average loss taken from Okumura's measured curves for a given frequency and distance
- an area correction factor, $G_{area}$: an adjustment based on the type of area, such as urban, suburban, or rural

The original curves were given for:

- base-station antenna height $h_b = 200\ \text{m}$
- mobile-station antenna height $h_m = 3\ \text{m}$

Why the model matters:

- it became a classic area model for wireless planning
- later models like **Hata** and **COST-231** were built from the same basic idea, but converted into easier formulas

<div style="page-break-after: always;"></div>

### Structure of the Okumura Model

The path loss is written as:

$$
L = L_{FS} + A_{mu}(f,d) - G(H_b) - G(H_m) - G_{area}
$$



- $L_{FS}$: free-space path loss, meaning the ideal loss in open space with no obstacles
- $A_{mu}(f,d)$: additional median loss from Okumura's curves, depends on frequency $f$ and distance $d$
- $G(H_b)$: base-station antenna height gain
- $G(H_m)$: mobile-station antenna height gain
- $G_{area}$: morphology correction term for the type of area

Meaning in words:

- start with the **free-space path loss**
- add the extra median loss taken from Okumura's measured curves
- then subtract gain terms that improve propagation, such as antenna height gain and area correction


## Okumura Model Terms

![[okumura terms.png]]

The slide gives the height-gain terms as:

$$
G(H_b) = 20 \log\left(\frac{H_b}{200}\right)
$$

$$
G(H_m) = 10 \log\left(\frac{H_m}{3}\right)
$$

So:

- taller base-station antennas usually reduce path loss
- taller mobile antennas also help, but with a smaller gain term

### Morphology Gain

The area correction depends on the environment. The slide lists:

- dense urban: $0\ \text{dB}$
- urban: $5\ \text{dB}$
- suburban: $10\ \text{dB}$
- rural: $17\ \text{dB}$

Note:

- here a **higher** $G_{area}$ is generally **better** because it is subtracted in the Okumura formula, so a larger value reduces the predicted path loss
- so rural gets the biggest reduction, while dense urban gets the least



<div style="page-break-after: always;"></div>

## The Hata Model

The **Hata model** is an empirical propagation-loss formula derived from the **Okumura model**.

Its purpose is to make Okumura-style prediction easier to calculate automatically, without reading values manually from curves.


For urban areas, the Hata model expresses propagation loss in a simple form like:

$$
A + B \log R
$$

where:

- $A$ and $B$ depend on frequency and antenna height
- $R$ is the distance between the base station and mobile station

So Hata keeps the same overall idea as Okumura, but turns it into direct formulas.

### Valid Range

According to the slides, the Hata model is applicable for:

- frequency: $100\ \text{MHz}$ to $1500\ \text{MHz}$
- distance: $1$ to $20\ \text{km}$
- base-station antenna height: $30$ to $200\ \text{m}$
- mobile-station antenna height: $1$ to $10\ \text{m}$

### Main Assumptions / Limitations

The model is simplified, so it assumes:

- isotropic antennas: an ideal imaginary antenna that radiates power equally in all directions.
- quasi-smooth terrain, not very irregular terrain
- urban-area propagation loss is the standard base formula
- correction equations are used for other areas

Hata is practical and easy to use, but it does **not** include path-specific corrections for each street, obstacle, or building.

### Why It Is Useful

Even though it is simplified, the Hata model has strong practical value because its predictions are usually close to Okumura's results, while being much easier to compute.

<div style="page-break-after: always;"></div>

### Hata Formulas 
he basically approximated the curve of okumura into values and put them in equations for different landscapes

![[hata eq.png | 400]]
![[descriptor.png | 400]]

notation:

- $f$ = carrier frequency in MHz
- $h_b$ = base-station antenna height in meters
- $h_m$ = mobile-station antenna height in meters
- $d$ = distance between base station and mobile station in km
- $A(h_m)$ = correction factor for mobile antenna height

tl;dr:

- start with the urban-area loss formula
- adjust it for the mobile antenna height
- if the environment is suburban or rural, apply extra correction terms, instead of looking manually at the curve

<div style="page-break-after: always;"></div>



## The EURO COST-231 Model

The **COST-231 model** was developed by the **European COoperative for Scientific and Technical Research** committee.

Its main purpose is to extend the **Hata model** to higher frequencies, specifically the **1.8 GHz to 2 GHz** band, which became important for **PCS (Personal Communications Services)**.

COST-231 is basically an updated version of Hata with different numerical constants to cover higher frequencies.

### Valid Range

- frequency: $1500\ \text{MHz}$ to $2000\ \text{MHz}$
- distance: $1$ to $20\ \text{km}$
- base-station antenna height: $30$ to $200\ \text{m}$
- mobile-station antenna height: $1$ to $10\ \text{m}$

### Formula

For urban areas:

$$
L_{COST}(urban) = 46.3 + 33.9\log(f) + [44.9 - 6.55\log(h_b)]\log(d) + C_m - 13.82\log(h_b) - A(h_m)
$$

### Parameters

- $f$ = carrier frequency in MHz
- $h_b$ and $h_m$ = base-station and mobile-station antenna heights in meters
- $d$ = distance between base station and mobile station in km
- $A(h_m)$ = mobile antenna height correction factor, same as in Hata
- $C_m$ = city-size correction factor:
  - $C_m = 0\ \text{dB}$ for suburbs
  - $C_m = 3\ \text{dB}$ for metropolitan centers


The slide also lists an environmental factor $C$ for $1900\ \text{MHz}$:
- dense urban: $-2$
- urban: $-5$
- suburban: $-10$
- rural: $-26$


So COST-231 is the **higher-frequency extension** of Hata.


- Hata works well up to $1500\ \text{MHz}$
- COST-231 extends similar formulas to $1500$-$2000\ \text{MHz}$
- add a city-size correction term
- useful for PCS and later cellular bands

<div style="page-break-after: always;"></div>

## Morphological Zones

**Morphological zones** are categories that describe the **type of land use** and **building density** in an area.

These categories are used in propagation models to apply different correction factors, because signal behavior depends heavily on the environment.

Zone types include (slide goes in detail and shows images): 

1. Suburban: mix of residential and business communities
2. Urban: urban residential and office areas
3. Dense Urban: dense business districts with skyscrapers (10-20 stories and above)
4. Rural: open farm land, large open spaces, sparsely populated residential areas
5. Rural-Highway:  highways near open farm land


tl;dr:

- different zones have different correction factors in area models
- the same base station can behave differently depending on whether it serves a dense urban core or a rural highway
- zones can also change abruptly, so a single cell may need to account for multiple morphologies



<div style="page-break-after: always;"></div>

## The MSI Planet General Model

The **MSI Planet model** is a general-purpose propagation model used in the PlaNET radio-planning software.

It includes terms similar to **Okumura-Hata** and **COST-231**, but also adds extra correction factors for specific obstructions and clutter.

### Formula (u can safely skip trust)

$$
P_r = P_t + K_1 + K_2\log(d) + K_3\log(H_b) + K_4 DL + K_5\log(H_b)\log(d) + K_6\log(H_m) + K_c + K_o
$$

### Parameters

- $P_r$ = received power in dBm
- $P_t$ = transmit ERP in dBm
- $H_b$ = base-station effective antenna height
- $H_m$ = mobile-station effective antenna height
- $DL$ = diffraction loss in dB
- $K_1$ = intercept
- $K_2$ = slope
- $K_3$ = correction factor for base-station antenna height gain
- $K_4$ = correction factor for diffraction loss, which accounts for clutter heights
- $K_5$ = Okumura-Hata correction factor for antenna height and distance
- $K_6$ = correction factor for mobile-station antenna height gain
- $K_c$ = correction factor due to clutter at the mobile-station location
- $K_o$ = correction factor for street orientation


In simple words:

- start with a basic path-loss trend
- then add correction terms for heights, distance, diffraction, clutter, and even street direction
- so it can be tuned more precisely for specific locations than the standard area models
- MSI Planet is a flexible general model
- it combines Hata-style terms with additional correction factors
- used in planning software to get more site-specific predictions

> [!note] all these models adding extra terms reminds me of this golden post: [link](https://www.reddit.com/r/LinkedInLunatics/comments/1mjqjd4/emc%C2%B2ai/)
> 
<div style="page-break-after: always;"></div>


## Walfisch-Betroni / Walfisch-Ikegami Models

![[walfsjdhs.png | 200]]

These models are used for **built-up urban areas**, especially where rows of buildings and streets strongly shape how the radio wave travels.

Ordinary Okumura-type models still work in this kind of environment, but the Walfisch models try to be **more accurate** by using the actual propagation mechanisms involved.

Main idea: In dense city areas, propagation is often dominated by:

- **diffraction over rooftops**
- **multiple reflections along streets**

So instead of treating the city only as a general environment type, this model tries to represent what the wave is physically doing.

### Path Loss Expression

$$
L = L_{FS} + L_{RT} + L_{MS}
$$

where:

- $L_{FS}$= free-space path loss: the basic loss that would happen even in open space with no buildings blocking the path
- $L_{RT}$ = rooftop diffraction loss: extra loss caused when the wave bends over the tops of buildings, blocking direct line-of-sight propagation
- $L_{MS}$ = multiscreen reflection loss: extra loss caused by the wave interacting with many rows of buildings as it moves through the city


<div style="page-break-after: always;"></div>

## Typical Model Results

The slides show practical examples of how different models and environments affect predicted cell range.

### Okumura/Hata at 870 MHz

![[comparison cost okumura.png | 300]]

Pattern:

- denser environments have shorter range
- rural areas allow much longer range because there is less obstruction
- the same environment at 1900 MHz gives noticeably shorter range than at 870 MHz
- this is because higher frequencies experience more attenuation and penetration loss


- frequency matters: higher frequency = shorter range for the same power
- environment matters: dense urban = much shorter range than rural
- these tables show why operators need more cells in dense urban areas and at higher frequencies

<div style="page-break-after: always;"></div>

## Propagation at 1900 MHz vs 800 MHz

Propagation behavior at 1900 MHz is **similar in nature** to 800 MHz, but all effects are **more pronounced**.

### Main Differences

**Penetration into buildings**:

- at 1900 MHz, signals can enter buildings through openings more effectively because the wavelength is smaller
- but once inside, absorbing materials and walls attenuate the signal more severely than at 800 MHz

**Overall effect**:

- at 1900 MHz, the signal usually changes more sharply from place to place because it is affected more strongly by walls, obstacles, and the local environment
- as a result, nearby locations can have more different signal levels than they would at 800 MHz
- in practice, this means strong-signal areas tend to stand out more, while weak-signal areas become weaker and more noticeable

**Coverage radius**:

- a 1900 MHz base station with the same ERP (power in watts) and antenna height covers roughly **two-thirds** the distance of an equivalent 800 MHz base station

So: 
- to cover the same area at 1900 MHz, you generally need more base stations or higher power
- this is why lower frequencies are often preferred for wide-area coverage, while higher frequencies are used for capacity in dense areas

tl;dr:
- higher frequency = shorter wavelength = more detailed interaction with the environment
- the result is generally shorter range and more variable signal strength



<div style="page-break-after: always;"></div>


## Statistical Techniques

### Distribution Statistics Concept

An area model predicts the **median** signal strength versus distance over an area.

That means:

- for each distance from the cell, the model gives the **average trend** signal level
- the real signal at a specific location may still be higher or lower because of local effects like shadowing, reflections, and clutter


![[stats.png | 200]]

If we measure many real points at the same distance, the signal values will not all be the same.

Instead, they spread around the predicted median value.

Two useful quantities are:

- $M$ = median observed signal strength
- $\sigma$ = standard deviation, which tells us how widely the real values are spread around the median

If the spread is approximately normal in dB, then $M$ and $\sigma$ can be used to estimate the probability of receiving a certain signal level at a given distance.


- the model gives the center of the distribution
- $\sigma$ tells us how much real locations wander above or below that center
- together, they let us talk about **probability of service**, not just average coverage




<div style="page-break-after: always;"></div>

## Practical Application of Distribution Statistics

### General Approach

1. Use a propagation model to predict signal strength versus distance.
2. Collect measured data in the real environment.
3. From the measurements, estimate:

- the median signal strength $M$
- the standard deviation of the error, $\sigma$

4. Add an extra margin so that a desired percentage of real locations will be above the required signal level.
 
> [!note] Recall model distribution 
> The basic model curve usually represents about the **50% level**.
> - roughly half of real observations are above the curve
> - roughly half are below it

If we want better reliability, we do not keep the design exactly on the median curve.

Instead, we add a margin so the predicted curve is moved to a safer level.

This is sometimes described as dropping the model curve so that a chosen percentage of real observations remain above the required operating threshold.



<div style="page-break-after: always;"></div>

## Cell Edge: Area Availability and Probability of Service

![[cell edge.png | 200]]

Here, we discuss probabilities that the signal at a location is good enough to meet the required service threshold.

The overall probability of service is usually **best close to the BTS (Base Transceiver Station)** and gets worse as distance increases.

This happens because path loss increases with distance, so the received signal gets closer to the minimum usable level near the cell edge.

For a cell with about **90% overall location probability** across the whole coverage area, the probability right at the **cell edge** is often about **75%**.

This is the common **90% / 75%** coverage objective.

<div style="page-break-after: always;"></div>

## Application of Distribution Statistics: Example

![[stats example.png | 300]]

Suppose we want to design a cell so that at least **75% of locations at the cell edge** receive at least:

$$
-95\ \text{dBm}
$$

The slides note that this corresponds roughly to providing coverage to about **90% of total locations within the cell**.

Assume measurements show:

$$
\sigma = 10\ \text{dB}
$$

Using the *Cumulative Normal Distribution* from the chart, the $75\%$ point corresponds to about:

$$
0.675\sigma
$$

This means the **median** signal at the cell edge must be stronger than the minimum required signal by $0.675\sigma$.

So the design target becomes:

$$
-95\ \text{dBm} + (0.675 \times 10\ \text{dB})
$$

$$
= -95\ \text{dBm} + 6.75\ \text{dB}
$$

$$
\approx -88\ \text{dBm}
$$

- the required minimum usable level is $-95\ \text{dBm}$
- but if we design the median edge signal to be only $-95\ \text{dBm}$, then only about $50\%$ of edge locations would meet that target
- to make about $75\%$ of edge locations meet the target, we design the **median** edge signal stronger, at about $-88\ \text{dBm}$

This extra amount is the **fade margin**.

<div style="page-break-after: always;"></div>


## Building Penetration

![[building penet.png | 300]]
### Statistical Characterization

Building and vehicle penetration are hard to model exactly with a simple analytical formula. Because many factors affect the extra loss (wall material, glass type, building thickness, openings and windows, floor level, where the user is inside the building or vehicle)


![[building loss.png | 300]]

Indoor coverage is usually modeled as:

$$
\text{total loss} = \text{outdoor path loss} + \text{building penetration loss}
$$

In other words:

- first estimate the normal outdoor signal level
- then add an extra penetration loss to account for entering the building or vehicle

This additional penetration loss is treated statistically, just like shadowing:

- estimate or measure the **median** penetration loss
- determine its statistical distribution
- estimate or measure its standard deviation
- add enough margin in the link budget to handle that extra loss


<div style="page-break-after: always;"></div>

## Composite Probability of Service


### Composite Median Loss

The median losses add directly:

$$
L_{\text{composite}} = L_{\text{outdoor}} + L_{\text{penetration}}
$$


### Composite Standard Deviation

The variations also combine, but not by simple addition.

The slide gives:

$$
\sigma_{\text{composite}} = \sqrt{\sigma_{\text{outdoor}}^2 + \sigma_{\text{penetration}}^2}
$$

So if outdoor loss and penetration loss each have their own spread, the total spread becomes larger.

The probability of service depends on both:

- the composite median
- the composite standard deviation



<div style="page-break-after: always;"></div>

## Example: Composite Probability of Service: Calculating Fade Margin for Link Budget

![[composition.png | 500]]
Suppose:

- outdoor attenuation standard deviation is $\sigma_{\text{outdoor}} = 8\ \text{dB}$
- penetration-loss standard deviation is $\sigma_{\text{penetration}} = 8\ \text{dB}$
- desired probability of service is $P = 75\%$ at the cell edge

We want to find:

- the composite standard deviation
- the required fade margin

#### Step 1: Find Composite Standard Deviation

Using the composite formula:

$$
\sigma_{\text{composite}} = \sqrt{\sigma_{\text{outdoor}}^2 + \sigma_{\text{penetration}}^2}
$$

$$
\sigma_{\text{composite}} = \sqrt{8^2 + 8^2}
$$

$$
= \sqrt{64 + 64}
$$

$$
= \sqrt{128}
$$

$$
\approx 11.31\ \text{dB}
$$

#### Step 2: Find Fade Margin for $75\%$ Service

From the cumulative normal distribution, $75\%$ corresponds to about:

$$
0.675\sigma
$$

So the required fade margin is:

$$
(11.31)(0.675) \approx 7.63\ \text{dB}
$$

*exam question probably *