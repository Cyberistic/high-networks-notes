yaps about his paper: Energy-aware blahblah SDN bender shmender

available in moodle, and his white board available in teams channel




![[sdn.png | 500]]
lots of SDN talk.

To achieve these energy savings, he use **Software-Defined Networking (SDN)**:
	Traditional networks have the decision-making logic baked into every single router. SDN changes this by separating the "Control Plane" (the brain making routing decisions) from the "Data Plane" (the hardware forwarding the data).
    
talks about **Mininet** (a network emulator) and **Ryu** or **ONOS** (types of SDN controllers).
    
- Because the central controller has a view of all traffic, it can make smart, network-wide decisions to pack traffic onto specific paths, allowing unused links to be put to sleep or powered down


<div style="page-break-after: always;"></div>


## the problem

Similar to first paper, it's a resource allocation problem:
how to significantly reduce the energy consumed by wired computer networks while still reliably delivering all required data.

find Best path s.t.: **no congestion, fast delivery, no delay, no packet loss, and integrity of flowtable**.


    

![[paper2.png | 400]]


This image shows **Flow Conservation**: the node "$e$" and arrows pointing in and out represents "flow conservation." Simply put, the amount of data traffic entering a router must equal the amount of traffic leaving it, unless that router is the final destination.


![[paper2-1.png | 400]]
- This image shows **Discrete Link Rates**: data flows (like $f=1$ and $f=2$) travel across nodes. Look at the red graph in the bottom right. This shows that network links don't consume power linearly; they operate at **discrete link rates** (like 100 Mbps, 1 Gbps, 10 Gbps), and each jump in speed requires a step up in power (Watts). tl;dr: more speed = more power
    

<div style="page-break-after: always;"></div>


### The Solution

Calculating the most energy-efficient routes while dealing with these discrete "step" speeds is NP-complete. If you try to solve it perfectly using brute-force math software (dr mentioned "GAMS" and "CPLEX"), it can take hours.

To fix this, he created a **Heuristic Algorithm** based on a mathematical trick called **Benders Decomposition**. Instead of trying to solve the massive, complex problem all at once, their algorithm breaks it into smaller, relaxed problems. It quickly finds a near-perfect routing path that minimizes energy consumption while satisfying the data demands.


To achieve "no congestion" and "no packet loss," the algorithm mathematically ensures that the capacity of the activated discrete link rate ($\overline{r}_l$) is always strictly greater than or equal to the actual traffic flowing through it ($r_l$). By using "integral routing" (sending a whole flow down a single path rather than splitting it up), the algorithm prevents packets from arriving out of order, which helps ensure fast delivery and minimal delay.


<div style="page-break-after: always;"></div>

### What matters in exam

You are given a paragraph like this (but hopefully simpler plz):
![[long-para.png]]

need to turn it into a set of defined variables: 
![[variables.png | 500]]

<div style="page-break-after: always;"></div>

so you can finally turn it into a math form with constraints:

![[long-para-math.png]]

<div style="page-break-after: always;"></div>


gemini explanation of the math slop soup:

For your task of translating a resource-allocation problem into its mathematical form, the most relevant part of this paper is **Section II: Network Model and Problem Formulation**. Specifically, the original optimization problem is encapsulated in **Equations (5a) through (5d)**.

Here is the exact mathematical formulation extracted from the paper:

### Objective Function

The goal of the problem is to minimize the total energy consumption across all links in the network:

$$min\sum_{l=1}^{L}\Gamma_{l}(\overline{r}_{l})$$

### Constraints

The problem is bound by three main constraints:

- **Total Link Rate:** The rate on any given link $l$ must equal the sum of the rates of all flows $f$ utilizing that link:
    
    $$r_{l}=\sum_{f\in\mathcal{F}}r_{l}^{f} \quad \forall l\in\mathcal{L}$$
    
- **Flow Conservation:** This ensures that traffic entering a forwarding element equals the traffic leaving it, unless the element is the origin or destination of the flow:
    
    $$\sum_{l\in\mathcal{L}_{e}}r_{l}^{f}-\sum_{l\in\mathcal{L}_{e}^{-}}r_{l}^{f}=\begin{cases}0&f\in\mathcal{F},e\in\mathcal{E},e\ne o(f), e\ne d(f)\\ r^{f}&f\in\mathcal{F},e=o(f)\\ -r^{f}&f\in\mathcal{F},e=d(f)\end{cases}$$
    
- **Discrete Link Rate Allocation:** The continuous required rate $r_{l}$ must be mapped to one of the available discrete operating rates $\overline{r_{l}}$ provided by the hardware:
    
    $$\overline{r_{l}}=\begin{cases}R_{0}&0<r_{l}\le R_{0}\\ R_{1}&R_{0}<r_{l}\le R_{1}\\ \vdots& \\ R_{max}&R_{max-1}<r_{l}\le R_{max}\end{cases} \quad \forall l\in\mathcal{L}$$
    

(Note: Later in Section III, the authors rewrite this into a relaxed "Benders decomposition" format to actually solve it, but if you only need the core mathematical representation of the problem itself with its direct constraints, Equations 5a-5d are exactly what you are looking for).