# POC-WebDeploy-Automation
# Need to have these prerequisites: 
1) New-NetFirewallRule -DisplayName "Allow WinRM HTTP" -Direction Inbound -Protocol TCP -LocalPort 5985 -Action Allow
2) winrm enumerate winrm/config/listener

   winrm create winrm/config/Listener?Address=*+Transport=HTTP

3) netstat -an | findstr 5985
4) Test-NetConnection -ComputerName 52.44.236.121 -Port 5985

5) winrm quickconfig

6) # Check if WinRM service is running
Get-Service WinRM

# Check the WinRM listener
winrm enumerate winrm/config/listener

# Ensure the service is configured to allow basic auth
winrm get winrm/config/service/auth

winrm set winrm/config/service/auth @{Basic="true"}
Enable-PSRemoting -Force

# Then try enabling Basic auth again:
Set-Item WSMan:\localhost\Service\Auth\Basic $true




