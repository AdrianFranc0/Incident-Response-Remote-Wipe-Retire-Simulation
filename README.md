# Remote Wipe / Retire Simulation — Microsoft Intune (Incident Response)

**Scenario:** This lab simulates a real-world incident where IT must remotely remove corporate data from a Windows device using Intune.  
- **Lost/stolen corporate laptop** → Wipe (full factory reset).  
- **Personal/BYOD device with corporate apps/data** → Retire (remove corporate footprint, leave personal data).  
- **Offboarding / compliance cases** → Either action depending on policy.  

**Why this matters:** Intune’s Retire and Wipe actions are core tools for incident response and device lifecycle management. They allow organizations to quickly secure corporate data while respecting whether a device is company-owned or personal.

---

## Overview

This project demonstrates both response paths on a Windows 10/11 VM:

- **Verify enrollment** — confirm device is managed by Intune  
- **Retire** — remove corporate profiles/apps while leaving OS/data intact *(BYOD/offboarding path)*  
- **Re-enroll** — bring the VM back under management so Wipe can be demonstrated  
- **Wipe** — factory reset back to OOBE *(lost/stolen corporate device path)*  

---

## What I built

- Windows 10/11 VM enrolled to Microsoft Intune  
- **Retire** action to remove workplace account + corporate footprint  
- **Re-enroll** procedure via Entra ID to manage the device again  
- **Wipe** action to trigger full reset to OOBE  
- Screenshot evidence at each stage, aligned with real-world incident response reasoning  

---

## Step-by-step

### 1) Verify Enrollment & Device Status
Confirmed the VM is connected to FALSOTECH tenant and managed by Intune.

<p align="center">
<img src="https://i.imgur.com/pH6PqHr.png" width="800" style="height:auto;" alt="VM enrolled in FALSOTECH tenant under Access work or school"/>
<br /><br />
</p>

---

### 2) Retire the Device (BYOD / Offboarding scenario)
From Intune, I issued **Retire** on the VM.  
- Removes company data and MDM enrollment  
- Leaves OS and personal files intact  
- Realistic for **BYOD or employee offboarding**, not for stolen devices  

<p align="center">
<img src="https://i.imgur.com/F4NIkEe.png" width="800" style="height:auto;" alt="Intune Retire action confirmation and VM message that workplace account removed"/>
<br /><br />
</p>

---

### 3) Re-Enroll the VM (to prep for Wipe demo)
After Retire, the device was unmanaged. To continue, I re-enrolled the VM back into Intune.  
- Shows **Access work or school → Connected** with FALSOTECH tenant  
- Now available again in Intune for Wipe  

<p align="center">
<img src="https://i.imgur.com/kHIzX42.png" width="800" style="height:auto;" alt="VM re-enrolled into FALSOTECH tenant and connected under Access work or school"/>
<br /><br />
</p>

---

### 4) Wipe (Lost/Stolen corporate device scenario)
Finally, I issued **Wipe** from Intune.  
- Full factory reset → device returns to OOBE  
- This is the action you’d use in a **stolen or compromised corporate laptop** case
  
After reset, the VM will reboot and land at the OOBE screen:  
- **Proof that the Wipe action fully reset the device** 
<p align="center">
<img src="https://i.imgur.com/tU1FAk6.png" width="800" style="height:auto;" alt="Wipe action initiated successfully in Intune for VM"/>
<br /><br />
</p>

 <p align="center">
<img src="https://i.imgur.com/B4338Lz.png" width="800" style="height:auto;" alt="Wipe action initiated successfully in Intune for VM"/>
<br /><br />
</p>

---

## What I learned

- The operational difference between **Retire** (BYOD/offboarding, keeps OS/data) and **Wipe** (lost/stolen, full reset)  
- How to confirm **device enrollment status** before issuing actions  
- Why **Re-enroll** is needed in lab context (so both actions can be demonstrated)  
- How to verify success through **Intune Device Actions history** and **endpoint behavior**  

- Always take a **VM snapshot before Wipe**, so you can roll back and redo the demo.  
- If **actions stay Pending**, sync from the VM (**Access work or school → Info → Sync**).  
- For strict Conditional Access setups, temporarily exclude your test user during testing.  
- In a real **lost/stolen device** scenario, you’d skip Retire and go straight to Wipe.  

---
