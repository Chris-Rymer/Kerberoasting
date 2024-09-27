<h1>Detecting Kerberoasting</h1>

<h2>Scenario</h2>
"Alonzo Spotted Weird files on his computer and informed the newly assembled SOC Team ASAP. Assessing the situation it is believed Kerberoasting attack may have occurred in the network. It is your Job to confirm the findings by analyzing the provided evidence. You are given: Security Logs from the Domain Controller, PowerShell-Operational Logs from the affected workstation and Prefetch Files from affected workstation." <br />


<h2>Languages and Utilities Used</h2>

- <b>PECmd (Eric Zimmerman)</b>
- <b>Timeline Explorer (Eric Zimmerman)</b>
- <b>Event Viewer</b>
- <b>Splunk</b> 

<h2>Environments Used </h2>

- <b>Windows 11</b>

<h2>Analysis:</h2>

<p align="center">
Parse the Prefetch files with PECmd to make it analysis ready: <br/>
<img src="https://i.imgur.com/oon3EP0.png" height="80%" width="80%" alt="Editme"/>
<br />
<br />
Analyzed event logs, found MSSQLService targeted at 11:18:09 PM on 5/20/2024 from a workstation with the IP of 172.17.79.129:  <br/>
<img src="https://i.imgur.com/oU8lv3W.png" height="80%" width="80%" alt="Editme"/>
<br />
<br />
Analyzed event log in Splunk and found a Kerberos service ticket was requested with MSSQLService:  <br/>
<img src="https://i.imgur.com/Vu6SHBm.png" height="80%" width="80%" alt="Editme"/>
<br />
<br />
Analyzed PowerShell logs and found restriction bypass command used:  <br/>
<img src="https://i.imgur.com/937FtHO.png" height="80%" width="80%" alt="Editme"/>
<br />
<br />
PowerShell logs show after bypass command was ran, a file named "PowerView.ps1" was executed. This file is part of the PowerSploit framework and is used to enumerate Active Directory for privileged accounts and other network information:  <br/>
<img src="https://i.imgur.com/rra9UdG.png" height="80%" width="80%" alt="Editme"/>
<br />
<br />
Edit:  <br/>
<img src="https://i.imgur.com/3HdIkyo.png" height="80%" width="80%" alt="Editme"/>
<br />
<br />
Edit:  <br/>
<img src="https://i.imgur.com/Y9C7Ykf.png" height="80%" width="80%" alt="Editme"/>
</p>
<h2>Conclusion</h2>
Edit <br />
