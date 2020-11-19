*Powershell Launch Wait Check*
=============


Powershell-based script utility for $Universe status check.
http://github.com/Automic-Community/Powershell-Launch-Wait-Check

<!-- List of attached files -->
Contents of Solution Package:

						
								*PowerShell_Status_Check.zip
								
								*81-image1.png
								
						


Documenation and Instructions
---

<p><span class="bbc_underline"><span>ORSYP $Universe Launch Wait Check</span></span><br /><br />The ORSYP $Universe status check script is a Powershell-based utility that uses the built-in UXSHW tool in the ORSYP toolkit to check for Launch Wait jobs and compare their timing to the current time. Using Jenkins to run it every six hours, if any job is one hour or more beyond the Launch Window, it will email an alert to the appropriate people.<br /><br />This can be adapted to use any scheduling tool, including Windows Scheduler, but will require a little more work on your end, as Jenkins has e-mail capabilities built-in and Windows Scheduler requires extra scripts to be able to do that.</p>
<p><strong class="title">Target environments:</strong> Windows Server 2008, Windows Server 2012</p>
<p><strong class="title">Prerequisites:</strong> Windows Powershell 2.0</p>
<p><strong class="title">Implementation:</strong> Tweak the scripts to point to the correct locations; in orsyp_launch_wait_check.bat, change the CALL to the uxsetenv.bat to point to the correct folder. Then, change to the correct env name in getList.ps1 - at the top, change SIM to EXP or another appropriate environment name.<br /> <br /> Then configure a scheduler of some kind (I highly recommend against setting it up in ORSYP $Universe Scheduler as if something is wacky with the scheduler, the check may not kick off) to launch the script on the scheduler server. From Jenkins, I configured Execute Windows Batch Command to use the following script:<br /> <br /> powershell invoke-command -ComputerName &lt;SERVERNAME&gt; -ScriptBlock {c:\scripts\orsyp_launch_wait_check.bat}<br /> <br /> Make sure you have Powershell remoting enabled on the ORSYP $Universe Scheduler server.</p>
<p><br />1. What's Included<br />Included is a bat file (orsyp_launch_wait_check.bat) and a Powershell script (getList.ps1).<br /><br />The bat file loads the environment variables and then kicks off the Powershell script.<br /><br />The Powershell script launches UXSHW and fails if there are any jobs whatsoever in Launch Wait an hour or more past their launch window.<br /><br />2.Usage<br />Tweak the scripts to point to the correct locations; in orsyp_launch_wait_check.bat, change the CALL to the uxsetenv.bat to point to the correct folder. Then, change to the correct env name in getList.ps1 - at the top, change SIM to EXP or another appropriate environment name.<br /><br />Then configure a scheduler of some kind (I highly recommend against setting it up in ORSYP $Universe Scheduler as if something is wacky with the scheduler, the check may not kick off) to launch the script on the scheduler server. From Jenkins, I configured Execute Windows Batch Command to use the following script:<br /><br />powershell invoke-command -ComputerName &lt;SERVERNAME&gt; -ScriptBlock {c:\scripts\orsyp_launch_wait_check.bat}<br /><br />Make sure you have Powershell remoting enabled on the ORSYP $Universe Scheduler server.<br /><br />The job will fail with an errorlevel of 1 if there are jobs stuck past their launch wait window.<br /><br />3. Licensing<br />This is completely free &amp; open source, meaning you're absolutely free to use it, dismantle it, adapt it and change it as you see fit. It uses ORSYP's built-in tools, so licensing for ORSYP is necessitated, but for this script you don't need anything special.</p>

Copyright and License
---

Broadcom does not support, maintain or warrant Solutions, Templates, Actions and any other content published on the Community and is subject to Broadcom Community [Terms and Conditions](https://community.broadcom.com/termsandconditions)


Questions or Need Help? 
---
Join the [Automic Community Integrations](https://community.broadcom.com/communities/community-home?CommunityKey=83e49dd4-b93e-464a-a343-2bb1e51c13ec) to discuss this integration.
