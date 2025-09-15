# Building a Home SOC in Azure with Microsoft Sentinel

## Objective
[Brief Objective - Remove this afterwards]

In this project, I built a basic home Security Operations Center (SOC) from scratch in Microsoft Azure. I created a virtual machine (VM) and intentionally exposed it to the internet as a honeypot to collect real-world attack data. I then forwarded security logs into a centralized repository and integrated Microsoft Sentinel to analyze and visualize attack patterns.

### This project allowed me to demonstrate hands-on skills in:

* Cloud security architecture (Azure Resource Groups, VNets, NSGs, and VMs)
* Honeypot deployment for real-world attack telemetry
* Log forwarding & enrichment with Azure Monitor and Log Analytics
* Threat detection & visualization with Microsoft Sentinel and KQL queries
* Practical SOC operations — from log ingestion to attack mapping

### Tools Used
[Bullet Points - Remove this afterwards]

- Security Information and Event Management (SIEM) system for log ingestion and analysis.
- Network analysis tools (such as Wireshark) for capturing and examining network traffic.
- Telemetry generation tools to create realistic network traffic and attack scenarios.

## Steps 
1. Create a Resource Group

I began by creating a dedicated resource group to logically contain all assets for this SOC lab.

![Create Resource Group](01%20Create%20resource%20group%20Azure.PNG)

2. Create a Virtual Network

Next, I set up a virtual network (VNet) to host my resources and ensure proper segmentation.
![Create VNet](02%20Create%20virtual%20network%20Azure.PNG)
3. Deploy a Virtual Machine

I deployed a Windows 10 VM inside the SOC lab VNet. This machine acts as the honeypot that attackers would interact with.
![VM Creation Step 1](03%20%20Step%20through%20VM%20creation%201%20Azure.PNG)
![VM Creation Step 2](03%20%20Step%20through%20VM%20creation%202%20Azure.PNG)
4. Verify Deployed Resources

Once deployment was completed, I confirmed all resources (VM, NIC, NSG, disk, and VNet) were grouped under my lab’s resource group.
![Deployed Items](04%20eployed%20items%20in%20RG.PNG)
5. Adjust the Network Security Group

To simulate a vulnerable system, I modified the Network Security Group (NSG) to allow inbound traffic from any source.
![NSG Rules](05%20Adjust%20the%20Network%20Security%20Group..PNG)
6. Modify the Windows Firewall

Inside the VM, I reduced the firewall restrictions to make it easier for attackers to attempt brute-force logins.

![Firewall Settings 1](06%20Modify%20firewall%201.PNG)
![Firewall Settings 2](06%20Modify%20firewall%202.PNG)
7. Generate Failed Logins & Review Logs

I simulated login attempts to trigger security events and validated that they were recorded in Windows Event Viewer.
![Failed Logins](07%20Try%20incorrect%20logins%20and%20check%20logs.PNG)
8. Create a Data Collection Rule

To centralize monitoring, I created a Data Collection Rule (DCR) to forward logs from the VM into Log Analytics.
![DCR Creation](08%20DCR%20creation%20dialog.PNG)
9. Connect Windows Security Events to Sentinel

I connected the VM’s Windows Security Events to Microsoft Sentinel, ensuring security telemetry flowed into my SOC workspace.
![Windows Security Connector](09%20Windows%20Security%20Events%E2%80%9D%20connector..PNG)
10. Confirm Logs in Log Analytics

Using Log Analytics, I confirmed that security events were successfully being ingested from the VM.
![Logs in LAW](10%20Run%20KQL%20query.PNG)
11. Enrich Logs with Geolocation Data

I uploaded geolocation data as a custom watchlist to enrich attacker IPs with location metadata.
![Upload Watchlist](11%20Upload%20geolocation%20data..png)
12. Query to Correlate Events with GeoIP

Using KQL, I joined failed login events with the geoIP watchlist to enrich them with location details.
![KQL Query](12%20Query%20to%20enrich%20events..png)
13. Visualize Attacks on a Map

Finally, I built a Sentinel workbook to map attack origins around the globe.
![Attack Map](13%20windows%20vm%20attack%20map.png)
14. Final Architecture

Here’s the high-level architecture of my SOC lab:![SOC Architecture](Azure%20VM%20Architechture.jpg)
















