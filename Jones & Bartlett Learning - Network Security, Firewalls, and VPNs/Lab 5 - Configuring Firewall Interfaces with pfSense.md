
# Introduction

Firewalls can be completely software-based and run on an endpoint or a server, or be standalone “turn-key” appliances—hardware devices with pre-installed software ready to be dropped into an existing network topology. Others, such as cloud firewalls, exist somewhere in between, with a hardware device on the local network and software managed remotely by a third party. In any case, the job of the firewall is fairly straightforward: to selectively filter traffic going from one side of a firewall to another.

There are a multitude of firewalls commercially available in the market for organizations to use, and two common notions you may hear when considering your options are 1) hardware is better, and 2) open-source options are less secure due to their code being public knowledge. However, the reality is that there are no truly hardware-only firewall devices, as they are all software-running-on-hardware stacks; and if open-source software was truly insecure (that is to say, if security through obscurity were the primary protection mechanism), proprietary behemoths such as Microsoft would produce the most secure software in the world.

pfSense, an open-source software product from Netgate, confronts both of these notions. Built on the FreeBSD operating system, and earning its name because it makes “sense” of the packet filter software (_pf_) that drives it, pfSense is among the most popular options in the market. It can be used effectively for anything from a SOHO (Small Office/Home Office) infrastructure to a data center environment. pfSense provides a robust set of features within an intuitive web-based graphical interface, as well as support for a wide range of packages (including IDS/IPS systems) and a trove of comprehensive and actively-maintained documentation. pfSense is also available as pre-configured hardware and virtual appliances for flexible and streamlined deployments.

As with any firewall, a pfSense deployment should begin with a detailed configuration plan based on the role of the firewall in the organization. Considerations when constructing such a plan may include the number and addresses of interfaces required for the device in order to support its position in the network, as well as any high-availability and redundancy requirements; the supporting structures the firewall depends on, including the time server it should synchronize with, and the DNS server it should query for name resolution (or, in some cases, how it will perform the resolution itself); and the security controls required for each network or zone under its protection. The importance of the planning stage should not be overlooked; a well thought-out plan will ensure fewer iterations on the configuration, provide a well-tested template for future deployments, and reduce the troubleshooting time in the event of misconfigurations by having a well-defined baseline to reference.

The most common deployment case for a pfSense machine is a perimeter firewall. Minimally, this consists of the two primary interfaces/zones: a LAN interface to support a Local Area Network, and a WAN interface to support a Wide Area Network (most often the public Internet). However, a common third implementation is a DMZ interface. DMZ, a term co-opted from military terminology, stands for de-militarized zone, and refers to a zone that exists between a LAN and WAN, both physically and in terms of its security. The role of a DMZ is to isolate internal hosts that require exposure to an untrusted network, such as the public Internet, on a special network segment. The effect is to limit the impact of a compromised machine to the DMZ, avoiding any direct exposure to sensitive machines and data on the LAN.

In this lab, you will plan the physical implementation of a pfSense virtual router/firewall appliance. The pfSense virtual appliance is a current-generation product that has much of the functionality and options that will be found in most firewall products, though the implementation may vary somewhat from firewall to firewall. Next, you will configure the pfSense appliance according to your planning document and test your configurations.

# Section 1

<u>Part 1- Plan the Physical Configuration of the Firewall</u>

On the vWorkstation desktop, **double-click** the **PFSENSE-FW-PHYSICAL-PLANNER file** to open the spreadsheet in OpenOffice.

*You will use the tabs on this spreadsheet to document the physical configuration for the pfSense virtual firewall/router appliance. The first item on the General tab is the Hostname.*

SS1
<img width="1911" height="870" alt="Screenshot 2025-09-21 140608" src="https://github.com/user-attachments/assets/b711286a-abb4-47d3-97fb-cea09f834fd8" />

At the Hostname row, **type _yourname_-pfSense** in the Settings column, replacing _yourname_ with your own name, to give a unique name to this firewall configuration. Do not include spaces when typing your name.

*A hostname is the unique name of the computer (host) on the network capable of originating or responding to an interaction using the Internet Protocol.*

In the Comments column of the Hostname row, **type _today’s date_** to record the date the configuration was planned.

At the Domain row, **type localdomain** in the Settings column to indicate this firewall is not on a domain network.

*If this firewall was part of a domain, you would enter the domain address here, such as securelabsondemand.com. Otherwise, localdomain is the default entry for pfSense, and is combined with the hostname to create the firewall’s fully qualified domain name.*

At the Primary and Secondary DNS Server rows, type the following static IP addresses in the Settings column:

- Primary DNS Server: **8.8.8.8**
- Secondary DNS Server: **8.8.4.4**

At both the Primary DNS Server and Secondary DNS Server rows, **type Do Not Override DNS** in the Comments column.

At the Time Server Hostname row, **type 0.pfsense.pool.ntp.org** in the Settings column.

*In a real-world scenario, this information should be provided by the network administrator (or your ISP).*

At the Time Zone row, **type Etc/GMT-7** in the Settings column to document that this pfSense firewall implementation will use Pacific Time.

*In a real-world scenario, this information should also be provided by the network administrator (or your ISP).*

At the Admin Password row, **type P&ss9999** in the Settings column.

SS2
<img width="1915" height="772" alt="Screenshot 2025-09-21 141100" src="https://github.com/user-attachments/assets/81d5cd65-b767-4c37-8cd0-c4b5534e4b43" />

At the bottom of the OpenOffice spreadsheet, **click** the **WAN tab** to define the configuration details for the WAN interface.

SS3
<img width="1353" height="637" alt="Screenshot 2025-09-21 141239" src="https://github.com/user-attachments/assets/a9e0db15-a4bb-4493-add4-c444d17de99d" />

At the Description row, **type WAN** in the Comments column.

At the Interface Type row, **type Static** in the Settings column.

*The pfSense Firewall Setup Wizard offers a choice of DHCP, Static, PPP, PPPoE, PPTP, and L2TP interface types. This interface will use a static connection.*

At the MAC address row, **type Not Required** in the Comments column.

*In this lab environment, there is no interface that will require a specific MAC address. If required by your network configuration, you would type the source MAC address in the Settings column.*

At the MTU (Maximum Transmission Unit) row, **type Default** in the Comments column.

*For compatibility with the widest range of networks, pfSense enables you to specify an MTU size or accept a default value. If you do not specify an MTU value, pfSense will assume an MTU of 1500 bytes for this configuration type.

At the MSS (Maximum Segment Size) row, **type Default** in the Comments column.

*No segment size needs to be specified for this network. If you do not specify an MSS value, pfSense will assume an MSS of 1500 bytes for this configuration type.*

At the IP address row, **type 202.20.1.1** in the Settings column to specify the firewall’s external (WAN) IP address, then **type IPv4** in the Comment column.

At the Subnet Mask row, **type ’24** in the Settings column to specify the subnet mask.

*OpenOffice requires the apostrophe to properly format the 24 entry as a character and not a formula. The 24 entry indicates a 24-bit Classless Interdomain Routing (CIDR) subnet mask.*

At the Upstream Gateway row, **type 202.20.1.2** in the Settings column.

*Normally this is provided by your ISP and will be the default route to the internet.*

At the DHCP Hostname row, **make no changes**, because this network is configured for a static connection.

*A DHCP hostname is not required in this configuration, though some Internet Service Providers require it (for security and verification reasons).*

At the Point-to-Point Protocol over Ethernet (PPPoE) rows, **make no changes**.

*The virtual lab does not use Point-to-Point over Ethernet Protocol.*

At the Point-to-Point Tunneling Protocol (PPTP) rows, **make no changes**.

At the Block RFC1918 Networks row, **type Block** in the Settings column.

*On a production “Internet-facing” firewall, you will almost always block RFC1918 Private Networks.*

At the Block bogon networks row, **type Do not block** in the Settings column.

SS4
<img width="1915" height="773" alt="Screenshot 2025-09-21 141736" src="https://github.com/user-attachments/assets/ff9471f9-e7fd-47f3-a54a-4a52f104109e" />

**Repeat steps 11-24** for the **LAN tab** in the OpenOffice spreadsheet, using the following values:

- Description: **LAN**
- Interface Type: **Static**
- MAC Address: **Not Required**
- MTU: **Default**
- MSS: **Default**
- IP address: **172.30.0.1**

 This is the internal interface to which you will be connecting in order to manage the pfSense firewall configuration from the WebGUI and serves as the default gateway for all hosts on the local network.  
 
- Subnet Mask: **'24**
- Upstream Gateway: **Not Required**
    Specifying a gateway would result in pfSense treating this as a WAN interface for the purpose of effecting NAT (Network Address Translation) and related functions. For internal interfaces, such as LAN or DMZ, this is not desirable.

- Block RFC1918: **Do not block**  
  
    As this is the internal interface, it resides in a private address space described by RC1918. Blocking these private addresses would block internal hosts from reaching the firewall, as well as any networks it stands between.  

- Block bogon networks: **Do not block**


SS5
<img width="1917" height="780" alt="Screenshot 2025-09-21 141938" src="https://github.com/user-attachments/assets/95903a03-a949-49f9-933f-19a2f05f0317" />

<u>Part 2 - Configure the LAN and WAN Firewall Interfaces</u>

From the Virtual Machine menu, **select** **pfSense-in** from the Virtual Machine dropdown menu to connect to the pfSense console.

SS6
<img width="1045" height="558" alt="Screenshot 2025-09-21 142221" src="https://github.com/user-attachments/assets/d57538f2-989c-41cb-b293-e4a523848d6f" />

At the pfSense console menu, **type 2** and **press Enter** to select the Set interface(s) IP address option.

At the _Enter the number of the interface you wish to configure_ prompt, **type 2** and **press Enter** to select the LAN interface for configuration.

SS7
<img width="1142" height="546" alt="Screenshot 2025-09-21 142315" src="https://github.com/user-attachments/assets/a48606dd-d0ae-4601-a92d-897e00ee9143" />

At the _Enter the new LAN IPv4 address_ prompt, **type 172.30.0.1** to assign the private address to the LAN interface, as specified in your worksheet.

*This is the address you will use to connect to the pfSense WebGUI from a local browser.*

At the _Enter the new LAN IPv4 subnet bit count_ prompt, **type 24** to add the subnet mask to the LAN IP address, as specified in your worksheet.

SS8
<img width="1012" height="587" alt="Screenshot 2025-09-21 142419" src="https://github.com/user-attachments/assets/a0bc70d5-e2cd-4f80-8a4d-9473c3b16c7f" />

At the prompt for an upstream gateway address, **press Enter** to specify none.

At the _Enter the new LAN Ipv6 address_ prompt, **press Enter** to specify none.

At the _Do you want to enable the DHCP server on LAN?_ prompt, **type n** and **press Enter** to decline and complete the IP assignment on the LAN interface.

*pfSense will take a few moments to reload the configuration with your changes. Upon completion, it will display the web address you will use to access the WebGUI. Once you see this address, you may continue to the next step.*

From the Virtual Machine menu, **select** **vWorkstation** from the Virtual Machine dropdown menu to connect to the vWorkstation.

From the vWorkstation taskbar, **click** the **Chrome icon** to open a new browser window

In the browser’s navigation bar, **type 172.30.0.1** and **press Enter** to access the pfSense WebGUI.

SS9
<img width="1897" height="873" alt="Screenshot 2025-09-21 142656" src="https://github.com/user-attachments/assets/bc8bc815-c962-4a6a-af0c-e97c5e971a3c" />

At the pfSense log-in screen, **type** the following credentials and **click Sign in** to log in to the pfSense firewall using the default administrator username and password.  

- Username: **admin**
- Password: **pfsense**

From the pfSense menu bar, **click System** and **select Setup Wizard** to open the pfSense Setup Wizard.

SS10
<img width="1892" height="771" alt="Screenshot 2025-09-21 142940" src="https://github.com/user-attachments/assets/5873fb40-0726-46ea-b965-dfecb41baf43" />

At the pfSense Setup page, **click Next** to proceed to the Netgate Global Support page.

At the Netgate Global Support page, **click Next** to proceed to the General Information page.  
  
*Starting on this page, you will use the entries in the Settings column of the Physical Configuration worksheet to complete the fields required by the pfSense Setup Wizard.*

On the General Information page, **type _yourname_-pfSense** in the Hostname field, as specified in your Settings column.

On the General Information page, **type localdomain** in the Domain field, as specified in your Settings column.

On the General Information page, **type** the following IP addresses for the Primary and Secondary DNS Servers, as specified in your Settings column.

- Primary DNS Server: **8.8.8.8**
- Secondary DNS Server: **8.8.4.4**

SS11
<img width="1565" height="607" alt="Screenshot 2025-09-21 143108" src="https://github.com/user-attachments/assets/4fefbb33-5b36-43ab-8690-84682f12ee71" />

On the General Information page, **click** the **Override DNS checkbox** to deselect it.

On the General Information page, **click** **Next** to continue to the Time Server Information page.

On the Time Server Information page, **type 0.pfsense.pool.ntp.org** in the Time server hostname field, as specified in your worksheet.

On the Time Server Information page, **select Etc/GMT-7** from the Timezone menu, as specified in your worksheet.

SS12
<img width="1512" height="436" alt="Screenshot 2025-09-21 143232" src="https://github.com/user-attachments/assets/40fba5f2-df61-44a6-a27c-9922f0d6556a" />

On the Time Server Information page, **click Next** to continue to the Configure WAN Interface page.

On the Configure WAN Interface page, **select** the **Static option** from the SelectedType menu, as specified in your worksheet.

In the General configuration section, **leave the MAC Address, MTU, and MSS fields blank**, as specified in your worksheet.

SS13
<img width="1461" height="582" alt="Screenshot 2025-09-21 143351" src="https://github.com/user-attachments/assets/6acf0407-c990-4aa8-9093-7fb497eb7762" />

In the Static IP Configuration section, **type 202.20.1.1** in the IP address field, as specified in your worksheet.

In the Static IP Configuration section, **select 24** from the Subnet Mask menu, as specified in your worksheet.

In the Static IP Configuration section, **type 202.20.1.2** in the Upstream Gateway field, as specified in your worksheet

SS14
<img width="1501" height="220" alt="Screenshot 2025-09-21 143627" src="https://github.com/user-attachments/assets/524d492b-24cb-43f3-971a-f00d62bc66bd" />

In the RFC1918 Networks section, **confirm** the **_Block RFC1918 Private Networks_ checkbox is selected**, as specified in your worksheet.

In the Block bogon networks section, **click** the **Block bogon networks checkbox** to deselect it, as specified in your worksheet.

SS15
<img width="1587" height="396" alt="Screenshot 2025-09-21 143704" src="https://github.com/user-attachments/assets/44f187d9-eee3-4b5d-9ab5-262ace666a05" />

**Click Next** to continue to the Configure LAN Interface page.

On the Configure LAN Interface page, **click Next** to accept the LAN Interface settings you configured from the console and continue to the Set Admin WebGUI Password page.

SS16
<img width="1581" height="378" alt="Screenshot 2025-09-21 143739" src="https://github.com/user-attachments/assets/9999ca3b-b81e-4442-89cd-f10203a524a3" />

On the Set Admin WebGUI Password page, **type P&ss9999** in both the Admin Password and Admin Password AGAIN fields, then **click Next** to save the password change and continue to the Reload configuration page.

SS17
<img width="1363" height="351" alt="Screenshot 2025-09-21 143818" src="https://github.com/user-attachments/assets/7f2e5a06-b1b7-4061-9e6a-c8a60d043e6f" />

On the Reload configuration page, **click Reload** to reload pfSense with your changes.

On the Wizard completed page, **click** the **Finish** button at the bottom to return to the pfSense dashboard.

<u>Part 3 - Verify the Firewall Implementation</u>

From the vWorkstation taskbar, **click** the **Command Prompt icon** to open a new Command Prompt window.

At the command prompt, **type ping 202.20.1.2** and **press Enter** to send an ICMP request to pfSense’s upstream gateway.

SS18
<img width="1475" height="587" alt="Screenshot 2025-09-21 144853" src="https://github.com/user-attachments/assets/c312baa3-94c3-4665-8f50-058baafee8c4" />

At the command prompt, **type exit** and **press Enter** to close the command prompt window.

On the Lab View toolbar, **select** the **RemoteWindows01 machine** from the Virtual Machine menu to open a connection to the RemoteWindows01 machine.

*The RemoteWindows01 machine is located on a different network on the WAN side of the pfSense firewall.*

From the RemoteWindows01 taskbar, **click** the **Command Prompt icon** to open a new Command Prompt window.

At the command prompt, **type ping 202.20.1.1** and **press Enter** to send an ICMP request to the WAN interface of the pfSense firewall.

SS19
<img width="1395" height="617" alt="Screenshot 2025-09-21 145018" src="https://github.com/user-attachments/assets/4809a167-6ace-4d58-8b6f-d82a77387012" />

# Section 2

<u>Part 1 - Plan the Physical Configuration of the Firewall</u>

On the vWorkstation desktop, **open** the **_yourname__PFSENSE-FW-PLANNER.ods** spreadsheet that you saved in Section 1.

In the Physical Configuration worksheet, **open** the **DMZ tab**.

On the DMZ tab, **document** the following physical configuration settings.

- Description: **DMZ**
- Interface Type: **Static IPv4  
- MAC Address: **n/a**
- MTU: **n/a**
- MSS: **n/a**
- IP Address: **172.40.0.1**
- Subnet Mask: **‘24**
- Upstream Gateway: **n/a**
- Block RFC1918 networks: **Yes**
- Block bogon networks: **No**

SS20
<img width="1552" height="707" alt="Screenshot 2025-09-21 145221" src="https://github.com/user-attachments/assets/8da187e0-02dd-4f19-bb52-30d3e76b0b8f" />

<u>Part 2 - Configure the DMZ Firewall Interface</u>

**Open** the **pfSense WebGUI**.

*If necessary, log in using the username admin and the password P&ss9999.*

From the pfSense menu bar, **select Interfaces > Assignments** to open the Interface management settings.

On the Interface Assignments page, **click** the **Add button** to assign a new interface to the vmx2 network port.

On the Interface Assignments page, **click** the **new OPT1 interface** to edit the settings for this Interface.

In the General Configuration section, **click** the **Enable checkbox** to enable this interface.

Use the details from the DMZ tab of your planner to **complete** the **configuration**, then **click Save**.

SS21
<img width="1446" height="663" alt="Screenshot 2025-09-21 145717" src="https://github.com/user-attachments/assets/cfcc2083-9f41-4d86-b850-44be400508a9" />

SS22
<img width="1628" height="617" alt="Screenshot 2025-09-21 145729" src="https://github.com/user-attachments/assets/0b445c96-1edb-4932-a094-94424f60a9d4" />

When prompted, **click Apply Changes** to apply your changes.

**Navigate** to the **pfSense dashboard**.

SS23
<img width="1495" height="612" alt="Screenshot 2025-09-21 151831" src="https://github.com/user-attachments/assets/b29f96a8-d9a3-48db-b073-a534a36f13ba" />

<u>Part 3 - Verify the Firewall Implementation</u>

From the Virtual Machine menu, **connect** to the **RemoteWindows01 machine**.

**Open** a new **Command Prompt window**.

At the command prompt, **execute the command** to ping the DMZ interface of the firewall.

```cmd
ping 172.40.0.1
```

SS24
<img width="1322" height="577" alt="Screenshot 2025-09-21 151943" src="https://github.com/user-attachments/assets/19955a7d-9c15-419d-b9c9-9d45fdbdb644" />

From the RemoteWindows01 desktop, **open** a new **browser window**.

In the web browser, **navigate** to **corporationtechs.com**.

*Corporationtechs.com is a website hosted on the TargetLinux01 web server. Since a rule exists that permits traffic into the DMZ, if your DMZ interface was properly configured, the website should load without any issues.*

SS25
<img width="1886" height="772" alt="Screenshot 2025-09-21 152034" src="https://github.com/user-attachments/assets/309ff19e-e7f1-42cc-99ab-5849462887ef" />

