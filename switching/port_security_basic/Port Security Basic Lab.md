# 🛡️ Port Security: Basic Configuration Lab

## Scenario

You are a junior network administrator at a small company. Recently, a rogue laptop was plugged into the network and gained access to sensitive resources. To prevent unauthorized devices from connecting, you've been asked to configure port security on Switch1. Each access port should allow only one authorized device, and any violation should result in the port being automatically disabled.

---

## Objectives

- Configure switch ports for access mode
- Enable sticky MAC learning to lock allowed devices
- Limit the number of MAC addresses per port to one
- Set the violation action to `shutdown`
- Simulate a violation by plugging in a rogue laptop
- Verify and recover from port shutdown

---

## Topology Overview

- **Switch1 (S1)**
- **PC0** connected to `Fa0/1` *(authorized device)*
- **Laptop0 (rogue)** connected to `Fa0/1` *(to simulate attack)*

---

## Tasks

### 1️⃣ Basic Switch Setup
```bash
Switch> enable
Switch# configure terminal
Switch(config)# hostname S1
S1(config)# no ip domain-lookup
2️⃣ Configure Port Fa0/1 with Port Security
bash
Copy
Edit
S1(config)# interface fa0/1
S1(config-if)# switchport mode access
S1(config-if)# switchport port-security
S1(config-if)# switchport port-security maximum 1
S1(config-if)# switchport port-security violation shutdown
S1(config-if)# switchport port-security mac-address sticky
S1(config-if)# exit
3️⃣ Save Config
bash
Copy
Edit
S1# copy running-config startup-config
4️⃣ Verify Allowed Device (PC0)
After PC0 sends traffic, check sticky MAC:

bash
Copy
Edit
S1# show port-security interface fa0/1
S1# show mac address-table
You should see PC0’s MAC address learned and saved as sticky.

⚠️ Simulate Violation: Rogue Laptop
5️⃣ Trigger Violation
Disconnect PC0 from Fa0/1.

Connect Laptop0 (rogue) to Fa0/1.

Attempt to ping or generate traffic.

6️⃣ Observe Shutdown Behavior
bash
Copy
Edit
S1# show interfaces status
S1# show port-security interface fa0/1
You should see:

Port is in err-disabled state

Violation count = 1

🔁 Optional Recovery
To restore the port after a shutdown:

bash
Copy
Edit
S1(config)# interface fa0/1
S1(config-if)# shutdown
S1(config-if)# no shutdown
✅ Verification Commands
bash
Copy
Edit
S1# show port-security
S1# show port-security interface fa0/1
S1# show mac address-table
S1# show interfaces status
📸 Suggested Screenshots
File Name	Content
port_security_topology.png	Network diagram (S1, PC0, rogue laptop)
port_security_verification.png	CLI output showing sticky MAC learned
port_security_violation.png	Port shutdown and violation shown in CLI

✅ Completion Checklist
 Port configured for access mode

 Port security enabled with 1 MAC limit

 Violation mode set to shutdown

 Sticky MAC address successfully learned

 Violation triggered by rogue laptop

 Port disabled (err-disabled) on violation

 CLI used to verify and recover port

📎 Optional Enhancements (For Pro Labs)
Backup the switch config as a .txt file

Add comments to .pkt file describing port configs

Link the screenshots from your GitHub README.md

Show both working state and post-violation state

📝 Author Notes
This lab is designed to simulate real-world access control practices using Cisco's port security features. It aligns with key CCNA exam objectives in network security and switch configuration.

yaml
Copy
Edit

---

Let me know if you’d like the next lab (`basic_static_routing.md`) in the same clean CCNA style — or if you want help writing your root `README.md` to make your whole repo look 🔥 on GitHub.