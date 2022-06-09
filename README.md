<h1>SIEM in Azure</h1>


<h2>Description</h2>
Project consists of using applications in Azure, such as Virtual Machines, Sentinel, and Log Analytics Workspace to create a SIEM in Azure. I am basically using the VM as a honeypot to attract hackers and bots to attempt to log into my VM. I used Sentinel, Log Analytics Workspace, and the website ipgeolocation in order to collect location data on the hackers attempting to log into our honeypot. In the VM, I used a Powershell script that looks for EventID 4625 in our VM to notify our SIEM when an attack occurs, and ipgeolocation shows us where the attack comes from, with timestamp and attempt username credential.
<br />


<h2>Utilities Used</h2>

- <b>Microsoft Azure</b> 
- <b>Virtual Machines in Azure</b>
- <b>Microsoft Sentinel in Azure</b>
- <b>Log Analytics workspaces in Azure</b>
- <b>PowerShell</b>
- <b>ipgeolocation.com</b>

<h2>Environments Used </h2>

- <b>Windows 10</b> (21H2)

<h2>Program walk-through:</h2>

<p align="center">
Pulled up the Azure Portal and search for "Virtual Machines" in Azure: <br/>
<img src="https://i.imgur.com/ufL3CgP.png" height="80%" width="80%" alt="SIEM in Azure Steps"/>
<br />
<br />
Create Azure Virtual Machine:  <br/>
<img src="https://i.imgur.com/aUJpRJ7.png" height="80%" width="80%" alt="SIEM in Azure Steps"/>
<br />
Used the following settings for Basics:  <br/>
<img src="https://i.imgur.com/G2goxSW.png" height="80%" width="80%" alt="SIEM in Azure Steps"/>
<br />
  <br/>
<img src="https://i.imgur.com/G5auuSm.png" height="80%" width="80%" alt="SIEM in Azure Steps"/>
<br />
 <br/>
<img src="https://i.imgur.com/TZ3vMfs.png" height="80%" width="80%" alt="SIEM in Azure Steps"/>
<br />
Used the following settings for Disks: <br/>
<img src="https://i.imgur.com/m8WhLnY.png" height="80%" width="80%" alt="SIEM in Azure Steps"/>
<br />
Used the following settings for Networking. <br/>
<img src="https://i.imgur.com/OfgwnLe.png" height="80%" width="80%" alt="SIEM in Azure Steps"/>
<br />
Created Network Security Group and use the following settings:  <br/>
<img src="https://i.imgur.com/VJy60mF.png" height="80%" width="80%" alt="SIEM in Azure Steps"/>
<br />
Review + Create and Created Virtual Machine: <br/>
<img src="https://i.imgur.com/FWTiqBw.png" height="80%" width="80%" alt="SIEM in Azure Steps"/>
<br />
Deployment is now in progress:  <br/>
<img src="https://i.imgur.com/EEEm7Jx.png" height="80%" width="80%" alt="SIEM in Azure Steps"/>
<br />
While Deployment was happening, I pulled up Log Analytics Workspace through the search bar:  <br/>
<img src="https://i.imgur.com/sfwu1f3.png" height="80%" width="80%" alt="SIEM in Azure Steps"/>
<br />
I created a new workspace with the following settings: <br/>
<img src="https://i.imgur.com/PLTpVHj.png" height="80%" width="80%" alt="SIEM in Azure Steps"/>
<br />
Hit create:  <br/>
<img src="https://i.imgur.com/knPASqz.png" height="80%" width="80%" alt="SIEM in Azure Steps"/>
<br />
Deployment then in progress for the new workspace:  <br/>
<img src="https://i.imgur.com/0qXszK4.png" height="80%" width="80%" alt="SIEM in Azure Steps"/>
<br />
Navigated to Microsoft Defender for Cloud:  <br/>
<img src="https://i.imgur.com/FlfzZwn.png" height="80%" width="80%" alt="SIEM in Azure Steps"/>
<br />
Navigated to Environment Settings:  <br/>
<img src="https://i.imgur.com/39IpfSJ.png" height="80%" width="80%" alt="SIEM in Azure Steps"/>
<br />
Clicked on Azure Subcription settings and set the following settings in place:  <br/>
<img src="https://i.imgur.com/9stJcCZ.png" height="80%" width="80%" alt="SIEM in Azure Steps"/>
<br />
Applied settings: <br/>
<img src="https://i.imgur.com/WBj75xy.png" height="80%" width="80%" alt="SIEM in Azure Steps"/>
<br />
Navigated back to Log Analytics Workspace:  <br/>
<img src="https://i.imgur.com/P00K5Fp.png" height="80%" width="80%" alt="SIEM in Azure Steps"/>
<br />
Opened up the workspace and navigated to the Virtual Machines tab:  <br/>
<img src="https://i.imgur.com/Dj0u2HH.png" height="80%" width="80%" alt="SIEM in Azure Steps"/>
<br />
Connected the Virtual Machine I made earlier to the workspace:  <br/>
<img src="https://i.imgur.com/HEk2OXt.png" height="80%" width="80%" alt="SIEM in Azure Steps"/>
<br />
Navigated to Microsoft Sentinel:  <br/>
<img src="https://i.imgur.com/QkcRpwU.png" height="80%" width="80%" alt="SIEM in Azure Steps"/>
<br />
Added Microsoft Sentinel to a workspace:  <br/>
<img src="https://i.imgur.com/aw2AqNI.png" height="80%" width="80%" alt="SIEM in Azure Steps"/>
<br />
Started up the Virtual Machine:  <br/>
<img src="https://i.imgur.com/dl2WDc3.png" height="80%" width="80%" alt="SIEM in Azure Steps"/>
<br />
Opened Remote Desktop Connection to connect to the VM and typed in credentials I made for the VM: <br/>
<img src="https://i.imgur.com/o9YjZeM.jpg" height="80%" width="80%" alt="SIEM in Azure Steps"/>
<br />
Pressed Yes:  <br/>
<img src="https://i.imgur.com/tKl2ZWl.png" height="80%" width="80%" alt="SIEM in Azure Steps"/>
<br />
Connected to the VM and turned off the privacy settings on the VM:  <br/>
<img src="https://i.imgur.com/vkQC7sD.png" height="80%" width="80%" alt="SIEM in Azure Steps"/>
<br />
Made it to the VM homescreen:  <br/>
<img src="https://i.imgur.com/KJzTQAh.png" height="80%" width="80%" alt="SIEM in Azure Steps"/>
<br />
Opened Edge:  <br/>
<img src="https://i.imgur.com/a1zQVMC.png" height="80%" width="80%" alt="SIEM in Azure Steps"/>
<br />
Open Event Viewer in the VM search bar:  <br/>
<img src="https://i.imgur.com/Y6YIwCY.png" height="80%" width="80%" alt="SIEM in Azure Steps"/>
<br />
Navigate to Security and select an Event with EventID 4625. This is what I will be looking for in the SIEM:  <br/>
<img src="https://i.imgur.com/A2cC4XE.png" height="80%" width="80%" alt="SIEM in Azure Steps"/>
<br />
Opened CMD and used the Ping command on my VM's IP Address. Notice how there's no response: <br/>
<img src="https://i.imgur.com/6KtPmca.png" height="80%" width="80%" alt="SIEM in Azure Steps"/>
<br />
Opened Windows Firewall and navigate to Public Profile settings. I turned off the firewall on the VM in order to make our honeypot more enticing:  <br/>
<img src="https://i.imgur.com/ZEcnppz.png" height="80%" width="80%" alt="SIEM in Azure Steps"/>
<br />
Repeated my step by pinging my VM's IP Address, and now have response from it:  <br/>
<img src="https://i.imgur.com/1gNEDqe.png" height="80%" width="80%" alt="SIEM in Azure Steps"/>
<br />
Opened PowerShell SE as an Administrator:  <br/>
<img src="https://i.imgur.com/ZfzJKjo.png" height="80%" width="80%" alt="SIEM in Azure Steps"/>
<br />
With his permission, I used joshmakador1's PowerShell code (https://github.com/joshmadakor1/Sentinel-Lab/blob/main/Custom_Security_Log_Exporter.ps1) for this SIEM and entered it into Powershell. This code is a Log Exporter, which will send our log data to Microsoft Sentinel later:  <br/>
<img src="https://i.imgur.com/1S4ZJl7.png" height="80%" width="80%" alt="SIEM in Azure Steps"/>
<br />
Navigated to ipgeolocation, created an account, and entered in the VM's IP address: <br/>
<img src="https://i.imgur.com/KeRwH2X.png" height="80%" width="80%" alt="SIEM in Azure Steps"/>
<br />
Navigated back to PowerShell on the VM and turned on the program. Several attacks came after the honeypot:  <br/>
<img src="https://i.imgur.com/apZ1xo8.png" height="80%" width="80%" alt="SIEM in Azure Steps"/>
<br />
Navigated to Files Explorer then ProgramData:  <br/>
<img src="https://i.imgur.com/Rb1jqDw.png" height="80%" width="80%" alt="SIEM in Azure Steps"/>
<br />
Opened the failed_rdp file:  <br/>
<img src="https://i.imgur.com/3cQCeoG.png" height="80%" width="80%" alt="SIEM in Azure Steps"/>
<br />
 <br/>
<img src="https://i.imgur.com/MUtqU7f.png" height="80%" width="80%" alt="SIEM in Azure Steps"/>
<br />
Created a custom log in Log Analytics Workspace:  <br/>
<img src="https://i.imgur.com/Dqe0omj.png" height="80%" width="80%" alt="SIEM in Azure Steps"/>
<br />
Copied the data from the failed_rdp file onto a .log file and entered it into the Select a File option: <br/>
<img src="https://i.imgur.com/5EItIqx.png" height="80%" width="80%" alt="SIEM in Azure Steps"/>
<br />
Selected the .log file as my path: <br/>
<img src="https://i.imgur.com/QWtsWU2.png" height="80%" width="80%" alt="SIEM in Azure Steps"/>
<br />
Created the custom log: <br/>
<img src="https://i.imgur.com/pT6kFuh.png" height="80%" width="80%" alt="SIEM in Azure Steps"/>
<br />
Navigated to the Logs tab in Log Analytics Workspace:  <br/>
<img src="https://i.imgur.com/zjXOL4O.png" height="80%" width="80%" alt="SIEM in Azure Steps"/>
<br />
Run the log:  <br/>
<img src="https://i.imgur.com/BtJfyOH.png" height="80%" width="80%" alt="SIEM in Azure Steps"/>
<br />
Extract the data from the top entry:  <br/>
<img src="https://i.imgur.com/6P9TnwB.png" height="80%" width="80%" alt="SIEM in Azure Steps"/>
<br />
Set a field value for each category of the collected data, starting with latitude:  <br/>
<img src="https://i.imgur.com/mVazKaI.png" height="80%" width="80%" alt="SIEM in Azure Steps"/>
<br />
Checked over the entries data to make sure the field value was consistent:  <br/>
<img src="https://i.imgur.com/sLKrodU.png" height="80%" width="80%" alt="SIEM in Azure Steps"/>
<br />
Repeated the previous steps with longitude, this time there were consistency issues in the field value. I corrected them to work as intended:  <br/>
<img src="https://i.imgur.com/cdzR0xL.png" height="80%" width="80%" alt="SIEM in Azure Steps"/>
<br />
This is where I had to correct the mistake by the field value. The purpose of this step is to get accurate data, and to train the field value to be accurate as new entries come into our honeypot: <br/>
<img src="https://i.imgur.com/EXihaVM.png" height="80%" width="80%" alt="SIEM in Azure Steps"/>
<br />
Modified the value and corrected the mistake:  <br/>
<img src="https://i.imgur.com/gJQeQZX.png" height="80%" width="80%" alt="SIEM in Azure Steps"/>
<br />
Followed the same steps with destinationhost:  <br/>
<img src="https://i.imgur.com/aeHtVlA.png" height="80%" width="80%" alt="SIEM in Azure Steps"/>
<br />
Repeated the steps with username: <br/>
<img src="https://i.imgur.com/fgm0cJs.png" height="80%" width="80%" alt="SIEM in Azure Steps"/>
<br />
Repeated the steps with sourcehost:  <br/>
<img src="https://i.imgur.com/DT05OwZ.png" height="80%" width="80%" alt="SIEM in Azure Steps"/>
<br />
Repeated with state: <br/>
<img src="https://i.imgur.com/VEvShNS.png" height="80%" width="80%" alt="SIEM in Azure Steps"/>
<br />
Repeated with country:  <br/>
<img src="https://i.imgur.com/bl4tHSj.png" height="80%" width="80%" alt="SIEM in Azure Steps"/>
<br />
Repeated with label: <br/>
<img src="https://i.imgur.com/3BgbApm.png" height="80%" width="80%" alt="SIEM in Azure Steps"/>
<br />
Repeated with timestamp. Once I was finished, I went back and repeated these steps as more entries came in to strenghten our data collection accuracy: <br/>
<img src="https://i.imgur.com/yUdqH7O.png" height="80%" width="80%" alt="SIEM in Azure Steps"/>
<br />
Navigated to Sentinel:  <br/>
<img src="https://i.imgur.com/8jjoqi7.png" height="80%" width="80%" alt="SIEM in Azure Steps"/>
<br />
Created new workbook:  <br/>
<img src="https://i.imgur.com/WwbkGlD.png" height="80%" width="80%" alt="SIEM in Azure Steps"/>
<br />
Typed the following code into the workbook:  <br/>
<img src="https://i.imgur.com/0Bk5v6T.png" height="80%" width="80%" alt="SIEM in Azure Steps"/>
<br />
Ran query and opened Map Settings. I used the settings shown for this map:  <br/>
<img src="https://i.imgur.com/yYr1dIr.png" height="80%" width="80%" alt="SIEM in Azure Steps"/>
<br />
Saved the Map Settings:  <br/>
<img src="https://i.imgur.com/ZjHOKto.png" height="80%" width="80%" alt="SIEM in Azure Steps"/>
<br />
Went back to the VM and made sure our Log Exporter code was running in PowerShell:  <br/>
<img src="https://i.imgur.com/NNgdP8j.png" height="80%" width="80%" alt="SIEM in Azure Steps"/>
<br />
At this point, I waited for 24 hours to see the results of the project. Here is where it started:  <br/>
<img src="https://i.imgur.com/cUdi38E.png" height="80%" width="80%" alt="SIEM in Azure Steps"/>
<br />
Here's where it was 24 hours later. This project brought in over 1,000 attempted log ins from around the world. You can see on the map where the attacks are coming from by country:  <br/>
<img src="https://i.imgur.com/dnsmnbq.png" height="80%" width="80%" alt="SIEM in Azure Steps"/>
<br />

</p>

<!--
 ```diff
- text in red
+ text in green
! text in orange
# text in gray
@@ text in purple (and bold)@@
```
--!>
