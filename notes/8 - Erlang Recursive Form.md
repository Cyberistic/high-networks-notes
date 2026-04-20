

The Erlang B formula is

$$
B(p,c)=\frac{\dfrac{p^c}{c!}}{\sum_{j=0}^{c}\dfrac{p^j}{j!}}
\tag{A}
$$

The recursive form is

$$
B(p,c)=\frac{p\,B(p,c-1)}{c+p\,B(p,c-1)}
\tag{B}
$$

We can write $(A)$ as

$$
\begin{align}
B(p,c)
&= \frac{\dfrac{p^c}{c!}}{\dfrac{p^c}{c!}+\sum_{j=0}^{c-1}\dfrac{p^j}{j!}} \\
&= \frac{\dfrac{p}{c}\left(\dfrac{p^{c-1}}{(c-1)!}\right)}{\dfrac{p^c}{c!}+\sum_{j=0}^{c-1}\dfrac{p^j}{j!}}
\end{align}
$$

> [!Note] Recall:
> $$
> \frac{p^c}{c!} = \frac{p\cdot p^{c-1}}{c\cdot (c-1)!} = \frac{p}{c}\left(\frac{p^{c-1}}{(c-1)!}\right)
> $$
> Also,
> $$
> \sum_{j=0}^{c}\frac{p^j}{j!} = \frac{p^c}{c!} + \sum_{j=0}^{c-1}\frac{p^j}{j!}
> $$
> because we separate the last term of the summation, which occurs at $j=c$.
> This is why the second line rewrites the numerator and also expands the denominator in that form.

Now multiply the fraction by

$$
\frac{1}{\sum_{j=0}^{c-1}\dfrac{p^j}{j!}}\Bigg/\frac{1}{\sum_{j=0}^{c-1}\dfrac{p^j}{j!}}
$$

which is just multiplying by $1$.

$$
\begin{align}
B(p,c)
&= \frac{\dfrac{p}{c}\left(\dfrac{p^{c-1}}{(c-1)!}\right)\times \dfrac{1}{\sum_{j=0}^{c-1}\dfrac{p^j}{j!}}}{\left(\dfrac{p^c}{c!}+\sum_{j=0}^{c-1}\dfrac{p^j}{j!}\right)\times \dfrac{1}{\sum_{j=0}^{c-1}\dfrac{p^j}{j!}}} \\
&= \frac{\dfrac{p}{c}\left(\dfrac{\dfrac{p^{c-1}}{(c-1)!}}{\sum_{j=0}^{c-1}\dfrac{p^j}{j!}}\right)}{\dfrac{\dfrac{p^c}{c!}}{\sum_{j=0}^{c-1}\dfrac{p^j}{j!}}+\dfrac{\sum_{j=0}^{c-1}\dfrac{p^j}{j!}}{\sum_{j=0}^{c-1}\dfrac{p^j}{j!}}} \\
&= \frac{\dfrac{p}{c}\left(\dfrac{\dfrac{p^{c-1}}{(c-1)!}}{\sum_{j=0}^{c-1}\dfrac{p^j}{j!}}\right)}{\dfrac{p}{c}\left(\dfrac{\dfrac{p^{c-1}}{(c-1)!}}{\sum_{j=0}^{c-1}\dfrac{p^j}{j!}}\right)+1}
\end{align}
$$

Notice that

$$
\frac{\dfrac{p^{c-1}}{(c-1)!}}{\sum_{j=0}^{c-1}\dfrac{p^j}{j!}} = B(p,c-1)
$$

So the expression becomes

$$
\begin{align}
B(p,c)
&= \frac{\dfrac{p}{c}B(p,c-1)}{\dfrac{p}{c}B(p,c-1)+1}
\end{align}
$$

Multiply the numerator and denominator by $c$:

$$
\begin{align}
B(p,c)
&= \frac{p\,B(p,c-1)}{p\,B(p,c-1)+c}
\end{align}
$$

Hence,

$$
B(p,c)=\frac{p\,B(p,c-1)}{c+p\,B(p,c-1)}
\tag{B}
$$


.. - / .... .- ... / -... . . -. / .- / .-- .... .. .-.. . / .. / - .-. ..- .-.. -.-- / .... --- .--. . / -.-- --- ..- / .- .-. . / -.. --- .. -. --. / .-- . .-.. .-.. / .-. . -- . -- -... . .-. / - .... .- - / .- .-.. .-.. .- .... / .. ... / .-- .. - .... / -.-- --- ..- / ..-. --- .-. . ...- . .-. / .- -. -.. / .- .-.. .-- .- -.-- ... / -.. --- / -. --- - / ..-. --- .-. --. . - / -- . / .. -. / -.-- --- ..- .-. / .--. .-. .- -.-- . .-. ...