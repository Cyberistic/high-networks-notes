
Let:

- $p$ = probability that one node transmits in a slot
- $n$ = number of nodes
- $1-p$ = probability that one node does not transmit in a slot



For one specific user to transmit successfully:

- that user must transmit, which happens with probability $p$
- the remaining $n-1$ users must stay silent, each with probability $(1-p)$

So,

$$
\begin{align}
P(\text{one specific user succeeds})
&= p(1-p)(1-p)\cdots(1-p) \\
&= p(1-p)^{n-1}
\end{align}
$$



## Probability That Any User Succeeds

Any one of the $n$ users could be the successful user, so

$$
\begin{align}
P_s
&= p(1-p)^{n-1} + p(1-p)^{n-1} + \cdots + p(1-p)^{n-1} \\
&= n\big[p(1-p)^{n-1}\big]
\end{align}
$$

Hence, the success probability of slotted ALOHA is

$$
P_s = np(1-p)^{n-1}
$$


<div style="page-break-after: always;"></div>

## Maximizing the Success Probability

We want to choose $p$ to maximize $P_s$.

$$
P_s = np(1-p)^{n-1}
$$

Differentiate with respect to $p$:

$$
\begin{align}
\frac{dP_s}{dp}
&= n\left[(1-p)^{n-1} + p(n-1)(1-p)^{n-2}(-1)\right] \\
&= n(1-p)^{n-1} - np(n-1)(1-p)^{n-2}
\end{align}
$$

Set the derivative equal to zero:

$$
\begin{align}
0
&= n(1-p)^{n-1} - np(n-1)(1-p)^{n-2} \\
&= n(1-p)^{n-2}\big[(1-p)-p(n-1)\big]
\end{align}
$$

So,

$$
\begin{align}
(1-p)-p(n-1) &= 0 \\
1-p-pn+p &= 0 \\
1-pn &= 0 \\
pn &= 1 \\
p^* &= \frac{1}{n}
\end{align}
$$

Thus, the value of $p$ that maximizes the success probability is

$$
p^* = \frac{1}{n}
$$



Substitute $p^* = \frac{1}{n}$ into $P_s$:

$$
\begin{align}
P_s
&= np^*(1-p^*)^{n-1} \\
&= n\left(\frac{1}{n}\right)\left(1-\frac{1}{n}\right)^{n-1} \\
&= \left(1-\frac{1}{n}\right)^{n-1}
\end{align}
$$

This is the probability of success for the whole system when each user transmits with the optimal probability $p^*$.


<div style="page-break-after: always;"></div>

## Capacity

Given: 

$$
\text{Capacity of the network} = \frac{P_s \cdot L}{T_{\text{slot}}} \; \text{bits/sec}
$$

where:

- $L$ = number of bits transmitted in one successful slot
- $T_{\text{slot}}$ = time duration of one slot

if

$$
R = \frac{L}{T_{\text{slot}}}
$$

is the transmission rate in bits/sec, then

$$
\text{Capacity of the network} = P_s \cdot R
$$

Capacity per user is

$$
\text{Capacity per user} = \frac{P_s \cdot R}{n}
$$

Here, $P_s$ is a success probability per slot, so to convert it to bits/sec we multiply by the number of bits in a successful slot and divide by the slot duration.


<div style="page-break-after: always;"></div>

## Behavior as the Number of Users Grows

Now let $n \to \infty$:

$$
\begin{align}
P_s
&= \left(1-\frac{1}{n}\right)^{n-1} \\
&= \left(\frac{n-1}{n}\right)^{n-1}
\end{align}
$$

> [!Note] Recall:
> Using the binomial expansion,
> $$
> (a+x)^t = \sum_{k=0}^{t} \binom{t}{k} a^{t-k}x^k
> $$

Apply this to $\left(1-\frac{1}{n}\right)^{n-1}$:

$$
\begin{align}
\left(1-\frac{1}{n}\right)^{n-1}
&= \sum_{k=0}^{n-1} \binom{n-1}{k}(1)^{n-1-k}\left(-\frac{1}{n}\right)^k \\
&= \sum_{k=0}^{n-1} \binom{n-1}{k}\frac{(-1)^k}{n^k} \\
&= \sum_{k=0}^{n-1} \frac{(n-1)!}{k!(n-1-k)!}\frac{(-1)^k}{n^k}
\end{align}
$$

Now take the limit:

$$
\begin{align}
\lim_{n\to\infty} P_s
&= \lim_{n\to\infty} \sum_{k=0}^{n-1} \frac{(n-1)!}{k!(n-1-k)!}\frac{(-1)^k}{n^k} \\
&= \sum_{k=0}^{\infty} \frac{(-1)^k}{k!}
\end{align}
$$

because for fixed $k$,

$$
\begin{align}
\lim_{n\to\infty} \frac{(n-1)!}{(n-1-k)!\,n^k}
&= \lim_{n\to\infty} \frac{(n-1)(n-2)\cdots(n-k)}{n^k} \\
&= 1
\end{align}
$$

Therefore,

$$
\begin{align}
\lim_{n\to\infty} P_s
&= \sum_{k=0}^{\infty} \frac{(-1)^k}{k!} \\
&= e^{-1} \\
&\approx 0.37
\end{align}
$$


<div style="page-break-after: always;"></div>

## Result

The maximum throughput of slotted ALOHA, as the number of users becomes very large, is

$$
e^{-1} \approx 0.37
$$

So the efficiency of slotted ALOHA is about **37%**.




## Pure ALOHA Performance

In **Pure ALOHA**, a node transmits immediately when it has a frame. There are no synchronized slots.

The key difference is the **vulnerable period**:

- in **Slotted ALOHA**, a frame only collides if another node transmits in the same slot
- in **Pure ALOHA**, a frame can collide with another frame that starts within one packet time **before** or **after** it

So the vulnerable period is **2 packet times** instead of `1`.

<div style="page-break-after: always;"></div>


### Success Probability for One Specific User

For one specific user to succeed in Pure ALOHA:

- that user must transmit, which happens with probability $p$
- no other node may transmit in the packet-time interval before it
- no other node may transmit in the packet-time interval after it

So,

$$
\begin{align}
P(\text{one specific user succeeds})
&= p(1-p)^{n-1}(1-p)^{n-1} \\
&= p(1-p)^{2(n-1)}
\end{align}
$$

### Success Probability for the Whole System

Any one of the $n$ users could be the successful user, so

$$
\begin{align}
P_s
&= np(1-p)^{2(n-1)}
\end{align}
$$

### Maximizing the Pure ALOHA Success Probability

We want to maximize

$$
P_s = np(1-p)^{2(n-1)}
$$

Differentiate with respect to $p$:

$$
\begin{align}
\frac{dP_s}{dp}
&= n\left[(1-p)^{2(n-1)} - 2p(n-1)(1-p)^{2(n-1)-1}\right]
\end{align}
$$

Set the derivative equal to zero and factor:

$$
\begin{align}
0
&= n(1-p)^{2n-3}\big[(1-p)-2p(n-1)\big]
\end{align}
$$

So,

$$
\begin{align}
(1-p)-2p(n-1) &= 0 \\
1-p-2pn+2p &= 0 \\
1+p-2pn &= 0
\end{align}
$$

For large $n$, this gives approximately

$$
p^* \approx \frac{1}{2n}
$$

<div style="page-break-after: always;"></div>

### Behavior as the Number of Users Grows

Substitute the approximate optimum $p^* = \frac{1}{2n}$:

$$
\begin{align}
P_s
&= n\left(\frac{1}{2n}\right)\left(1-\frac{1}{2n}\right)^{2(n-1)} \\
&= \frac{1}{2}\left(1-\frac{1}{2n}\right)^{2(n-1)}
\end{align}
$$

Now let $n \to \infty$:

$$
\begin{align}
\lim_{n\to\infty} P_s
&= \frac{1}{2} e^{-1} \\
&= \frac{1}{2e} \\
&\approx 0.18
\end{align}
$$


So the efficiency of Pure ALOHA is about **18%**, which is worse than Slotted ALOHA because the vulnerable period is twice as large.
