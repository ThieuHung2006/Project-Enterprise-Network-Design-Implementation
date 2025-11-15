# Project-Enterprise-Network-Design-Implementation
Lab project: Core–Distribution–Access network with VLANs, DMZ, ACL/NAT, HSRP, EtherChannel, OSPF

Oject
- VLAN segmentation cho IT, HR, Accounting
- VLSM-based subnetting để tối ưu IP
- DMZ gồm DNS, Mail, DHCP servers
- Kết nối ISP qua OSPF
- Kiểm thử end-to-end thành công, đảm bảo redundancy & high availability
- Cấu hình SW_core HSRP, Spanning-Tree, EtherChannel LACP,OSPF

Network Topology<img width="1864" height="913" alt="project" src="https://github.com/user-attachments/assets/2fbd61f2-50e2-4127-a9e1-f378bc048a14" />

Network Topology
<img width="594" height="177" alt="Table" src="https://github.com/user-attachments/assets/88e98436-fc15-47e5-9aca-1dd6e707e377" />

Router_DMZ Configuration
- Interfaces: e0/1, e0/2, e0/0.99, e0/3
- Default route: `ip route 0.0.0.0 0.0.0.0 200.100.50.1`
- OSPF: router-id 3.3.3.3, networks 192.168.99.0, 10.0.0.0, 10.1.0.0, 200.100.50.0
- Default-information originate: advertise default route to Core Switch
- NAT/ACL: inside for VLANs, outside to ISP
Full Router_DMZ configuration is available


SW_core1 Configuration
- VLANs: 10 (IT), 11 (HR), 12 (Accounting)
- Trunk Ports: e0/3 trunked VLAN 10; e1/0 trunked VLANs 11 & 12
- EtherChannel (LACP): Port-channel 1 (e0/0–2) for Core redundancy with SW_core2
Layer 3 Interfaces:
- e1/1: 10.0.0.1/30 link to Router_DMZ
- SVI VLAN 10: 192.168.10.2/24, HSRP 10 (192.168.10.1), DHCP relay 192.168.99.10
- SVI VLAN 11: 192.168.11.2/24, HSRP 11 (192.168.11.1), DHCP relay 192.168.99.10
- SVI VLAN 12: 192.168.12.2/24, HSRP 12 (192.168.12.1), DHCP relay 192.168.99.10
- Routing: IP routing enabled; OSPF router-id 1.1.1.1, networks 10.0.0.0/30, 192.168.10.0/24, 192.168.11.0/24, 192.168.12.0/24
Full SW_core1 configuration is available

