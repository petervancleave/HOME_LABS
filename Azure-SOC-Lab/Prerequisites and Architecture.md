### Prerequisites:

- Azure account with credits (In my case, I use a student account from my school to get free credits. If want to signup for Azure with a student account, go to portal.azure.com and sign up via school email). 
- Familiarity with CLI tools (Powershell, BASH), Python.
- Free API keys - Sign up for AbuseIPDB (abuseipdb.com) and VirusTotal (virustotal.com)
- Azure CLI (install from docs.microsoft.com/en-us/cli/azure/install-azure-cli, Python 3.x. (AZURE CLI IS OPTIONAL).
- A public MaxMind GeoLite2-City CSV or similar free geolocation dataset

### Project Architecture:

- Azure Resource Group - container for all resources
- Virtual Network (VNet) and Network Security Group (NSG) - provides networking for the VM; NSG to open ports to expose the honepot.
- Honeypot VM - Windows 10 VM with firewall disabled and ports open to capture attacks.
- Log Analytics Workspace - central repo for logs from the VM.
- Sentinel - SIEM linked to the workspace for querying via KQL, alerts, workbooks.

### Data Flow: 

1. Attacks hit VM
2. Logs generate
3. Azure Monitor Agent forwards to workspace
4. Sentinel queries
5. Visualize incidents

```text

Real Attackers --> [Exposed Ports (NSG)] --> Honeypot VM (Windows, Logs via Event Viewer)
                                    |
                                    v
Azure Monitor Agent --> Log Analytics Workspace (Raw Logs)
                                    |
                                    v
Microsoft Sentinel (KQL Queries, Geolocation Join, Attack Map Workbook)

```
