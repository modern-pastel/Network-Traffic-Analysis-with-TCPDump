# Network-Traffic-Analysis-with-TCPDump
Utilize TCPDump to capture and analyze TCP traffic. This project uses Linux commands, pipes, and input/output redirection
## Objective

Set up Elastic Stack for Security Information and Event Management (SIEM) using the Elastic Web portal and a Kali Linux virtual machine. This process involved generating security events on the Kali VM, configuring an agent to send data to the SIEM, and exploring how to query and analyze logs within the SIEM platform

### Skills Learned

- Successfully set up and configured Elastic Stack SIEM in a home lab environment
- Proficiency in deploying a Kali Linux VM
- Configre elastic agents for log collection
- Forwarding data to the SIEM for effective security event monitoring
- Developed a custom dashboard to visualize security events
- Successfully created and tested alert rules for detecting specific security events

### Tools Used

- Elastic Stack SIEM system for log ingestion and analysis.
- Kali Linux VM
- Telemetry generation tools to create network traffic

## Steps
1. Create an Elastic Stack account and set up Linux VM. I had previously installed Linux onto my PC before starting this lab
2. Setting up the Agent to Collect Logs.
   - Used the Kibana main menu bar and clicked on the "Add Integrations" button on the bottom.
![image](https://github.com/user-attachments/assets/087da525-0c2a-4321-882e-53dc0bb422e9)
  - Then searched for "Elastic Defend", opened the integration page, and clicked on "Install Elastic Agent"
![image](https://github.com/user-attachments/assets/839abaa8-e82e-464b-9917-53e4162b3086)
  - Copied the command to install the Elastic Agent and pasted that into the Kali terminal (command line)
![image](https://github.com/user-attachments/assets/fd5bb61e-6d1d-479d-844f-23c7ee71f719)
![image](https://github.com/user-attachments/assets/2c4b9d44-9c60-4ca9-8984-9da145cb006c)
3. Generating Security Events on the Kali VM
  - Run NMAP scans

![image](https://github.com/user-attachments/assets/b0537934-85b3-4328-a955-3a20d28d6de0)

4. Querying for Security Events in the Elastic SIEM
   - Go back to the menu icon in Kibana, and under the observability tab, click on logs.
   - In the search bar, I used the query: process.args:"sudo"
![image](https://github.com/user-attachments/assets/effc0b80-5cfc-4de3-9504-d7639053acc8)

  - I can then look at and analyze different events through the log details
![image](https://github.com/user-attachments/assets/996733e8-8380-4201-9833-e06737243c1f)

5. Create a dashboard to visualize events
   - Under the icon menu with the 3 lines in the top left, I clicked on the Analytics tab, then dashboard, then create dashboard, then create visualiztion.
   - Select “Area” as the visualization type. Select "Count" as the vertical field type, and "Timestamp" for the horizontal field. This will create a chart that shows the count of events over time.
   - This is what the dashboard ends up looking like:
   
![image](https://github.com/user-attachments/assets/707b9916-5254-4f0b-a329-3e9d8f83cb0d)

6. Create an Alert
   - The final step for this lab was creating alerts.
   - Click on the menu icon on the top-left, then under “Security,” click on “Alerts.” Click on “Manage rules” at the top right. Click on the “Create new rule” button at the top right. Under the “Define rule” section, select the “Custom query” option from the dropdown menu. Under “Custom query,” set the conditions for the rule. I used the query event.action:"nmap_scan". Set the severity level for the alert to high. Keep all the other default settings under “Schedule rule” and click “Continue.”
![image](https://github.com/user-attachments/assets/4b1bec07-fa90-4794-9bf4-de0c16ef3413)

  - In the "Rules Action" section. I have it setup to send an email notification when the rule is triggered.
  - Finally, click the “Create and enable rule” button to create the alert.
![image](https://github.com/user-attachments/assets/3d017875-4a62-41be-ad8b-999b8c2a37ed)

This SIEM monitors logs for Nmap scan events. If an Nmap scan event is detected, the alert will be triggered and an email will be sent to me.
