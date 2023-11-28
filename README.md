# Minitoring Photon OS
<img width="120" alt="Photon OS" src="https://github.com/rafaelurrutiasilva/images/blob/main/logos/Photon_OS.png" align=left> <br>
A general introduction on how to handle logging and monitoring on VMware [Photon OS](https://vmware.github.io/photon). <br>
<br>
<br>
## Introduction
VMware has an extensive ecosystem of products for maintaining control over their applications. This includes monitoring, logging, and more. However, if you prefer or need alternative methods, you have come to the right page.
<br>
<br>
---

## Logging
You will need to install a system for log processing. My recommmendation is go for `rsyslog`.
* The installation is done by:
```
tdnf install rsyslog
```
* The you need to configure the destination syslog server, replace the line: `*.* @@remote-host:514` with `*.* @@syslog.of.your:514`.
Where **syslog.of.your** is the namn or IP address of your syslog server.

* restart and enable rsyslog
```
systemctl restart rsyslog.service
systemctl enable rsyslog.service 
````
* Sending specific log
You can configure rsyslog to handle specific files to be sent to the syslog server. This is done in the configuration file: `/etc/rsyslog.d/application.conf`.<br>
See the documentation for more details.



## Monitoring Nagios checks
In my repository, [Nagios Bash Plugins](https://github.com/rafaelurrutiasilva/nagios-bash-plugins). I have four small Bash scripts that will likely provide all the help you may need. These scripts check tasks, CPU, memory, or swap using the top command. The disk utilization, file age with a few attributes, and, of course, Linux processes. <br>
All the scripts can be installed locally and then executed using SSH from the authorized monitoring server. **Be aware of security**!

## Security in focus
* Use a local account with just enough privileges; consider using sudo, for example, to limit access specifically for these file checks.
* Utilize SSH keys for authentication.
* Restrict login access to only the necessary IP addresses.
