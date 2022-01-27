# Introduction
This project describes a way to enable CyberArk PSMP to connect transparently to a PowerShell terminal

# Requirements
- Port 22 Open
- OpenSSH Server feature
  Launch Windows Settings -> Apps -> Optional Features -> Add a Feature ->  Open SSH Server -> Install
  Run:  *Start-Service sshd*
        *Set-Service -Name sshd -StartupType 'Automatic'*

At this point, any incoming SSH connection will default to cmd.exe.
Execute the following command to replace it to powershell.exe:
  *New-ItemProperty -Path "HKLM:\SOFTWARE\OpenSSH" -Name DefaultShell -Value "C:\Windows\System32\WindowsPowerShell\v1.0\powershell.exe" -PropertyType String -Force*

# Configuration
You may add a Windows Local Account to your PVWA but categorize it as an Unix Account, so PSMP can be used via SSH
(I'm currently investigating password rotation via Linked Accounts. If you havee any insights, please submit a Pull Request)

# Transparent Connection
Open Putty or your terminal and type: *ssh YourADLoginUser@WindowsLocalAccount@PowershellServer@PSMPServer*
PSMP will prompt for you AD User's Password and then proceed with the login
