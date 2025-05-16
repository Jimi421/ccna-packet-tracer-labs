
## 💾 Save Configuration

Once all configurations are complete and verified, save your work:

```bash
copy running-config startup-config
This ensures all changes are stored in NVRAM and persist after a reboot.

Completion Checklist ✅
 Unused ports shut down

 CDP disabled

 enable secret set and encrypted

 Console & VTY access secured

 Passwords encrypted

 Banner displayed

 SSH (optional) working

 HTTP server commands attempted or noted as skipped

 ✅ Running config saved to startup-config

Notes
This lab reflects real-world switch hardening practices required in enterprise environments and expected on the CCNA exam. Some services (like HTTP) may be unavailable in Packet Tracer but are noted for completeness and realism.

yaml
Copy
Edit

---

Let me know if you'd like me to reprint the **full final version** of the updated `README.md` with this included — or if you’re ready to push and move to the next lab!





You said:
yes reprint full for copy 


ChatGPT said:
You got it! Here is your final, full, copy-paste-ready README.md for the Switch Hardening Basics Lab, now including:

💾 copy running-config startup-config

✅ Updated completion checklist

⚠️ Notes for Packet Tracer limitations (e.g., ip http server)

📄 switching/switch_hardening_basics/README.md
markdown
Copy
Edit
# 🔒 Switch Hardening Basics Lab

## Scenario

You are a network technician preparing a new switch for deployment. Your goal is to secure it using Cisco best practices before placing it into production. This includes shutting down unused ports, disabling unnecessary services, securing remote access, and encrypting stored credentials.

This lab focuses purely on switch-side security configuration — no routers or PCs are required.

---

## Recommended Device

> ✅ **Use the "Switch-PT Multilayer" (Cisco 3560)** for this lab in Packet Tracer.

This allows:
- VLAN management
- Routing configuration (if needed)
- Full access to security features like `enable secret`, `service password-encryption`, SSH setup

> ⚠️ **Note:** The commands `ip http server` and `ip http secure-server` are **not supported** on Packet Tracer switches (including multilayer). In real Cisco hardware, these are valid. To simulate them in PT, use a **Cisco 2901 router instead**.

---

## Objectives

- Disable unused interfaces
- Disable CDP and unused services
- Set and encrypt console/VTY access
- Configure a secure enable password
- Add a legal login banner
- Optionally enable SSH for remote access
- Save the configuration

---

## Lab Topology

| Device | Model               | Function         |
|--------|---------------------|------------------|
| SW1    | Switch-PT Multilayer | Core switch (single device only) |

---

## Commands & Configuration

### 🔧 1. Disable Unused Ports

```bash
interface range fa0/1 - 24
description UNUSED_PORT
shutdown
📡 2. Disable CDP Globally
bash
Copy
Edit
no cdp run
🚫 3. Disable Unused Services (Optional in PT)
bash
Copy
Edit
! May not be supported in PT
no ip http server
no ip http secure-server
no service pad
no ip bootp server
no ip source-route
✅ OK to skip if Packet Tracer throws an "Invalid input" error.

🧾 4. Set a Banner MOTD (Legal Disclaimer)
bash
Copy
Edit
banner motd ^C
Unauthorized access is prohibited. This system is monitored.
^C
🔐 5. Enable Password Encryption
bash
Copy
Edit
service password-encryption
🔑 6. Secure Privileged EXEC Mode
bash
Copy
Edit
enable secret PrivExecSecure!
👤 7. Create a Local User Account
bash
Copy
Edit
username admin secret Cisco123!
🔒 8. Secure Console and VTY Lines
bash
Copy
Edit
line console 0
password ConsoleSecure!
login
exit

line vty 0 4
login local
transport input ssh
exit
🛡️ 9. (Optional) Enable SSH for Remote Access
bash
Copy
Edit
hostname SW1
ip domain-name lab.local
crypto key generate rsa
! Choose 1024 bits or higher
💾 10. Save Configuration
bash
Copy
Edit
copy running-config startup-config
This ensures all changes are stored in NVRAM and persist after a reboot.

Verification Commands
bash
Copy
Edit
show running-config
show interfaces status
show cdp neighbors
show ip http server status
✅ Look for:

Unused ports: administratively down

CDP: disabled

Passwords: encrypted

Banner: appears at login

SSH/VTY login secured

enable secret protected

Completion Checklist ✅
 Unused ports shut down

 CDP disabled

 enable secret set and encrypted

 Console & VTY access secured

 Passwords encrypted

 Banner displayed

 SSH (optional) working

 HTTP server commands attempted or noted as skipped

 ✅ Running config saved to startup-config

Notes
This lab reflects real-world switch hardening practices required in enterprise environments and expected on the CCNA exam. Some services (like HTTP) may be unavailable in Packet Tracer but are included for realism and completeness. Saving the configuration is a critical final step to ensure your security settings persist across reboots.