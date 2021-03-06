systemd Service Monitoring template for Zabbix
===========================================


FEATURES
--------
* Discovery of systemd Services
* Provides alerting when a service stops or restarts

REQUIREMENTS
------------
* RHEL/CentOS/Oracle EL
* Ubuntu 16.04
* Zabbix 3.4

INSTALLATION
------------
* Server
  * Import template __Template_App_systemd_Services.xml__ file
  * Link template to host
* Agent
  * Place the following files inside /etc/zabbix/:
  * service_discovery_blacklist
  * Place the following file inside /usr/local/bin/:
  * service_restart_check.sh
  * Copy __userparameter_systemd_services.conf__ to __/etc/zabbix/zabbix\_agentd.d/userparameter\_systemd\_services.conf__
  * Restart zabbix_agent

NOTES
------------

This assumes you have disabled all unnecessary services prior to enabling the template. Any service that is enabled and not running will result in an alert.

If you cannot, use the service_discovery_blacklist to add services that you don’t want to monitor.

Additionally this excludes getty and autovt which are not reported by systemctl with the tty and will result in an error.

Testing
-------
To test that everything works use `zabbix_agentd -t` to query the statistics :

```bash
# Discover systemd services
zabbix_agentd -t "systemd.service.discovery"
zabbix_agentd -t "systemd.service.status[sshd]"
zabbix_agentd -t "systemd.service.PID[sshd]"
zabbix_agentd -t "systemd.uptime"
```
