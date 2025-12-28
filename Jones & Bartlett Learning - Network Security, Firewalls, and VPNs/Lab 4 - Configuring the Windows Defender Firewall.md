
# Introduction

The purpose of a firewall is to control network access in both directions: inbound and outbound. Network firewalls are hardware devices that sit at the perimeter of protected networks and regulate traffic entering and leaving that network. Host firewalls are software, typically part of the operating system, which run on individual computers, regulating the network traffic allowed to enter and leave that system. The Windows Defender Firewall is a host firewall that works in conjunction with any network firewalls that protect the same server.

Best practice for firewall configuration is to implement a default deny policy that says that any traffic not explicitly permitted by a firewall rule is disallowed by default. System administrators then set firewall policies by creating rules that describe the types of traffic allowed to pass through the device.

In this lab, you will use a web browser to attempt to connect to a Windows 2019 server using HTTP but see that the connection is blocked by the Windows Defender Firewall. You will then enable a rule in Windows Firewall that allows the HTTP connection. Finally, you will verify that the new rule allows your web connection to succeed.

# Section 1

<u>Part 1 - Test Access to a Windows IIS Server Using a Web Browser</u>

On the vWorkstation taskbar, **click** the **Internet Explorer icon** to launch the browser.

SS1
<img width="1911" height="888" alt="Screenshot 2025-09-21 132404" src="https://github.com/user-attachments/assets/51673442-be75-4d30-8856-2fd559f5b521" />

In the browser’s address box, **type http://172.30.0.16** (the IP address for TargetWindows02) and **press Enter** to connect to the Windows 2019 server.

*The browser will display an error message indicating that the browser cannot connect to the IIS web server on TargetWindows02.*

SS2
<img width="1788" height="682" alt="Screenshot 2025-09-21 132546" src="https://github.com/user-attachments/assets/8a216b24-9a8c-4a02-a2df-d96b21d46b2f" />

**Minimize** the **browser window**.

<u>Part 2 - Enable a Windows Defender Firewall Rule to Allow HTTP Access</u>

On the Lab View toolbar, **select** **TargetWindows02** from the Virtual Machine dropdown menu to connect to the TargetWindows02 web server.

From the TargetWindows02 taskbar, **click** the **Windows Start button**, then **click** the **Control Panel button** to open the Control Panel window.

SS3
<img width="1513" height="725" alt="Screenshot 2025-09-21 132709" src="https://github.com/user-attachments/assets/01b1ceac-8122-499e-b125-c7f6eb5018a7" />

In the Control Panel window, **click** the **System and Security** **link**.

In the right pane, **click** the **Windows Defender Firewall link** to open the Windows Defender Firewall page.

In the left pane, **click** the **Advanced settings link** to open the Windows Defender Firewall with Advanced Security window.

In the left pane, **click** the **Inbound Rules link** to display the list of preconfigured firewall rules.

SS4
<img width="1767" height="780" alt="Screenshot 2025-09-21 132809" src="https://github.com/user-attachments/assets/e8d50b0e-8226-4584-86ce-df88a461df34" />

*A green checkmark in front of the rule indicates that the rule is already enabled. Any rules without a preceding green checkmark have not been enabled.*

In the center pane, **click** the **World Wide Web Services (HTTP Traffic-In) rule** to select it.

SS5
<img width="1400" height="737" alt="Screenshot 2025-09-21 133845" src="https://github.com/user-attachments/assets/0e813ece-6c2f-4042-bd80-12b8de6b99dd" />

In the Actions pane, **click** **Enable Rule** to enable the World Wide Web Services (HTTP Traffic-in) rule, which allows inbound HTTP traffic through the firewall.

*A green checkmark will appear in front of the rule to indicate that the rule has been enabled.*

SS6
<img width="698" height="621" alt="Screenshot 2025-09-21 133922" src="https://github.com/user-attachments/assets/bc99c57f-7dff-4e5e-bfa6-ef20518aa4b9" />

In the Actions pane, **click Properties** to open the World Wide Web Services (HTTP Traffic-In) Properties dialog box.

In the Properties dialog box, **click** the **Protocols and Ports tab** and review the information displayed.

*The tab confirms that World Wide Web Services (HTTP traffic) is allowed into the server on TCP port 80.*

SS7
<img width="1507" height="763" alt="Screenshot 2025-09-21 134004" src="https://github.com/user-attachments/assets/63bc48d2-1605-4686-b2f3-1dcb3d4776d1" />

In the Properties dialog box, **click** the **General tab** and **confirm** that the Enabled checkbox is selected.

SS8
<img width="633" height="737" alt="Screenshot 2025-09-21 134033" src="https://github.com/user-attachments/assets/8ff48646-2577-4521-8c8d-65baf6532184" />

**Click OK** to close the Properties dialog box.

**Close** the **Windows Defender Firewall with Advanced Security window**.

**Close** the **Windows Defender Firewall window**.

<u>Part 3 - Confirm the Windows Defender Firewall Configuration Allows HTTP</u>

On the Lab View toolbar, **select** **vWorkstation** from the Virtual Machine dropdown menu to open a connection to the vWorkstation.

On the vWorkstation taskbar, **click** the **Internet Explorer icon** to restore the browser window.

From the browser toolbar, **click** the **Refresh button** to reconnect to the web server on TargetWindows02.

*With the web traffic now permitted into the server, Internet Explorer should display the IIS Server homepage on the Windows 2019 server, indicating that the firewall rule was applied successfully.*

SS9
<img width="1897" height="775" alt="Screenshot 2025-09-21 134208" src="https://github.com/user-attachments/assets/5008e717-4477-4e3e-944e-38e0c9a2d87a" />

**Close** the **browser window**.

# Section 2

<u>Part 1 - Test Access to Windows IIS Server Using PowerShell</u>

**Connect** to the **TargetWindows02 machine**.

From the TargetWindows02 taskbar, **launch PowerShell**.

At the PowerShell prompt, **execute Get-NetFirewallRule -DisplayName "World Wide Web Services (HTTP Traffic-In)"** to query the status of the Inbound rule (Traffic-In) for the World Wide Web Services

```powershell
Get-NetFirewallRule -DisplayName "World Wide Web Services (HTTP Traffic-In)"
```

SS10
<img width="1076" height="768" alt="Screenshot 2025-09-21 134353" src="https://github.com/user-attachments/assets/02da2a7b-264c-4cd1-9ef3-54e3492b4bd9" />

```text
Note: The Get-NetFirewallRule command returns a list of information about the rule you have queried. Some of the relevant parameters are listed below.

- Grouping - identifies the group name for the rule (World Wide Web Services (HTTP)).
- Enabled - indicates the enabled status (True or False) of the rule.
- Profile - identifies the firewall profile to which this rule belongs (Domain, Private, or Public).
- Direction - specifies whether the rule is Inbound or Outbound.
- Action - describes the action the rule will have on the traffic (Allow or Block).
- Edge Traversal - determines the rule’s response (Allow or Block) to unsolicited inbound packets that have passed through a NAT device.
```

At the PowerShell prompt, **execute Get-NetFirewallRule -DisplayName "World Wide Web Services (HTTP Traffic-In)" | Get-NetFirewallAddressFilter** to query the IP address information for the same rule.

```powershell
Get-NetFirewallRule -DisplayName "World Wide Web Services (HTTP Traffic-In)" | Get-NetFirewallAddressFilter
```

SS11
<img width="1072" height="207" alt="Screenshot 2025-09-21 134712" src="https://github.com/user-attachments/assets/a171dff6-4beb-4b81-84b2-1c67bab7fe45" />

<u>Part 2 - Enable a Windows Defender Firewall Rule to Allow HTTP Access</u>

**Connect** to the **TargetWindows02 machine**.

At the PowerShell prompt, **execute Set-NetFirewallRule -DisplayName "World Wide Web Services (HTTP Traffic-In)" -Enabled True** to enable web traffic from remote users.

```powershell
Set-NetFirewallRule -DisplayName "World Wide Web Services (HTTP Traffic-In)" -Enabled True
```

SS12
<img width="1067" height="112" alt="Screenshot 2025-09-21 135016" src="https://github.com/user-attachments/assets/0e6eebf6-2309-42cf-b63b-51bb8358e551" />

At the PowerShell prompt, **execute the Get-NetFirewallRule command** to show the updated status of the rule.

SS13
<img width="1162" height="431" alt="Screenshot 2025-09-21 135143" src="https://github.com/user-attachments/assets/efd49324-5fc3-4c6f-bc3c-5866e960d000" />

<u>Part 3 - Confirm the Windows Defender Firewall Configuration Allows HTTP</u>

**Connect** to the **vWorkstation machine**.

From the vWorkstation taskbar, **restore** the **browser** and **refresh** the **page** to reconnect to the web server on TargetWindows02.

*With the web traffic now permitted into the server, Internet Explorer should display the IIS Server homepage on the Windows 2019 server, indicating that the firewall rule was applied successfully.*



