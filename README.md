# Project: Enterprise Network Design & Implementation

Lab project: Core–Distribution–Access network with VLANs, DMZ, ACL/NAT, HSRP, EtherChannel, OSPF

## Objective
- Implement VLAN segmentation for IT, HR, and Accounting departments
- Optimize IP usage using VLSM-based subnetting
- Configure DMZ with DNS, Mail, and DHCP servers
- Connect to ISP using OSPF
- Ensure redundancy and high availability through HSRP and EtherChannel
- Verify end-to-end connectivity

## Network Topology
## Network Topology

![Network Topology Diagram](https://github.com/user-attachments/assets/4d5c048b-714c-407f-9c5c-0299d74adb48)

![Network Topology Table](https://github.com/user-attachments/assets/dd898172-db29-4c0e-a185-6b8dd90d5a68)

*Network topology diagram and table

## Router_DMZ Configuration
- Interfaces: e0/1, e0/2, e0/0.99, e0/3
- Default route: `ip route 0.0.0.0 0.0.0.0 200.100.50.1`
- OSPF: router-id 3.3.3.3, networks 192.168.99.0, 10.0.0.0, 10.1.0.0, 200.100.50.0
- Default-information originate: advertise default route to Core Switch
- NAT/ACL: inside for VLANs, outside to ISP  
Full configuration available: `Router_DMZ.txt`

## SW_core1 Configuration
- VLANs: 10 (IT), 11 (HR), 12 (Accounting)
- Trunk Ports: e0/3 trunked VLAN 10; e1/0 trunked VLANs 11 & 12
- EtherChannel (LACP): Port-channel 1 (e0/0–2) for Core redundancy with SW_core2
- Layer 3 Interfaces:
  - e1/1: 10.0.0.1/30 link to Router_DMZ
  - SVI VLAN 10: 192.168.10.2/24, HSRP 10 (192.168.10.1), DHCP relay 192.168.99.10
  - SVI VLAN 11: 192.168.11.2/24, HSRP 11 (192.168.11.1), DHCP relay 192.168.99.10
  - SVI VLAN 12: 192.168.12.2/24, HSRP 12 (192.168.12.1), DHCP relay 192.168.99.10
- Routing: IP routing enabled; OSPF router-id 1.1.1.1, networks 10.0.0.0/30, 192.168.10.0/24, 192.168.11.0/24, 192.168.12.0/24  
Full configuration available: `SW_core1_config.txt`

## Verification
- Show VLANs: `show vlan brief`
- Show Trunks: `show interfaces trunk`
- Show EtherChannel: `show etherchannel summary`
- Show NAT translations: `show ip nat translations`
- Verify HSRP status: `show standby brief`
- Verify OSPF neighbors: `show ip ospf neighbor`
- End-to-end ping tests:
  - From PC VLAN 10 → 192.168.99.10 (DNS)
  - From PC VLAN 11 → 192.168.12.1 (Accounting gateway)
  - Internet access via NAT → 8.8.8.8

## Conclusion
- VLAN, Trunk, EtherChannel (LACP), and HSRP successfully implemented for Core–Distribution–Access network
- DMZ configured with NAT/ACL for DNS, Mail, and DHCP servers
- ISP connected via point-to-point OSPF with default route advertised
- End-to-end testing completed successfully, ensuring redundancy and high availability

## Lessons Learned / Key Takeaways
- Understand Core–Distribution–Access network design and enterprise network deployment
- Implement VLAN segmentation and VLSM subnetting to optimize IP usage
- Configure Layer 3 SVI, Trunk, EtherChannel (LACP), and Spanning-Tree for redundancy & high availability
- Deploy HSRP for gateway redundancy
- Set up DMZ with NAT/ACL for server access and security
- Connect ISP via OSPF point-to-point and advertise default route
- Conduct end-to-end connectivity testing and troubleshooting
- Improve skills in reading topologies, writing lab reports, and configuring real network devices

## About
Lab project: Core–Distribution–Access network with VLANs, DMZ, ACL/NAT, HSRP, EtherChannel, OSPF
