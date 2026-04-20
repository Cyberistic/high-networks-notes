go back to the slides, I will provide a quick refresher only. Not everything is included here cuz it's basic knowledge. Rest of the notes are better I promise


- many paradigms i networks, including client-server and peer-to-peer

| Scale | Type | Example |
| --- | --- | --- |
| Vicinity | PAN (Personal Area Network) | Bluetooth |
| Building | LAN (Local Area Network) | Wi-Fi / Ethernet |
| City | MAN (Metropolitan Area Network) | City-wide fiber / municipal network |
| Country | WAN (Wide Area Network) | Cellular network / ISP backbone |
| Planet | The Internet (network of all networks) | The global Internet |


- VPN is a WAN from virtual links
- RFID is the chip thingy
- a port is a logical (not physical) connection to a computer (there is a table of common ports in the slides)
- a socket links two processes together, you can have a sending, listening (for connections), or receiving socket.
- IPV4 is 4 bytes, IPV6 is 16 bytes (128 bits)
- IP, TCP, UDP, Error correction
- A *repeater* (physical layer) copies ALL bits from one network to another
- a *bridge* (data link layer) copies frames *selectively* by filtering headers
- a *router* (network layer) copies packets from one network to another, also filters by network headers
- a *gateway* (network layer and above) connects stuff together, can encrypt, translate between protocols, act as a router, etc


<div style="page-break-after: always;"></div>


## protocol layers

![[protocol-layers.png | 400]]

- Each protocol instance talks virtually to its peer using a *protocol*

- Each layer communicates only by using the one below, the lower layer provides a *service*

- Lower layer services are accessed by an interface

- At bottom, messages are carried by the medium

- Each layer adds it's own header (control information), and removes the previous layer's headers. Sometimes they split and join messages as well

- Connection vs connection-less services (UDP and TCP)

| Issue | Example mechanisms at different layers |
| --- | --- |
| Reliability despite failures | Codes for error detection/correction<br>Routing around failures |
| Network growth and evolution | Addressing and naming<br>Protocol layering |
| Allocation of resources like bandwidth | Multiple access<br>Congestion control |
| Security against various threats | Confidentiality of messages<br>Authentication of communicating parties |

- The point is that there are some issues that are not wholly the responsibility of any one layer, and they crop up again and again in the text. For example, reliability is often considered a key function of the transport layer (i.e., making transport reliable) yet reliability mechanisms also appear in other layers (error codes in the link layer, routing around failures in the network layer, and replication at the application layer).


<div style="page-break-after: always;"></div>

## OSI

![[OSI.png | 500]]

- Physical layer implements a digital communication link that deliver bits.

- Data link layer implements a packet delivery service between nodes that are attached to the same physical link.

- Network layer guides the packets from their source to their destination, along a path that may comprise a number of links.

- Transport layer supervises the end-to-end transmission of packets. This layer may arrange for retransmission of erroneous packets.

- Session layer users the transmission layer services to set up and supervise connections between end systems.

- Presentation layer takes care of data compression, security, and format conversions so that nodes that user different representations of information can communicate efficiently and securely.

- Application layer implements commonly used communication services including file transfer, directory services, virtual terminal.

**vs TCP/IP model**: In TCP/IP, Session and Presentation layers are skipped and we jump straight to application
