# Minitoring Photon OS
<img width="120" alt="Photon OS" src="https://github.com/rafaelurrutiasilva/images/blob/main/logos/Photon_OS.png" align=left> <br>
A general introduction on how to handle logging and monitoring on VMware [Photon OS](https://vmware.github.io/photon). <br>
<br>
<br>
## Introduction
VMware has an extensive ecosystem of products for maintaining control over their applications. This includes monitoring, logging, and more. However, if you prefer or need alternative methods, you have come to the right page.

---

## Logging
You will need to install a system for log processing. My recommmendation is go for `rsyslog`.
* The installation is done by:
```
tdnf install rsyslog
```
* The you need to configure the destination syslog server, replace the line: `*.* @@remote-host:514` with `*.* @@syslog.of.your:514`
* restart and enable rsyslog
```
systemctl restart rsyslog.service
systemctl enable rsyslog.service 
````

## Monitoring Nagios checks

https://github.com/rafaelurrutiasilva/nagios-bash-plugins

