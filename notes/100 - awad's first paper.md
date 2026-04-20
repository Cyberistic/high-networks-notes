yaps about his paper: A Dual-Decomposition-Based Resource Allocation for mpmofmdosdsdjosj soad

available in moodle, and his white board available in teams channel

we covered abstract and "IV. PROBLEM FORMULATION AND PROPOSED SOLUTION"

![ center | 400 ](art.png%20)

## the problem 
it's a resource allocation problem

base station has limited power $P_{BS}$ 
and user #1 is watching a 1080p video, why would we give him bandwidth for a 4k video when he only needs bandwidth for 1080p? wasteful and with multiple users the base station will run out of power even if realistically it should be able to handle the load

so we have to ooga booga spend only the necessary power to each user

we have to define this mathematically

![ center | 300 ](why.png%20)


![ center | 300 ](ofdma.png%20)

look at this beautiful checkerboard. frequency is split into multiple bands. only *ONE* user can use the band x at time *t* (not multiple colors)



basically:
s = subscriber (each user)
$x^s_{n}$ = subscriber s is allocated to the band n
$r^s$ = how much expected bandwidth the subscriber needs
then $U^s(r^s)$ = user satisfaction (like he's satisfied when watching 1080p video and getting 1080p bandwidth -- no lag)
it platues
![ center | 300 ](satis.png%20)

$P^s_{n}$ = how much power the user needs 

then the equation becomes:

![ center | 300 ](eq.png%20)

we want to MAX user satisfaction $U$ for each user $s$ given their expected rate $r$ 
and we have s users and n bands in the frequency

tadaaaa!! from problem statement to maths

<div style="page-break-after: always;"></div>

## does paper matter in exam?

no, but he'll give us a problem in plain english and expect us to somehow turn it into a mathematically defined problem like the above

### more yaps

![ center | 400 ](idk.png%20)

the sum of expected power for all users at given time $t$ must not exceed the total power of the system (احلف؟)
![ center | 300 ](eq2.png%20)

the sum of the expected bandwidth $r$ for all users at given time $t$ must not exceed the total throughput ($c$) of the system (احلف؟)

![ center | 300 ](eq3.png%20)

> [!info] todo: ask dr how the helly we're supposed to do this
