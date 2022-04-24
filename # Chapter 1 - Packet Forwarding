# Chapter 1 - Packet Forwarding

Status: Iniciado
Ultimo Repaso: April 23, 2022
inList: No
inMenu: No
publish: No

# Network Device Communication

- TCP/IP is based on the conceptual *Open System Interconnexion (OSI)* model
    
    ![Untitled](Chapter%201%20-%20Packet%20Forwarding%2015bf1beb161548edae46463f4e414fbb/Untitled.png)
    
- The applications generate data at `Layer 7` and the host sends data down the OSI model.
    
    As the data moves downt the OSI mode, it is **encapsulated** or **modified** as needed.
    
- At `Layer 3`, host decides if the data should be send to another application (on the same device) or needs to be sent to different device.
    
    If is on the same device, data is moved up the stack. If it’s sent to differente device, the device/host continues processing down the OSI model, towards **Layer1**
    
- Modern Multilayer switches (MLSs) normally have `Application-Specific Integrated Circuits (ASICs)`, which can switch (Layer 2) packets “in hardware”.
    
     MLS als performs other Layer 3 functions, like routing. 
    

## Layer 2 Forwarding

- The data link layer (Layer 2) handles local addressing.
- Layer 2 addressing uses a unique source and destination address for segments.
- Ethernet uses *`media access control*(MAC)` addresses
    - Other data link layer protocol such a Frame Relay use an entirely different addressing method.

<aside>
💡 **NOTE**

- A MAC address is `48-bit` long, split in six octets notated in HEX
- The first three octets are assisgned by the manufacturer → OUI
- The last three octets are unique for each NIC (in theory)
- A device only process a frame and moves at Layer 3 level if contains its own MAC as frame destination.
- Network broadcast with MAC FF:FF:FF:FF:FF:FF is the only exception and will be always processed inside the same network segment
- Broadcast are not typically forwarded beyond a Layer 3 boundaries
</aside>

### **Collision Domains**

- Ethernet is a Multiple Access type of network (everyone has to fight for the use of the medium)
- Ethernet networks uses *`Carrier Sense Multiple Access/Collision Detect (CSMA/CD)`* method  to ensure only one device talks at time in a ***`collision domain`***.
    - CSMA/CD means if a device detects that another is transmitting data, it delays transmitting until the cable is quite.
- The communications in a collision domain is `half-duplex`.

<aside>
🔥 **KEY TOPIC:**

- As more devices are added to a collision domain, less efficient the network becomes.
- Networks hubs expands a collision domain.
- Hubs were devices without any intelligence, they simple repeat traffic out of every port
</aside>

- Network switches create virtual channels.
- A switch maintains a table that associates a host’s MAC addresses to the port that sourced the traffic.
- A switch uses the local `MAC address table` to forward network traffic only to the port associated with where the `destination` MAC is attached.
- A switch learns from the `source` MAC and forwards based on the `destination` MAC.
- A network switch works in full duplex.
- Hub Vs Switch Collision Domains:

![Untitled](Chapter%201%20-%20Packet%20Forwarding%2015bf1beb161548edae46463f4e414fbb/Untitled%201.png)

- Communication between PC-A and PC-B is received by PC-C
- PC-C must process the frame (consuming resources), then discards the frame
- PC-C has to wait until PC-A and PC-B conversation finishes

![Untitled](Chapter%201%20-%20Packet%20Forwarding%2015bf1beb161548edae46463f4e414fbb/Untitled%202.png)

- The switch can connect two collision domains by using the MAC address table
- *Unknown unicast flooding*
    
    When the switch doesn’t have the destination MAC address on its table, it forwards the frame on every switch port, except were it was received.
    
- Broadcast traffic causes communication between network devices to stop due CSMA/CD (that’s why needs to be avoided/reduced)
- Broadcast traffic do not cross Layer 3 boundaries. (subnet to subnet)
- All devices on the same Layer 2 segment are considered to be in the same broadcast domain.

### Virtual LANs

- Adding a router between LAN segments helps shrink broadcast domain.

<aside>
🔥 **KEY TOPIC:**

- Virtual LANs (VLANs)
    
    Provides logical segmentation by creating multiple broadcast domains on the same network switch
    
- With VLANs, multiple broadcast domains can reside on the same switch
- Network devices in one VLAN cannot communicate with devices in a different VLAN via Layer 2 (or broadcast)
</aside>

- VLANs are defined in the `IEEE 802.1Q standard`
    
    
- IEEE 802.1Q adds a `32 bit`s header to the original Ethernet frame, between the `source MAC address` and the `EtherType` fields.
    
    ![https://upload.wikimedia.org/wikipedia/commons/thumb/0/0e/Ethernet_802.1Q_Insert.svg/1328px-Ethernet_802.1Q_Insert.svg.png](https://upload.wikimedia.org/wikipedia/commons/thumb/0/0e/Ethernet_802.1Q_Insert.svg/1328px-Ethernet_802.1Q_Insert.svg.png)
    
- 802.1Q tag format
    
    ![Untitled](Chapter%201%20-%20Packet%20Forwarding%2015bf1beb161548edae46463f4e414fbb/Untitled%203.png)
    
- 802.1Q tag fields:
    
    
    | Field Name | Size | Description |
    | --- | --- | --- |
    | TPID (Tag protocol identifier) | 16 bits | set to 0x8100 to identify the frame as a 802.1Q, this field is located at the same position as EtherType field in untagged frames, and is used to distinguish the frame from untagged frames.  |
    | PCP (Priority code point) | 3 bits | Indicates a class of service (CoS) for the frame (IEEE 802.1p). Different PCP values can be used to prioritize different class of traffic. |
    | DEI (Drop elgible indicator) | 1 bit | Indicates whether the frame can be dropped when there is congestion. May be used separately or in conjunction with PCP. |
    | VLAN identifier (VID) | 12 bits | Specifies the VLAN associated with the frame. |
- PCP, DEI, and VLAN ID fields sometimes are referred as subfields of the TCI field (Tag control information)
- 12 bits for VID provides 4094 unique VLAN numbers
    - VID value 0x000 is only used for 802.1p traffic
    - VID value 0xFFF is reserved
- On Cisco Catalyst:
VLAN `1` is the default VLAN and cannot be modified or deleted
VLAN `2 to 1001` are in the normal VLAN range
VLAN `1002 to 1005` are reserved and cannot be delete
VLAN `1006 to 4094` are in the extended VLAN range
    
    VID value 0x000 and 0xFFFF are not used.
    

**VLANs creation:** 

- To create a VLAN use the **global configuration** command`vlan*vlan-id*`
    
    ![Untitled](Chapter%201%20-%20Packet%20Forwarding%2015bf1beb161548edae46463f4e414fbb/Untitled%204.png)
    

**VLAN verification**

- VLANs and their port assignment are verified with the `show vlan [{brief|id*vlan-id*|name*vlanname*|summary}]` command
    
    ![Untitled](Chapter%201%20-%20Packet%20Forwarding%2015bf1beb161548edae46463f4e414fbb/Untitled%205.png)
    
- `show vlan brief` displays only the relevant port-to-VLAN mappings
    
    ![Untitled](Chapter%201%20-%20Packet%20Forwarding%2015bf1beb161548edae46463f4e414fbb/Untitled%206.png)
    
- `show vlan summary` displays a count of VLANS, VLANS participating in VTP, and VLANs that are in the extended VLAN range.
    
    ![Untitled](Chapter%201%20-%20Packet%20Forwarding%2015bf1beb161548edae46463f4e414fbb/Untitled%207.png)
    
- `show vlan id*vlan-id*` displays all the output from the original command but filtered to only the VLAN specified (by VLAN id)
    
    ![Untitled](Chapter%201%20-%20Packet%20Forwarding%2015bf1beb161548edae46463f4e414fbb/Untitled%208.png)
    
- `show vlan name*vlanname`* displays all the output from the original command but filtered to only the VLAN specified (by VLAN name)
    
    ![Untitled](Chapter%201%20-%20Packet%20Forwarding%2015bf1beb161548edae46463f4e414fbb/Untitled%209.png)
    
- `show vlan` and `show vlan brief` commands doesn’t show the trunk ports, `show vlan id*vlan-id*` and `show vlan name*vlanname*` commands shows only the ports where the VLANs is currently active **including** **trunk** ports.

![Untitled](Chapter%201%20-%20Packet%20Forwarding%2015bf1beb161548edae46463f4e414fbb/Untitled%2010.png)

![Untitled](Chapter%201%20-%20Packet%20Forwarding%2015bf1beb161548edae46463f4e414fbb/Untitled%2011.png)

### Access Port

<aside>
🔥 **KEY TOPIC**

- An access port is assigned to only one VLAN.
- The 802.1Q tags are not included on frames transmitted or received on access ports.
</aside>

- Catalyst switches place switch **ALL** ports as `Layer 2 access ports` for `VLAN 1` by default.
- Configuring and Access Port
    - `switchport mode access` command is used to manually configure a port as an access port
    - `switchport access {vlan vlan-id | name vlanname}` command is used to associate a port with and specific VLAN
    
    ![Untitled](Chapter%201%20-%20Packet%20Forwarding%2015bf1beb161548edae46463f4e414fbb/Untitled%2012.png)
    

### 🌶️ Trunk Ports

- *Trunk ports* are used in a switch to connect another switch, router, firewall, or server (with a virtual switch) and carry multiple VLANs traffic in a single cable.
- Configuring a Trunk Port
    - `switchport mode trunk` command is used to statically define a port as trunk
    
    ![Untitled](Chapter%201%20-%20Packet%20Forwarding%2015bf1beb161548edae46463f4e414fbb/Untitled%2013.png)
    
- Verifying a Trunk Port
    - `show interface trunk` command is very useful to verify and troubleshoot *trunk ports*
    
    ![Untitled](Chapter%201%20-%20Packet%20Forwarding%2015bf1beb161548edae46463f4e414fbb/Untitled%2014.png)
    
- Native VLANs
    
    ![Untitled](Chapter%201%20-%20Packet%20Forwarding%2015bf1beb161548edae46463f4e414fbb/Untitled%2015.png)
    
    - `switchport trunk native vlan*vlan-id`* is the command used to change the native vlan in an specific port.
    - All switch control plane traffic is advertised using VLAN 1
    - You should change the native VLAN to something else than 1, it should be set to a VLAN that you’re not using (dummy VLAN)
- Allowed VLANS
    - Trunk ports can be restricted to allow only specific VLANS (traffic engineering)
    - This can also cause some problems if is not done carefully
    - `switchport trunk allowed {*vlan-ids*| all | none | add*vlan-ids*| remove*vlan-ids*| except*vlan-ids*}`
        - `*vlan-ids*` option substitute the current vlan list allowed in the port with the ones specified in the command (be carefull).
        - `all` allows all the VLANs on the switch
        - `none` remove all the VLANs
        - `add*vlan-ids`* add the specified VLANs to those already allowed in the port
        - `remove*vlan-ids*` remove the specified VLANs from the VLANs already allowed in the port.
        - `except*vlan-ids*`  regardless which VLANs are currently allowed in the port, includes ALL VLANs except the ones specified.

### Layer 2 Diagnostic Commands

- MAC Address Table
    - `show mac address-table [address*mac-address*| dynamic | vlan*vlan-id*]` is the command used to display de MAC address table
        - `address*mac-address`* Display entries that match the explicit MAC address
        - `dynamic`  Shows only the MAC address dynamically learned (not statically set)
        - `vlan*vlan-id`* Shows the entries for a specific VLAN
    - In multiple MAC address entries appear on the same port, then another switch, hub, or virtual switch it’s connected in that port.
    - `mac address-table static*mac-address* vlan*vlan-id* {drop | interface*interface-id*}` command adds a manual entry (static) on the MAC address table, allowing to associate to a specific port, or to drop traffic upon receipt.
        - `clear mac address-table dynamic [{address*mac-address*| interface*interface-id*| vlan*vlan-id*}]` command is used to clear the entire MAC address table or, only to remove a specific address or, all the MAC associated with a specific VLAN or interface.
    - 🔥 The MAC address table resides in *content addressable memory* (CAM)
        - CAM is faster than the typical computer RAM memory (1 clock-cycle search)
        - A Binary CAM (BCAM) provides a search result of 0 for true or 1 for false (and the memory location)
        - A Binary CAM has a Search Line(1bit) and a Match Line (1bit) for every word bit. (we are moving to the electronics arena here!!!)
        
        ![Untitled](Chapter%201%20-%20Packet%20Forwarding%2015bf1beb161548edae46463f4e414fbb/Untitled%2016.png)
        
        - A Ternary CAM (TCAM) can provide a third value “X” which means *don’t care,* and is used as a wildcard to provide more faster switching mechanisms.
        - More good stuff here: [Link 1](https://etherealmind.com/basics-what-is-content-addressable-memory-cam/), [Link 2](http://movingpackets.net/2016/07/06/response-cam-table-basics/), [Link 3](https://www.pagiamtzis.com/pubs/pagiamtzis-jssc2006.pdf)
- Switch Port Status
    - Instead of looking for the configuration for a switch port, sometimes it´s more useful to check the real status of the switch port.
    - `show interfaces*interface-id*switchport` command shows the real current status of the switchport.
    - `show interfaces switchport` displays the same but for all the switchports.
    
    ![Untitled](Chapter%201%20-%20Packet%20Forwarding%2015bf1beb161548edae46463f4e414fbb/Untitled%2017.png)
    
- Interface Status
    - `show interface status` command is useful for viewing the status of switchports in a condensed way.
    
    ![Untitled](Chapter%201%20-%20Packet%20Forwarding%2015bf1beb161548edae46463f4e414fbb/Untitled%2018.png)
    

## Layer 3 Forwarding

- Two main methodologies for Layer 3 forwarding:
    - Forwarding traffic to devices on the same subnet
    - Forwarding traffic to devices on different subnets

### Local Network Forwarding

- Address Resolution Protocol (ARP) provides a method of mapping Layer 3 IP addresses to Layer 2 MAC addresses.
- ARP table contains IP addresses and their corresponding MAC Address.
- ARP does not contain entries for devices on a remote network but contains ARP entry for the IP of the next hop.
- ARP request are broadcast messages and contain the IP address of the unknown devices.
- ARP response it’s a unicast message. IP owner responded with their IP and MAC Address.
- ARP entries are removed if no communication occurs with the host during a length of time.
- `show ip arp [*mac-address*| *ip-address*  vlan *vlan-id*| *interface-id*]` command is used to view the ARP table on a Router

### Packet Routing

- Routers learn routes in several ways:
    - Static route entry
    - Default next-hop entry
    - Routing protocols
- Routers also have ARP tables and send ARP requests to find the MAC address of the destination.
- What a router do when receives a packet:
    1. Receives the packet based on the destination MAC
    2. Analyze the destination IP address
    3. Locates the appropriate network entry on its routing table.
    4. Identifies the outbound interfaces (if there is a match on the routing table)
    5. Modifies the source MAC address to the MAC address of his own interface.
    6. Looks for the destination MAC address on his ARP table
    7. Modifies the destination MAC, and sends the packet.

### IP Address Assignment

- `ip address*ip-address subnet-mask`* command is used to assign a IPv4 address to an interface.
- An interface with an IPv4 address AND that is in an up state injects a network into the routing table, as a connected route.
- Connected routes have AD zero (0)
- **Routing Information Base**, another way to call the router Routing Table.
- **Secondary IPv4 address on an interface:**
    - `ip address ip-address subnet-mask secondary` assign a “secondary” address on an interface
    - You can have multiple “secondary” address, but only one “primary” address.
    - To remove the “primary” address, you should remove all the “secondary” first.
    - If you don't add the `secondary` option in the command, the IPv4 address is overwritten.
    - Why would you need a secondary IP address on an interface:
        
        > According with Cisco”
        The optional keyword **secondary** allows you to specify an unlimited number of secondary addresses. Secondary addresses are treated like primary addresses, except the system never generates datagrams other than routing updates with secondary source addresses. IP broadcasts and ARP requests are handled properly, as are interface routes in the IP routing table.
        > 
        > 
        > Secondary IP addresses can be used in a variety of situations. The following are the most common applications:
        > 
        > - There may not be enough host addresses for a particular network segment. For example, your subnetting allows up to 254 hosts per logical subnet, but on one physical subnet you need to have 300 host addresses. Using secondary IP addresses on the routers or access servers allows you to have two logical subnets using one physical subnet.
        > - Many older networks were built using Level 2 bridges. The judicious use of secondary addresses can aid in the transition to a subnetted, router-based network. Routers on an older, bridged segment can be easily made aware that there are many subnets on that segment.
        > - Two subnets of a single network might otherwise be separated by another network. This situation is not permitted when subnets are in use. In these instances, the first network is *extended*, or layered on top of the second network using secondary addresses.
        > 
        > ---
        > 
        > **Note**
        > 
        > If any router on a network segment uses a secondary address, all other devices on that same segment must also use a secondary address from the same network or subnet. Inconsistent use of secondary addresses on a network segment can very quickly cause routing loops.
        > 
    
- `ipv6 address *ipv6-address/prefix-length`* command to add an IPv6 to an interface
    - Command can be repeated multiple times to add multiple IPv6 address to the same interface
- **Routed Subinterfaces**
    - Physical router interface connected to a trunk port, needs logical subinterfaces (one for each VLAN in the trunk)
    - VLANs are associated with the subinterface with the command `encapsulation dot1q vlan-id`
    
    ![Untitled](Chapter%201%20-%20Packet%20Forwarding%2015bf1beb161548edae46463f4e414fbb/Untitled%2019.png)
    
- Switched Virtual Interfaces (SVIs)
    - SVI or VLAN interface can be created on a switch and a IP address can be assigned
    - The switch must have an interface associated to the VLAN in *up* state, for the SVI to be in an *up* state.
    - On a Mult iLayer Swtich, SVIs can be used to routing packets.
    
- Routed Switch Ports
    - Command `no switchport` can be used to convert a Layer 2 port on a switch to a routed (L3) port. So you can assign an IP address.
    - Some network engineers and vendors, instead, define a transit VLAN, create SVI for that VLAN and then assign an interface for that VLAN. Some things to consider on this approach:
        - VLAN could exist elsewhere in the Layer 2 realm
        - Spanning tree could impact the topology. Because your extending the Spanning Tree no another switch.

### Verification of IP Address

- `show ip interface [brief | interface-id |vlan vlan-id]` command shows MTU, DHCP relay, ACLs, and the primary IP address.
- `brief` option shows in more condensed way
- You can parse the output with `| exclude` field, to reduce unnecessary data.
- `show ipv6 interface [brief | interface-id | vlan vlan-id]` command shows the same for IPv6

# Forwarding Architecture

- Today’s router don't remove the L2 information, verify routes and add L2 headers again (3 steps), they do everything is one single step.
- **IP Packet switching or IP packet forwarding:** The process of receiving an IP packet on an input interface and making a decision about whether to forward the packet on an output interface or drop it.
- Process switching evolves to *fast switching* to Cisco Express Forwarding (CEF)

## Process Switching

- Oldest method for Cisco IOS Switching
- Also referred as *software switching* or *slow path*
- Every packet is inspected a general-purpose CPU
- `ip_input`process is in charge of process switching.
- Process switching is the fallback for CEF
- “Punted packets” are sent to CPU because cannot be switched by CEF.
- Routers uses process switching for:
    - Packets sourced or destined to the router (SSH/TELNET, control traffic, routing protocols)
    - Packets that are too complex (IP packets with IP options)
    - Packets that requires extra information (e.g. ARP)
        
        ![Untitled](Chapter%201%20-%20Packet%20Forwarding%2015bf1beb161548edae46463f4e414fbb/Untitled%2020.png)
        

### Cisco Express Forwarding

- Cisco proprietary switching mechanism.
- There are two types of routers:
    - Software-based routers
        - general-purpose CPU (in charge of everything)
        - Uses CEF as their default packet switching mechanism since the 1990s —> Software CEF
    - Hardware-based routers
        - general-purpose CPU
        - Forwarding Engines implemented in:
            - Application-specific integrated circuits (ASICs)
            - Network processing units (NPUs)
            - Ternary content addressable memory (TCAM)
        - CEF it’s their default switching mechanism —> Hardware CEF

---

I didn’t continue taking notes on this Chapter, it was taking me to mucho time. I need to consider another approach to study more effectively.

### Ternary Content Addressable Memory

### Centralized Forwarding

### Distributed Forwarding

## Software CEF

## Hardware CEF

## Stateful Switchover

## SDM templates

[https://www.ciscopress.com/articles/article.asp?p=101629&seqNum=4#:~:text=TCAM allows a packet to,or Layer 3 forwarding decision](https://www.ciscopress.com/articles/article.asp?p=101629&seqNum=4#:~:text=TCAM%20allows%20a%20packet%20to,or%20Layer%203%20forwarding%20decision).

## Process Switching

## Cisco Express Forwading

- Turned on by default

```jsx
ip cef
```

- CEF contains two different tables:
    - CEF Forwarding Information Base
        - Similar to Routing Table
        - When the routing table is updated, the FIB is also updated
        - It's a very efficient route look-up source, where the processor is not involved
        - Layer 3 information
        - show ip cef
            - Next Hop
            - attached
            - receive
            - drop
    - CEF Adjacency Table
        - Information about directly connected devices (next-hop)
        - Adjacency = reachable via single link-layer hop
        - Layer 2 information
        - show adjacency detail
    
    ## DITKA questions
    
    [DITKA Chapter1](https://www.notion.so/bad71ed76333490a9ffcb3993a77afbd)
