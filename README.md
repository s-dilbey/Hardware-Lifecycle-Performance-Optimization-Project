# Hardware Lifecycle & Performance Optimization Project
## Technical Case Study: Diagnostic, Migration, and Physical Remediation

### 📌 Project Overview
This project documents the performance audit and hardware refresh of two legacy workstations. The objective was to extend the hardware lifecycle by identifying system bottlenecks, performing data migrations from HDD to SSD, and implementing post-migration optimizations while adhering to data integrity and security best practices.

---

### 🛡️ GRC & Security Alignment (NIST CSF 2.0)
As a career-switcher into Cyber Security/GRC, I approached this technical task through the lens of the **NIST Cybersecurity Framework**:

* **Govern (GV.AM):** Established a formal asset inventory by documenting hostnames, OS versions, and hardware specifications.  
* **Protect (PR.DS):** Performed pre-migration audits for BitLocker/Device Encryption and executed secure media sanitization.
* **Recover (RC.RP):** Developed and utilized WinPE Recovery Media to remediate bootloader failures during the migration process.

---

### 💻 Case Study 1: Dell Latitude E6420 (Standard Migration)
**Issue:** Significant performance degradation.  
**Diagnosis:** Utilized Task Manager to identify 100% Disk Utilization at idle.
* Determined the mechanical HDD (5400 RPM) was the primary hardware bottleneck.

**Execution:**
* **Cloning:** Used Macrium Reflect to clone the HDD to a 240GB Patriot Burst Elite SSD.
* **Optimization:** * Verified **TRIM** was active via `Optimize Drives`.
    * Modified BIOS to ensure **AHCI Mode** was enabled for optimal SATA throughput.
    * Disabled **Fast Startup** to ensure clean kernel initialization.

---

### ⚠️ Case Study 2: ASUS X555QA (Complex Recovery)
**Issue:** Extreme system latency.  
**Diagnosis:** Utilized Task Manager to identify 100% Disk Utilization at idle.  

**Technical Challenges & Incident Response:**
1.  **Volume Management:** Encountered "unmovable files" error when shrinking a 1TB partition. Resolved using **MiniTool Partition Wizard**.
2.  **MFT Corruption:** An out-of-sync partition size during the first clone attempt resulted in a RAW file system. **Remediation:** Cleared the SSD and re-initialized the clone with synchronized partition parameters.
3.  **Bootloader Failure:** The system failed to find the boot partition post-swap. **Resolution:** Booted into a WinPE environment via USB and utilized the "Fix Windows Boot Problems" tool.
4.  **Hardware Remediation:** A Zero Insertion Force (ZIF) connector for the keyboard was damaged during disassembly. **Repair:** Fabricated a custom shim using cardstock and non-conductive adhesive to restore full keyboard functionality.

---

### 🛠️ Tools & Technologies
* **Software:** Macrium Reflect, MiniTool Partition Wizard, WinToy (Debloating).
* **Hardware:** SATA to USB 3.0 Interface, ESD-safe prying tools, SSD media.
* **Frameworks:** NIST SP 800-88 (Media Sanitization Guidelines).

---

### 🧼 Data Retirement & Sanitization
To maintain the **Confidentiality** of the data on the retired mechanical drives, the following sanitization plan was implemented:
* **Method:** Physical destruction (Platter disruption).
* **Standard:** Aligned with **NIST SP 800-88** guidelines for physical destruction of magnetic media to ensure data is unrecoverable by any technical means.

---

### 💡 Lessons Learned
* **Risk Mitigation:** Always create recovery media *before* hardware disassembly.
* **Physical Security:** Legacy consumer hardware often has brittle internal components (ZIF connectors); tactical patience is required for physical maintenance.
* **Documentation:** Detailed logging of error codes and partition sizes is critical for troubleshooting "RAW" drive errors.

