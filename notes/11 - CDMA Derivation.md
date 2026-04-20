
## CDMA Idea

In CDMA, each user is assigned a code made of several **chips**.

**Code as chips:**

```
Code

      +1      +1
      ___     ___
     |   |   |   |
_____|   |___|   |___
        -1      -1

<-------- 4 chips -------->
```

If two users have orthogonal codes $S$ and $T$, then

$$
S \cdot T = \frac{1}{m}\sum_{i=1}^{m} S_i T_i = 0
$$

where $m$ is the number of chips in the code.

> [!Note] Recall:
> Two codes are **orthogonal** if, when we compare them chip by chip, the positive and negative products cancel each other out.
> $$
> S \cdot T = \frac{1}{m}\sum_{i=1}^{m} S_i T_i = 0
> $$
> Here is the idea:
> - If two chips are the same sign, their product is `+1`.
> - If two chips are opposite signs, their product is `-1`.
> - For orthogonal codes, the total number of `+1` products and `-1` products balances so the sum is `0`.
>
> So orthogonal does **not** mean the codes are identical. It means they are arranged so that, overall, they have zero similarity.
>
> This is why CDMA works: when the receiver decodes using one user's code, any other user's orthogonal code contributes a total of `0`, so it does not affect the final result.

<div style="page-break-after: always;"></div>

The code also satisfies:

$$
S \cdot S = \frac{1}{m}\sum_{i=1}^{m} S_i S_i = \frac{1}{m}\sum_{i=1}^{m} S_i^2 = 1
$$

and the complement of the code satisfies:

$$
S \cdot (-S) = -1
$$

This means:

- the code matched with itself gives $1$
- the code matched with its complement gives $-1$
- the code matched with an orthogonal user gives $0$


<div style="page-break-after: always;"></div>

## Example

Assume we use 4-chip codes.

### Chip sequences

Station A uses

$$
A = [+1,-1,+1,-1]
$$

```
A:

      +1      +1
      ___     ___
     |   |   |   |
_____|   |___|   |___
        -1      -1
```

Station B uses

$$
B = [+1,+1,-1,-1]
$$

```
B:

      +1  +1
      ______
     |      |
_____|      |________
            -1  -1
```

Station C uses

$$
C = [+1,-1,-1,+1]
$$

```
C:

      +1          +1
      ___         ___
     |   |       |   |
_____|   |_______|   |___
        -1  -1
```

These codes are orthogonal.

For example,

$$
\begin{align}
A \cdot B &= \frac{1}{4}\big[(+1)(+1)+(-1)(+1)+(+1)(-1)+(-1)(-1)\big] \\
&= \frac{1}{4}(1-1-1+1) \\
&= 0
\end{align}
$$

Similarly, $A \cdot C = 0$ and $B \cdot C = 0$.


<div style="page-break-after: always;"></div>

## Sending Data

Suppose:

- Station A sends bit `1`
- Station B sends bit `0`
- Station C sends nothing

In this example:

- bit `1` means send the code itself
- bit `0` means send the complement of the code
- sending nothing means send all zeros

So the transmitted chip streams are:

$$
\text{A sends } [+1,-1,+1,-1]
$$

```
      +1      +1
      ___     ___
     |   |   |   |
_____|   |___|   |___
        -1      -1
```

$$
\text{B sends } [-1,-1,+1,+1]
$$

```
                +1  +1
                ______
               |      |
_______________|      |____
      -1  -1
```

$$
\text{C sends } [0,0,0,0]
$$

```
_________________________
  0    0    0    0
```


<div style="page-break-after: always;"></div>

## Combined Signal

The channel adds all users' transmitted chip values together:

$$
\begin{align}
\text{Signal}
&= [+1,-1,+1,-1] + [-1,-1,+1,+1] + [0,0,0,0] \\
&= [0,-2,+2,0]
\end{align}
$$

So the received combined signal is

$$
[0,-2,+2,0]
$$


<div style="page-break-after: always;"></div>

## Detection

To recover one user's data, take the dot product of the received signal with that user's code and divide by the number of chips.

### Detecting A

$$
\begin{align}
\text{Data for A}
&= \frac{[0,-2,+2,0] \cdot [+1,-1,+1,-1]}{4} \\
&= \frac{0(+1)+(-2)(-1)+(+2)(+1)+0(-1)}{4} \\
&= \frac{0+2+2+0}{4} \\
&= 1
\end{align}
$$

So A sent binary `1`.

### Detecting B

$$
\begin{align}
\text{Data for B}
&= \frac{[0,-2,+2,0] \cdot [+1,+1,-1,-1]}{4} \\
&= \frac{0(+1)+(-2)(+1)+(+2)(-1)+0(-1)}{4} \\
&= \frac{0-2-2+0}{4} \\
&= -1
\end{align}
$$

So B sent binary `0`.

### Detecting C

$$
\begin{align}
\text{Data for C}
&= \frac{[0,-2,+2,0] \cdot [+1,-1,-1,+1]}{4} \\
&= \frac{0(+1)+(-2)(-1)+(+2)(-1)+0(+1)}{4} \\
&= \frac{0+2-2+0}{4} \\
&= 0
\end{align}
$$

So C did not send any data.


## Summary

CDMA works because orthogonal codes do not interfere when we decode with the correct code:

- result `1` means the user sent bit `1`
- result `-1` means the user sent bit `0`
- result `0` means the user was silent


<div style="page-break-after: always;"></div>

## Maximum Number of Stations

If the channel uses codes of length $N$ chips, then the maximum number of mutually orthogonal stations is:

$$
\text{Max stations} = N
$$

This is because each station needs its own orthogonal code, and with code length $N$, we can construct at most $N$ orthogonal code vectors.

So in CDMA:

- an $N$-chip code can support at most $N$ stations
- each station is assigned one unique orthogonal code
- if we try to add more than $N$ stations, the extra codes will no longer all be orthogonal



a channel using 8-chip codes can support up to 8 orthogonal stations, a channel using 16-chip codes can support up to 16 orthogonal stations, and so on.

> [!Note] In practice, with loss/noise:
> The value $N$ is the **ideal** maximum, assuming perfectly orthogonal codes and perfect reception.
> In a real channel, attenuation, noise, interference, and imperfect synchronization reduce performance.
> This means the **practical** number of stations is usually **less than $N$**.
>
> So:
> - ideal case: maximum stations $= N$
> - lossy/noisy case: maximum stations $< N$
>
> The exact number depends on how much interference and distortion the receiver can still tolerate while decoding correctly.

IF TALEB AND THE DR SAY NUM OF CHANNELS =/= NUM OF BITS, THEY ARE WRONG!! DO NOT LISTEN TO THEM TRUST ME THEY ARE JUST TRYING TO CONFUSE YOU. THEY ARE SENT BY THE CDMA CORPORATION TO SELL MORE BITS.

