## Software-Defined Networking (SDN)

**Short definition:** SDN is a networking approach where control is done by software in a central controller instead of being embedded separately inside every switch/router.

**SDN** stands for **Software-Defined Networking**.

The main idea is to separate the **control plane** from the **data plane**.

- **control plane** = decides where traffic should go
- **data plane** = actually forwards packets

In traditional networking, both are usually built into each router or switch.

In SDN, the control logic is moved to a **central controller**, while the switches mainly forward traffic according to rules sent by that controller.

![[sdn-1.png | 400]]

<div style="page-break-after: always;"></div>

## SDN vs Traditional Networking

![[sdn-vs-traditional.png | 400]]

### Traditional Networking

In traditional networks:

- each router or switch has its own control plane and data plane
- each device makes forwarding decisions locally
- configuration is often done box-by-box

So the network is more distributed, but also harder to manage as it grows.

### SDN

In SDN:

- the **SDN controller** acts as the control plane
- switches mainly act as forwarding devices in the data plane
- the controller communicates with switches using control messages such as **OpenFlow** messages

instead of every switch providing its own logic, the controller has a wider view of the whole network.

What this means physically:

- traditional networking = each device decides for itself
- SDN = one logical controller tells devices how to behave

<div style="page-break-after: always;"></div>

## Key Advantages

### Centralized Control

SDN controllers manage the entire network from a single point.

This improves:

- efficiency
- automation
- easier network-wide decision making

### Programmability

Network behavior can be modified via APIs.

So the network becomes easier to adapt when requirements change.

### Improved Traffic Management

Dynamic routing can optimize traffic based on real-time conditions.

This helps the network react better to congestion or changing traffic loads.

### Scalability

New devices can be added more easily without complicated manual configuration on every box.

### Cost Reduction

SDN can reduce operational costs by automating tasks that would otherwise require manual configuration.


