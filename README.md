# Inter-VLAN Routing implementation using Multilayer Switches
# Inter-VLAN Routing with a Layer 3 Switch

## Project Highlights
This project demonstrates several key networking concepts:
* **VLANs**: The network is segmented into three separate Virtual Local Area Networks (VLANs) to improve security and performance.
* **Layer 3 Switching**: A multilayer switch is used as the central point for routing traffic between the different VLANs.
* **Trunking**: The links connecting the access switches to the multilayer switch are configured as trunks to carry traffic from all three VLANs.
* **EtherChannel**: Link aggregation is used to bundle multiple physical links into a single logical link, providing increased bandwidth and redundancy.
* **LACP**: The Link Aggregation Control Protocol is used to automatically manage the EtherChannel bundles.

## Network Topology
The network is designed with three VLANs, each with its own subnet and a default gateway configured on the multilayer switch.

**VLAN 10**: `192.168.1.0/24` | **VLAN 20**: `192.168.2.0/24` | **VLAN 30**: `192.168.3.0/24`

![Network Topology Diagram](topology.png)

## Configuration Details

### End devices
| Device | VLAN | IP address | Network | Default Gateway | Connected Switch | Access port |
|---|---|---|---|---|---|---|
| PC0 | 10 | 192.168.1.2/24 | 192.168.1.0 /24 | 192.168.1.1/24 | Switch_A | Fa0/1 |
| PC1 | 10 | 192.168.1.3/24 | 192.168.1.0 /24 | 192.168.1.1/24 | Switch_A | Fa0/2 |
| PC2 | 20 | 192.168.2.2/24 | 192.168.2.0 /24 | 192.168.2.1/24 | Switch_B | Fa0/1 |
| PC3 | 20 | 192.168.2.3/24 | 192.168.2.0 /24 | 192.168.2.1/24 | Switch_B | Fa0/2 |
| PC4 | 30 | 192.168.3.2/24 | 192.168.3.0 /24 | 192.168.3.1/24 | Switch_A | Fa0/5 |
| PC5 | 30 | 192.168.3.3/24 | 192.168.3.0 /24 | 192.168.3.1/24 | Switch_A | Fa0/6 |

### Switches
| Switch | Connected device | Switch port |
|---|---|---|
| Switch_A | MultilayerSwitch_A | Fa0/3, Fa0/4 |
| Switch_B | MultilayerSwitch_A | Fa0/3, Fa0/4 |

### MultilayerSwitch_A
| Switch | Switch port |
|---|---|
| Switch_A | Fa0/1, Fa0/2 |
| Switch_B | Fa0/3, Fa0/4 |

### Etherchannel
| Port-channel | Switches | Ports | Mode |
|---|---|---|---|
| 1 | Switch_A | Fa0/3, Fa0/4 | LACP - Active |
| | MultilayerSwitch_A | Fa0/1, Fa0/2 | |
| 2 | Switch_B | Fa0/3, Fa0/4 | LACP - Active |
| | MultilayerSwitch_A | Fa0/3, Fa0/4 | |

### Trunk Links
| Switch | Trunk | Allowed VLANs |
|---|---|---|
| Switch_A | Port channel 1 | VLAN 10, VLAN 20, VLAN 30 |
| Switch_B | Port channel 2 | VLAN 10, VLAN 20, VLAN 30 |
| MultilayerSwitch_A | Port channel 1 & Port channel 2 | VLAN 10, VLAN 20, VLAN 30 |

## Cisco CLI Configuration
_Note: The `show run` outputs and copy buttons from the HTML file cannot be directly replicated in Markdown. You can paste the code blocks below as preformatted text._

### Switch_A `show run` Output
