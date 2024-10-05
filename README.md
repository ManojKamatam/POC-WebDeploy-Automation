# POC-WebDeploy-Automation
# Need to have these prerequisites: 
1) New-NetFirewallRule -DisplayName "Allow WinRM HTTP" -Direction Inbound -Protocol TCP -LocalPort 5985 -Action Allow
2) winrm enumerate winrm/config/listener

   winrm create winrm/config/Listener?Address=*+Transport=HTTP

3) netstat -an | findstr 5985
4) Test-NetConnection -ComputerName 52.44.236.121 -Port 5985

5) winrm quickconfig



