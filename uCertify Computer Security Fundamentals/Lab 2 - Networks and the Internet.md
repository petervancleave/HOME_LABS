
### 2.5.1 Using the tracert Command

In this lab, you will learn to use the `tracert` command. It is used for viewing various details about the path that a packet takes from the source to the destination computer/device.  
To use the `tracert` command, here's what you need to do:

1. Click the **Check** button to check if the machine is initialized properly, whether a PowerShell process is running in the background, and whether you can proceed with the task or not.

2. From the desktop, open **Google Chrome**

SS1

3. In the **Google Chrome** window, in the address bar, type URL as _`google.com`_ and press **Enter**

4. In the bottom left corner of the screen, click the **Start** icon, and from the right pane, open **Windows PowerShell**.

SS2

5. In the **Administrator: Windows Powershell** window, execute the following command:

SS3

6. Close all windows

### 2.5.2 Using the Ping Command

In this lab, you will learn to use the ping command. The ping command is used to test the ability of the source computer to reach a specified destination computer.

1. Click the **Check** button to check if the machine is initialized properly, whether a PowerShell process is running in the background, and whether you can proceed with the task or not.
2. In the bottom left corner of the desktop, click the **Start** icon, and from the right pane, open **Windows PowerShell**.

3. In the **Administrator:** **Windows PowerShell** window, execute the following command to ping the hostname **www.example.com**:

```javascript
ping -n 5 -l 1500 www.example.com
```

SS4

### 2.5.3 Using Routes

In this lab, you will learn to use routes in a network. Routing Information Protocol (RIP) is a dynamic routing protocol that uses hop count as a routing metric to find the best path between the source and the destination network. It is a distance-vector routing protocol that has AD value 120 and works on the application layer of the OSI model. RIP uses port number 520.

1. **Important:** Click the **Check** button to check if the machine is initialized properly and no PowerShell process is running in the background and if you can proceed with the task or not.

2. Click the **Start** menu, click **Windows PowerShell**.
3. In the **Administrator: Windows PowerShell** window, type the following command and press **Enter** to show a list of network adapters (or interfaces) on the local computer, including each of the MAC addresses:

```
route print
```

SS5

4. Type the following command and press **Enter** to add a new route in the IPv4 Route Table:

```
route add 193.168.1.0 mask 255.255.255.0 193.168.1.1
```


5. Type the following command and press **Enter** to print the new route in the IPv4 Route Table:

```
route print
```

SS6

6. Type the following command and press **Enter** to close the **Windows PowerShell** window:

```
exit
```


### 2.5.4 Using the netstat Command

In this lab, you will learn to use the netstat command. It is a networking utility that identifies a computer’s listening ports, along with incoming and outgoing network connections. To use the netstat command, here's what you need to do:

1. Click the **Start** menu and open **Windows P****owerShell**.
2. Execute the following commands in the **Windows PowerShell** window to list all the computer’s connections and listening ports:

```
netstat -a
```

3. Execute the following command in the **Windows PowerShell** window to check if a process starts listening on TCP port 23:

```
netstat -a | findstr ':23'
```

SS7

4. Drag the **Windows PowerShell** window to the left side of the screen.
5. Click the **Start** menu and open another **Windows** **PowerShell** window.
6. Drag the second **Windows PowerShell** window to the right side of the screen.
7. Execute the following command in the second **Windows PowerShell** window to enable ssh or remote connection:

```
ssh administrator@localhost -p23
```

8. Type _Yes_ and **password** as _uC@123456_.
9. Go back to the first **Windows** **PowerShell** window and execute the following command:
```javascript
netstat -a | findstr ':23'
```


10. You will observe **State** as **ESTABLISHED** which means there’s an actual connection between your machine and the remote IP and port that is able to exchange traffic.

11. Exit

12. Go back to the first **Windows** **PowerShell** window and execute the following command:

```
netstat -a | findstr ':23'
```


### 2.5.5 Using ARP

In this lab, you will learn to use ARP. ARP (Address Resolution Protocol) is used to map IP addresses to MAC (media access control) addresses To use ARP, here's what you need to do:

1. Click the **Check** button to check if the machine is initialized properly, whether a PowerShell process is running in the background, and whether you can proceed with the task or not.

2. In the bottom left corner of the desktop, click the **Start** icon, and from the right pane, open **Windows PowerShell**.

3. In the **Administrator:** **Windows PowerShell** window, execute the following command to display the `arp` cache entry for IP addresses:

```
arp -a
```

SS8


### 2.5.6 Using ipconfig

In this lab, you will learn to use the ipconfig command. It displays all current TCP/IP (Transmission Control Protocol/Internet Protocol) network configuration values and refreshes DHCP (Dynamic Host Configuration Protocol) and DNS (Domain Name System) settings. To use the ipconfig command, here's what you need to do:

1. Click the **Check** button to check if the machine is initialized properly, whether a PowerShell process is running in the background, and whether you can proceed with the task or not.
2. In the bottom left corner of the desktop, click the **Start** icon, and from the right pane, open **Windows PowerShell**.
3. In the **Administrator:** **Windows PowerShell** window, execute the following command to display the information pertaining to your network adapter, namely, TCP/IP configurations:

```javascript
ipconfig
```

SS9

4. Execute the following command to display the full TCP/IP configuration for all adapters:

```javascript
ipconfig /all
```

SS10

5. Execute the following command to display the help file for `ipconfig`:

```javascript
ipconfig /?
```

SS11

6. Execute the following command to close the **Administrator: Windows PowerShell** window:
```javascript
exit
```


### 2.5.7 Using the nslookup Command for Passive Reconnaissance

In this lab, you will learn to use the nslookup command for passive reconnaissance. It can be used to connect with your network's DNS (Domain Name System) server and to verify whether the DNS server is running. To use the nslookup command for passive reconnaissance, here's what you need to do:

1. From the left sidebar, click the **Terminal** icon

2. In the **Terminal** window, execute the following command to find the mail servers for the **www.example.com** website:

```javascript
nslookup www.example.com 8.8.8.8
```

SS12