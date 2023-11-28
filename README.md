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



## Monitoring using Nagios checks
In my repository, [Nagios Bash Plugins](https://github.com/rafaelurrutiasilva/nagios-bash-plugins). I have four small Bash scripts that will likely provide all the help you may need. These scripts check tasks, CPU, memory, or swap using the top command. The disk utilization, file age with a few attributes, and, of course, Linux processes. <br>
All the scripts can be installed locally and then executed using SSH from the authorized monitoring server. **Be aware of security**!

## Security in focus
* Use a local account with just enough privileges; consider using sudo, for example, to limit access specifically for these file checks.
* Utilize SSH keys for authentication.
* Restrict login access to only the necessary IP addresses.

## Monitoring using SNMP
You will need to install (`tdnf install net-snmp`) and configure (`snmpconf -g basic_setup`) the snmp services on your system. Carefully consider which version to use and why. Your options are essentially v2 or v3.<br>
When all the configuration is done, then you can start to explore the OIDs in the table below:

OID                       |      Used for
--------------------------|---------------------------------------------
1.3.6.1.2.1.1.3.0         |      Timeticks/Uptime (for the snmpd process)
1.3.6.1.2.1.1.5.0         |      hostname
1.3.6.1.4.1.2021.10.1.3.1 |      Load 1  min
1.3.6.1.4.1.2021.10.1.3.2 |      Load 5  min
1.3.6.1.4.1.2021.10.1.3.3 |      Load 15 min
1.3.6.1.4.1.2021.4.5.0    |      Total RAM in machine
1.3.6.1.4.1.2021.4.6.0    |      Total RAM used
1.3.6.1.4.1.2021.4.11.0   |      Total RAM Free
1.3.6.1.4.1.2021.4.3.0    |      Total Swap Size
1.3.6.1.4.1.2021.4.4.0    |      Available Swap Space
1.3.6.1.4.1.2021.9.1.6.1  |      Total size of the disk/partion (kBytes): .
1.3.6.1.4.1.2021.9.1.7.1  |      Available space on the disk
1.3.6.1.4.1.2021.9.1.8.1  |      Used space on the disk
1.3.6.1.4.1.2021.9.1.9.1  |      Percentage of space used on disk
1.3.6.1.2.1.25.4.2.1.2    |      Process list

## Prometheus Node Exporter
If you already are familiar with Prometheus and Grafana with not to run install and run the [Prometheus Node Exporter](https://github.com/prometheus/node_exporter).<br> 
You have a few choices: Configure and run as a container applikation, create you own RPM using the community spec-file, [node_exporter.spec](https://github.com/utobi/prometheus-rpm/blob/master/node_exporter/contrib/node_exporter.spec) or you can install locally using my script [install_prometheus_exporter.sh](https://github.com/rafaelurrutiasilva/Prometheus_on_PhotonOS/blob/main/scripts/install_prometheus_exporter.sh), part of my repo [Prometheus_on_PhotonOS](https://github.com/rafaelurrutiasilva/Prometheus_on_PhotonOS)




