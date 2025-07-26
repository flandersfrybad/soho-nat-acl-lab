# soho-nat-acl-lab

# 🧠 SOHO Network: NAT + ACL + PAT Lab | Cisco Packet Tracer

Hey there 👋 I’m Lanner.

This is a real-world Small Office / Home Office (SOHO) lab I built inside Cisco Packet Tracer to simulate basic firewall logic, NAT, and PAT behavior.

Yes, there’s a video walkthrough:
🎥 https://www.tiktok.com/@herrotarrow/video/7530746921497988383

---

## 🧱 Topology Summary

PC0 <---> Router0 <---> Server0
192.168.0.0/24 NAT 10.0.0.0/24


- PC0 = Internal host (192.168.0.10)
- Router0:
  - Fa0/0 = Inside = 192.168.0.1
  - Fa0/1 = Outside = 10.0.0.1
- Server0 = Simulated Internet (10.0.0.2)

---

## 🧰 What’s Covered

✅ NAT setup (inside/outside)  
✅ PAT using `overload`  
✅ ACL to allow ICMP, HTTP (80), HTTPS (443)  
✅ Deny-by-default firewall behavior  
✅ Packet Tracer live ping + NAT verification  
✅ CLI + visual logic

---

## 🔧 CLI Highlights

### NAT + PAT Setup

```bash
interface fa0/0
 ip address 192.168.0.1 255.255.255.0
 ip nat inside
 no shutdown

interface fa0/1
 ip address 10.0.0.1 255.255.255.0
 ip nat outside
 no shutdown

ip nat inside source list 100 interface fa0/1 overload

ACL (Access Control List) 100

ip access-list extended 100
 permit icmp 192.168.0.0 0.0.0.255 any echo
 permit tcp 192.168.0.0 0.0.0.255 any eq www
 permit tcp 192.168.0.0 0.0.0.255 any eq 443
 deny ip any any

Then apply to inside interface:

interface fa0/0
 ip access-group 100 in

🧪 Test Commands

ping 192.168.0.1
ping 10.0.0.2
show ip interface brief
show ip nat statistics
show ip nat translations
show access-lists

From browser inside PC0:

    http://10.0.0.2 ✅

    https://10.0.0.2 ✅

📁 Files (Included)

    soho-nat-acl-lab.pkt → the live Packet Tracer simulation

    README.md → this guide

    cli-commands.txt (all typed commands)

    topology.png (screenshot)

💡 Why I Built This

This lab builds skills used in:

    Network+ simulations

    Security+ firewall + NAT sections

    SOC/Helpdesk Tier I–II packet flow logic

    Real-world interviews ask: “Can you configure a router to allow only web traffic?”

🙋‍♂️ Contact

Built by: @herrotarrow
lannertfayad@yahoo.com
https://www.linkedin.com/in/lannertfayad/
Questions? DM me on TikTok or drop an issue on this repo.

Let’s go deeper next time—VLANs, DHCP, DNS spoofing, Wireshark, and beyond.
