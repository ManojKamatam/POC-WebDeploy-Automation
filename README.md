# POC-WebDeploy-Automation
# Need to have these prerequisites: 
1) New-NetFirewallRule -DisplayName "Allow WinRM HTTP" -Direction Inbound -Protocol TCP -LocalPort 5985 -Action Allow   ******************   6
2) winrm enumerate winrm/config/listener

   winrm create winrm/config/Listener?Address=*+Transport=HTTP

3) netstat -an | findstr 5985
4) Test-NetConnection -ComputerName <public-ip> -Port 5985

# Test these if unreachable

5) winrm quickconfig   *************** 3
6) winrm set winrm/config/service '@{AllowUnencrypted="true"}' *********** 4
7) winrm enumerate winrm/config/listener *************** 5
9) winrm create winrm/config/listener?Address=*+Transport=HTTP ***
10) Restart-Service winrm  ********** 8
11) Test-WsMan -ComputerName 34.198.209.155 -Authentication Basic -Credential (Get-Credential) *************** 9
12) 
13) winrm set winrm/config/service/auth '@{Basic="true"}' **************** 7


14) # Check if WinRM service is running
Get-Service WinRM

# Check the WinRM listener
winrm enumerate winrm/config/listener

# Ensure the service is configured to allow basic auth
winrm get winrm/config/service/auth    ********************** 1

winrm set winrm/config/service/auth @{Basic="true"}
Enable-PSRemoting -Force

# Then try enabling Basic auth again:
Set-Item WSMan:\localhost\Service\Auth\Basic $true  ******************** 2




