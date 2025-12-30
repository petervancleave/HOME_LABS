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

### Basic Outline

Set Up Azure Basics:
Log into portal.azure.com with your student account.
Create a Resource Group: Search "Resource groups" > Create > Name: "rg-soclab", Region: East US 2.
Create Virtual Network: Search "Virtual networks" > Create > Name: "vnet-soclab", attach to resource group, default subnet.

Deploy Honeypot VM:
Search "Virtual machines" > Create > Basics: Resource group "rg-soclab", Name: "corpnet-east1" (generic to avoid suspicion), Image: Windows 10/11, Size: Standard B1s (cheap).
Networking: Attach to "vnet-soclab", create public IP.
Security: Set admin username/password (note them down).
Review + Create, then wait for deployment.
Disable Firewall: RDP into VM (use public IP and credentials), open Windows Defender Firewall > Turn off all profiles.
Open Ports: In portal, go to VM > Networking > Add inbound rule: Allow any source/port/protocol (high risk – for lab only).

Create Log Analytics Workspace:
Search "Log Analytics workspaces" > Create > Name: "law-soclab", attach to "rg-soclab", Region: East US 2.

Connect VM to Workspace:
Install Agent: In workspace > Agents > Download Windows agent, but use portal extension: VM > Extensions > Add "AzureMonitorWindowsAgent".
Create Data Collection Rule (DCR): Search "Data collection rules" > Create > Name: "dcr-soclab", attach to resource group/workspace > Resources: Add VM > Data sources: Add "Windows event logs" (Security, filter for Event ID 4625) > Review + Create.
Wait 20-40 minutes for logs to flow (test by querying in workspace).

Set Up Microsoft Sentinel:
Search "Microsoft Sentinel" > Add > Select "law-soclab" workspace > Enable 31-day trial.
Install Connector: In Sentinel > Content hub > Search "Windows Security Events" > Install > Create connector.

Query Logs with KQL:
In Sentinel > Logs > Run query: SecurityEvent | where EventID == 4625 | project TimeGenerated, Account, IpAddress | order by TimeGenerated desc.
Filter recent: Add | where TimeGenerated > ago(5m).

Enrich with Geolocation:
Upload Watchlist: In Sentinel > Watchlists > Add > Name: "GeoIP", upload CSV (columns: IP range, Lat, Long, City, Country).
Enriched Query: SecurityEvent | where EventID == 4625 | lookup kind=leftouter _GetWatchlist('GeoIP') on IpAddress | project TimeGenerated, Account, IpAddress, City, Country.

Create Attack Map:
In Sentinel > Workbooks > New > Add query (use enriched KQL, summarize by City/Country).
Add map visualization: Select "Map" tile, bind to Lat/Long, color by attack count (e.g., green-low, red-high).
Save and monitor for real attacks (logs build up fast).

Monitor and Extend:
RDP to VM > Event Viewer > Windows Logs > Security: View raw failed logins.
In Sentinel: Watch for incidents; optionally add analytic rules for alerts.
Shut down VM when done to save credits.
