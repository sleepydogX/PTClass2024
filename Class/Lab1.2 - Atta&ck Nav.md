**Lab 1.2: MITRE ATT&CK Navigator**

**Objective**: Use the MITRE ATT&CK Navigator to map and visualize adversarial techniques based on the previous exercise. 

**Steps**:

1.	**Access ATT&CK Navigator**:

•	Go to the MITRE ATT&CK Navigator website: [Navigator](https://mitre-attack.github.io/attack-navigator/).

2.	**Create a New Layer**:

•	Start a new layer and select a version of the ATT&CK matrix.

3.	**Map Techniques**:

•	Choose specific techniques from the matrix relevant to your exercise and add them to the layer.

4.	**Customize the Layer**:

•	Use color coding to indicate the status of each technique (e.g., green for covered, red for not detected). 

•	Also include a list of tools that can be used to execute the attack and to detect the attack in the **COMMENTS** section.

5.	**Save and Export**:

•	Save the layer and export it as a JSON file or image.

6.	**Review the Layer**:

•	Review the visual representation to identify gaps in coverage.

**Expected Outcome**: A visual map of attack techniques with insights into potential gaps.

### SOLUTION:

![image](https://github.com/user-attachments/assets/7e650464-7f80-4996-9e43-8c4c3062b6ef)


Code:
```
{
  "version": "4.5",
  "name": "XYZ Corporation Phishing Campaign Simulation",
  "description": "A purple teaming exercise focused on simulating a sophisticated phishing attack targeting XYZ Corporation.",
  "domain": "enterprise-attack",
  "techniques": [
    {
      "techniqueID": "T1566.001",
      "tactic": "initial-access",
      "color": "#FF6666",
      "comment": "Phishing: Spear Phishing Attachment - Simulated phishing email with malicious attachment. \nAttack Tools: Phishery, Gophish, Social Engineer Toolkit (SET). \nDetection Tools: Email filtering solutions, EDR, Email security gateways.",
      "enabled": true
    },
    {
      "techniqueID": "T1204.002",
      "tactic": "execution",
      "color": "#FFCC66",
      "comment": "User Execution: Malicious File - Execution of malicious attachment. \nAttack Tools: Metasploit, PowerShell Empire, Custom Scripts. \nDetection Tools: EDR, Antivirus/Anti-malware solutions, Application Whitelisting.",
      "enabled": true
    },
    {
      "techniqueID": "T1071.001",
      "tactic": "command-and-control",
      "color": "#FF9966",
      "comment": "Command and Control: Application Layer Protocol - Establish C2 over HTTPS. \nAttack Tools: Cobalt Strike, Covenant, PowerShell Empire. \nDetection Tools: Network Traffic Analysis, DNS Logs, Web Proxy Logs.",
      "enabled": true
    },
    {
      "techniqueID": "T1003.001",
      "tactic": "credential-access",
      "color": "#66CCFF",
      "comment": "Credential Dumping: LSASS Memory - Attempt to dump credentials. \nAttack Tools: Mimikatz, ProcDump, PowerShell. \nDetection Tools: Sysmon with specific rules, EDR, Windows Event Logs (Security Log: 4624, 4672, etc.).",
      "enabled": true
    },
    {
      "techniqueID": "T1021.001",
      "tactic": "lateral-movement",
      "color": "#66FF66",
      "comment": "Lateral Movement: SMB/Windows Admin Shares - Move laterally using stolen credentials. \nAttack Tools: PsExec, SMBexec, CrackMapExec. \nDetection Tools: Network Traffic Analysis, Windows Event Logs (4728, 4732, etc.), EDR.",
      "enabled": true
    },
    {
      "techniqueID": "T1048.002",
      "tactic": "exfiltration",
      "color": "#CC66FF",
      "comment": "Exfiltration: Exfiltration Over Alternative Protocol - Simulate data exfiltration over an encrypted channel. \nAttack Tools: Rclone, Cobalt Strike, Custom Scripts. \nDetection Tools: Network Traffic Analysis, Data Loss Prevention (DLP) tools, Web Proxy Logs.",
      "enabled": true
    }
  ],
  "gradient": {
    "colors": ["#ffffff", "#ff0000"],
    "minValue": 0,
    "maxValue": 1
  },
  "legendItems": [
    {
      "label": "Techniques Used",
      "color": "#FF6666"
    },
    {
      "label": "User Execution",
      "color": "#FFCC66"
    },
    {
      "label": "Command and Control",
      "color": "#FF9966"
    },
    {
      "label": "Credential Dumping",
      "color": "#66CCFF"
    },
    {
      "label": "Lateral Movement",
      "color": "#66FF66"
    },
    {
      "label": "Exfiltration",
      "color": "#CC66FF"
    }
  ]
}
```
