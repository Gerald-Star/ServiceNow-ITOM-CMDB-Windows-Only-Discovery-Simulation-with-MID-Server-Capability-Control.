
# Project: ServiceNow ITOM/CMDB Windows-Only Discovery Simulation with MID Server Capability Control  

##  Project Description  
This project demonstrates how to configure and execute a **targeted Discovery in ServiceNow** that only updates a **Windows Server** while leaving a Linux Server untouched.  

By customizing **MID Server capabilities** and controlling **protocol behavior (WMI/WinRM only)**, I simulated a real-world scenario where Discovery is restricted to specific device types, ensuring that only relevant Configuration Items (CIs) are updated in the CMDB.  

I Configured a targeted **ServiceNow Discovery** to update only a **Windows Server** while skipping a Linux Server.  
By customizing **MID Server capabilities** and restricting to **WMI/WinRM protocols**, I simulated a real-world use case where Discovery is OS-specific and CMDB updates are controlled.  
---

## Visual Representation  
```plaintext
+-----------------+ +-------------------+
| ServiceNow | | MID Server |
| Discovery Engine| ---------> | Windows Protocols |
+-----------------+ +-------------------+
|
| Uses WMI / WinRM / SMB
v
+---------------------+
| Windows Server 192.168.16.11 |
| ✅ Discovered & Updated |
+---------------------+

 +---------------------+
 | Linux Server 192.168.16.12  |
 |  ❌ Skipped (No SSH/SNMP)    |
 +---------------------+

```
## Key Steps Performed  

1. **Discovery Schedule Setup**  
   - Created a custom Discovery Schedule named *Sim Win Only Behavior*.  
   - Defined IP range: `192.168.16.11–192.168.16.12`.  

2. **MID Server Configuration**  
   - Assigned a dedicated MID Server with **Windows-only capabilities** (`WMI`, `WinRM`).  
   - Excluded Linux protocols (`SSH`, `SNMP`).  

3. **Protocol Control (Shazzam Probe)**  
   - Verified that Shazzam probe scanned only **Windows-specific ports**:  
     - `135` (WMI/DCOM)  
     - `445` (SMB)  
     - `5985` (WinRM)  
   - Excluded Linux ports such as `22` (SSH) and `161` (SNMP).  

4. **Discovery Execution & Validation**  
   - Ran Discovery and validated results:  
     - ✅ **Windows Server** (`192.168.16.11`) → classified, identified, and updated in the CMDB.  
     - ❌ **Linux Server** (`192.168.16.12`) → skipped, no update performed.  

5. **Debugging & Verification**  
   - Checked **Discovery Status record** under *Devices tab* to confirm only the Windows host was updated.  
   - Verified in **ECC Queue logs** that only Windows protocol communication occurred.  

---

## Outcome / Value  
- Showcased how to **fine-tune Discovery** for targeted infrastructure.  
- Demonstrated **control over CMDB updates** by protocol and OS type.  
- Validated troubleshooting skills using **Discovery Status** and **ECC Queue**.  

---


### Screenshot Placeholder  

![Discovery Devices Tab](images/discovery_devices_tab.png)  
*Example: Only Windows Server updated, Linux skipped*  

![ECC Queue Debug](images/ecc_queue_windows_only.png)  
*Example: Shazzam probe shows Windows protocols only*  

---

## 🛠️ Skills Highlighted  
- ServiceNow ITOM: Discovery & CMDB  
- MID Server Capabilities Management  
- Protocol & Probe Customization  
- Debugging with ECC Queue  
- Selective Device Onboarding  

---
