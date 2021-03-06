EL Cheatsheets and checklists
=============================

_Nico Hunink (3 TIN HoGent)_ 

### Samba_cheatsheet

### Tools
* `yum install setroubleshoot`, gevolgd door: `service auditd restart`
* `yum install xorg-x11-xauth policycoreutils-gui bitmap-fixed-fonts`
* `yum install net-tools`
* `repoquery -qf */netstat */lsof */nmap`
      * Wanneer niet geïnstalleerd: `yum install yum-utils`
* IP-conflicten opsporen: `sudo yum install arp-scan`
<br> en 
    `arp-scan -I eth0 -l`
* _yum install nmap_


###SELinux ###

| Actie                                  | Command                                    |
| :---                                    | :---                                       |
| Status controleren                | `sestatus` |
| Starten setroubleshoot (daemon)| `setroubleshootd` |
| Herstellen initiële SELinux-settings| `restorecon -R -v [target-folder]`(bijv. /var/www) |
| In de logs controleren op output van setroubleshoot | `grep setroubleshoot /var/log/messages` |
| Config files SELinux | `/etc/selinux/config `                         |
| Labeling controleren (optie -Z) | `ls -lZ [/usr/sbin/httpd]`                       |
| Change context | `chcon` |
| Ingestelde booleans opvragen | `getsebool -a` (en evt. `| grep samba/smbd/nmbd`) |
| Een boolean instellen| `setsebool [boolean] [0|1]` (-P toevoegen om permanent te maken) |
| (na install setroubleshoot) | `sealert -l [de opgegeven code]` |
| Grafische tool| `system-config-selinux` |
| SELinux-Alerts vinden in de logs | `sealert -a /var/log/audit/audit.log | less` |

* `ls -Z`
* `netstat -Z`

###Testen ###

Wanneer een script niet runt in combinatie met een Windows-host (door einde-markeringen, eigen aan Microsoft):

`yum install dos2unix -f`.

Run vervolgens `dos2unix [script]`.

### Firewall en DNS ###
* `lsof -i -n -P | grep` ... ( list open files, geeft lijst geopende bestanden en door welke processen deze gebruikt worden, weer)
* Firewall: /etc/sysconfig/iptables
    * systemctl restart iptables.service
* DNS: /etc/resolv.conf

### Services controleren ###

* SAMBA: 
    * systemctl status smb.service (daemon)
    * systemctl status nmb.service (daemon)
* FTP: 
    * systemctl status vsftpd.service
*  `journalctl  -r -o verbose -u smb.service`
*  `journalctl  -r -o verbose -u nmb.service`
* `ps | grep` [naam_service]
* `tail -f less /var/logs/messages`
      * (en verdere logs in de directory logs)
      * zoek dan naar DHCP op deze manier: /DHCP
