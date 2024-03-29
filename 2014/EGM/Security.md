------------
<h3 align="center">
2014 EGM: Security (30 Marks)                                                                                                                                                
</h3>
<p align="center">
<a href="http://www.redbrick.dcu.ie/help/exams/admin-2014-egm">Redbrick</a>
</p>
------------ 
1. **What is AppArmor?** (2 marks)<br>
AppArmor is a Mandatory Access Control (MAC) system which is a kernel Linux Security Module (LSM) enhancement to confine programs to a limited set of resources. 
AppArmor's security model is to bind access control attributes to programs rather than to users. 
AppArmor proactively protects the operating system and applications from external or internal threats, even zero-day attacks, by enforcing good behavior and preventing even unknown application flaws from being exploited. 
AppArmor security policies completely define what system resources individual applications can access, and with what privileges.<br>
2. **What are: pf, fail2ban, iptables** (3 marks)<br>
  * _pf_: Packet Filter is a BSD licensed stateful packet filter, a central piece of software for firewalling. It is comparable to netfilter (iptables), ipfw and ipfilter.  
  * _fail2ban_: An intrusion prevention software framework which protects computer servers from brute-force attacks. 
It is able to run on POSIX systems that have an interface to a packet-control system or firewall installed locally, for example, iptables.  
  * _iptables_: A command-line firewall utility that uses policy chains to allow or block traffic. 
When a connection tries to establish itself on your system, iptables looks for a rule in its list to match it to. 
If it doesn’t find one, it resorts to the default action.  
3. **What does VPN stand for? Why would one be used?** (3 marks)<br>
VPN stands for _Virtual Private Network_. A VPN extends a private network across a public network. 
It enables a computer or network-enabled device to send and receive data across shared or public networks as if it were directly connected to the private network, while benefiting from the functionality, security and management policies of the private network. <br>
4. **What are SSH keys? What command would you use to configure one?** (3 marks)<br>
SSH keys serve as a means of identifying yourself to an SSH server using public-key cryptography and challenge-response authentication. 
One immediate advantage this method has over traditional password authentication is that you can be authenticated by the server without ever having to send your password over the network. 
Anyone eavesdropping on your connection will not be able to intercept and crack your password because it is never actually transmitted. 
Additionally, using SSH keys for authentication virtually eliminates the risk posed by brute-force password attacks by drastically reducing the chances of the attacker correctly guessing the proper credentials. <br>
`ssh-keygen` is the command used to configure one. <br>
5. **You suspect maK has a rootkit on one of the machines. What command could you run to check for the rootkit?** (3 marks)<br>
*Redbrick Specific*  
6. **You have just installed a new linux server. Name 3 things you should do to secure this system.** (3 marks)<br>
  * Configure iptables and other security software such as fail2ban  
  * Add the line `PermitRootLogin no` to `/etc/ssh/sshd_config` to disable login as root over SSH. 
  * Enable automatic security updates. To do this on an Ubuntu server:  
  `sudo apt-get install unattended-upgrades` this will install the unattended-upgrades package.  
  `sudo dpkg-reconfigure -plow unattended-upgrades` this will enable and configure the default configs.  
7. **Why is ssh as root disabled on our machines?** (2 marks)<br>
If ssh as root is permitted on a machine then a brute force attacker can try brute force `ssh root@$IP`. If they succeed then they have root access and complete control of the machine. If ssh as root is not permitted then they must first find a privilidged user with sudoer rights to ssh as.  
Also sudo reduces accidents by restricting commands to a reduced "remotely available" set.  
8. **Name 3 files that should only be readable by root and what they do.** (4 marks)<br>
`/etc/shadow` and `/etc/gshadow` - contain encrypted user passwords and group account information.  
`/etc/passwd` - contains user information required at login.  
`/etc/sudoers` - controls who can run certain commands and whether you need a password for particular command  
9. **Why would you set the sticky bit on a file?** (3 marks)<br>
A sticky bit is a permission bit that is set on a directory that allows only the owner of the file within that directory or the root user to delete or rename the file. No other user has the needed privileges to delete the file created by some other user.  
The sticky bit is useful on directories that are world-writable, such as /tmp. In these directories, anyone can create a file, so the directory needs to be world-writable. But that would mean anyone could delete a file, too, even if it didn't belong to them, since deleting a file is controlled by the write permission on the directory. When a directory has the sticky bit, only the owner of a file has the permission to delete it.  
`chmod +t /path/to/directory/` adds the sticky bit permission to a directory
10. **You left a root terminal unlocked and someone has used it to do something. The history files has been deleted. How do you go about finding out what they did?** (4 marks)<br>
The first thing to do is read the .bash_history file and see what it contains: `cat ~/.bash_history`  
If this file is empty try logging out and back in. If the user did `history -c` or `cat /dev/null > ~/.bash_history` then .bash_history will show the commands. (the history entries have a copy in the memory and it will flush back to the file when you log out.) If the user deleted the history with `history -c && history -w` or `cat /dev/null > ~/.bash_history && history -c && exit` then the history is lost. 
