# LAB 3.7 - AD Network creation

In this lab, you will learn how to use **VulnerableAD**, a PowerShell script, to create a deliberately misconfigured and vulnerable **Active Directory (AD)** environment. This lab is useful for testing red team techniques, blue team detection strategies, and understanding common AD misconfigurations that attackers exploit.

### Objective:

The goal of this lab is to set up a vulnerable Active Directory environment using the **VulnerableAD** script. You will install Active Directory on a Windows Server, configure it, and use the VulnerableAD script to misconfigure AD settings, creating realistic vulnerabilities for testing security tools and attack techniques.

---

### Prerequisites:

- **Windows Server 2019/2016 VM:** A virtual machine running Windows Server (with Desktop Experience).
- **PowerShell:** Installed and configured on the Windows Server.
- **Active Directory Domain Services (AD DS):** Installed on the Windows Server.
- **VulnerableAD Script:** Downloaded from the repository.
- **Network Configuration:** Ensure your server is isolated from any production environments to prevent unintended impacts.

---

### General Steps:

1. **Set Up the Virtual Environment:**
    - Create a Windows Server 2019/2016 virtual machine (VM).
    - Configure the network settings to ensure the VM is isolated.
2. **Install Active Directory Domain Services (AD DS):**
    - Install and configure Active Directory Domain Services (AD DS) on the server, creating a domain for testing.
3. **Download and Configure the VulnerableAD Script:**
    - Download and run the VulnerableAD PowerShell script to create a vulnerable AD environment.

---

### **Solution Section: Commands and Step-by-Step Instructions**

### 1. **Set Up the Virtual Machine:**

- Download **Windows Server 2019/2016 ISO** from Microsoft and set up a VM using **VirtualBox** or **VMware**.
- Configure the VM with at least **4GB of RAM** and **40GB of disk space**.
- Install Windows Server using the "Desktop Experience" option.

### 2. **Install Active Directory Domain Services (AD DS):**

- **Step 1:** Once the server installation is complete, open the **Server Manager** and click on **Add Roles and Features**.
- **Step 2:** Follow the wizard to install **Active Directory Domain Services (AD DS)**.
    - Choose **Role-Based Installation**.
    - Select the server from the server pool and click **Next**.
    - Under the **Server Roles** section, select **Active Directory Domain Services**, and click **Next** to install all dependencies.
- **Step 3:** After installation, click **Promote this server to a domain controller**.
    - Select **Add a new forest** and provide a domain name (e.g., `lab.local`).
    - Set the **Directory Services Restore Mode (DSRM)** password.
- **Step 4:** Complete the installation and restart the server when prompted. Your Windows Server is now a domain controller.

### 3. **Download and Configure VulnerableAD Script:**

- **Step 1:** Open **PowerShell** as Administrator on your Windows Server.
- **Step 2:** Clone or download the **VulnerableAD** script from the GitHub repository. You can clone it directly using the following command:
    
    ```bash
    
    git clone https://github.com/WazeHell/vulnerable-AD.git
    
    ```
    
- **Step 3:** Navigate to the **vulnerable-AD** directory and run the setup script to configure your AD environment with vulnerabilities:
    
    ```bash
    
    cd .\vulnerable-AD\
    .\Vulnerable-AD.ps1
    
    ```
    
- **Step 4:** The script will automatically create multiple vulnerabilities in your Active Directory environment. These include misconfigurations, weak permissions, insecure group policies, and mor.
