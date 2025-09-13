# Inter-VLAN Routing implementation using Multilayer Switches
Inter-VLAN Routing with a Layer 3 Switch
This repository contains a Packet Tracer project that demonstrates a fundamental network topology using inter-VLAN routing with a Layer 3 switch. The goal of this project is to showcase the ability to logically segment a network using VLANs and enable communication between them.

Project Highlights
This project implements several key networking concepts:

VLANs: The network is segmented into three separate Virtual Local Area Networks (VLANs) to improve security and performance.

Layer 3 Switching: A multilayer switch is used as the central point for routing traffic between the different VLANs.

Trunking: The links connecting the access switches to the multilayer switch are configured as trunks to carry traffic from all three VLANs.

EtherChannel: Link aggregation is used to bundle multiple physical links into a single logical link, providing increased bandwidth and redundancy.

LACP: The Link Aggregation Control Protocol is used to automatically manage the EtherChannel bundles.

Network Topology
The network is designed with three VLANs, each with its own subnet and a default gateway configured on the multilayer switch.

VLAN 10: 192.168.1.0/24

VLAN 20: 192.168.2.0/24

VLAN 30: 192.168.3.0/24



Configuration Details
The following table provides a high-level overview of the network configuration.

End Devices
Device

VLAN

IP Address

Network

Default Gateway

Connected Switch

Port

PC0

10

192.168.1.2/24

192.168.1.0/24

192.168.1.1

Switch_A

Fa0/1

PC1

10

192.168.1.3/24

192.168.1.0/24

192.168.1.1

Switch_A

Fa0/2

PC2

20

192.168.2.2/24

192.168.2.0/24

192.168.2.1

Switch_B

Fa0/1

PC3

20

192.168.2.3/24

192.168.2.0/24

192.168.2.1

Switch_B

Fa0/2

PC4

30

192.168.3.2/24

192.168.3.0/24

192.168.3.1

Switch_A

Fa0/5

PC5

30

192.168.3.3/24

192.168.3.0/24

192.168.3.1

Switch_A

Fa0/6

Switches
Switch

Connected Device

Ports

Trunk Links

Allowed VLANs

Switch_A

MultilayerSwitch_A

Fa0/3, Fa0/4

Port-channel 1

10, 20, 30

Switch_B

MultilayerSwitch_A

Fa0/3, Fa0/4

Port-channel 2

10, 20, 30

MultilayerSwitch_A

Switch_A & Switch_B

Fa0/1, Fa0/2, Fa0/3, Fa0/4

Port-channel 1 & 2

10, 20, 30

Getting Started
To view and interact with this project:

Download and install Cisco Packet Tracer.

Clone this repository to your local machine.

Open the .pkt file in Packet Tracer.

Feel free to explore the configurations on each device and test connectivity using ping commands between different hosts.

Contributing
Suggestions and improvements are welcome! If you have ideas on how to enhance this project, feel free to open an issue or submit a pull request.
