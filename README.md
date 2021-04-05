# opnsense

OpnSense Custom Auto Block bad acting IP Addresses as detected in the /var/log/filter.log file.

1) Copy actions_autoblock.conf to /usr/local/opnsense/service/conf/actions.d/
2) Copy actions_autoallow.conf to /usr/local/opnsense/service/conf/actions.d/
3) Copy rc.autoblock /to /usr/local/etc/
4) Copy rc.autoallow /to /usr/local/etc/
5) Create an Alias called BlockedAuto

Firewall -> Aliases

| Field       | Value                              |
|-------------|------------------------------------|
| Enabled     | checked                            |
| Name        | BlockedAuto                        |
| Type        | URL (IPs)                          |
| Content     | https://127.0.0.1/blocked.txt      |
| Statistics  | unchecked                          |
| Description | Auto Block Bad Acting IP Addresses |

6) Create an Alias called AllowedAuto

Firewall -> Aliases

| Field       | Value                              |
|-------------|------------------------------------|
| Enabled     | checked                            |
| Name        | AllowedAuto                        |
| Type        | URL (IPs)                          |
| Content     | https://127.0.0.1/allowed.txt      |
| Statistics  | unchecked                          |
| Description | Auto Allow Addresses for Services  |

7) Add outgoing Firewall Rule to WAN

Firewall -> Rules -> WAN

| Field                     | Value                             |
|---------------------------|-----------------------------------|
| Action:                   | Block                             |
| Disabled:                 | unchecked                         |
| Quick:                    | checked                           |
| Interface:                | WAN                               |
| Direction:                | out                               |
| TCP/IP Version:           | IPv4                              |
| Protocol:                 | any                               |
| Source / Invert:          | unchecked                         |
| Source:                   | BlockedAuto                       |
| Destination / Invert:     | unchecked                         |
| Destination:              | any                               |
| Destination port range:   | any to any                        |
| Log:                      | checked                           |
| Category:                 | Blocked                           |
| Description: DROP:        | Blocked Bad Acting IPs (In)       |
| Source OS:                | any                               |
| No XMLRPC Sync:           | unchecked                         |
| Schedule:                 | none                              |
| Gateway:                  | default                           |

8) Add incoming Firewall Rule to WAN

Firewall -> Rules -> WAN

| Field                     | Value                             |
|---------------------------|-----------------------------------|
| Action:                   | Block                             |
| Disabled:                 | unchecked                         |
| Quick:                    | checked                           |
| Interface:                | WAN                               |
| Direction:                | out                               |
| TCP/IP Version:           | IPv4                              |
| Protocol:                 | any                               |
| Source / Invert:          | unchecked                         |
| Source:                   | any                               |
| Destination / Invert:     | unchecked                         |
| Destination:              | BlockedAuto                       |
| Destination port range:   | any to any                        |
| Log:                      | checked                           |
| Category:                 | Blocked                           |
| Description: DROP:        | Blocked Bad Acting IPs (In)       |
| Source OS:                | any                               |
| No XMLRPC Sync:           | unchecked                         |
| Schedule:                 | none                              |
| Gateway:                  | default                           |

9) Add outgoing Firewall Rule to WAN

Firewall -> Rules -> WAN

| Field                     | Value                             |
|---------------------------|-----------------------------------|
| Action:                   | PASS                              |
| Disabled:                 | unchecked                         |
| Quick:                    | checked                           |
| Interface:                | WAN                               |
| Direction:                | out                               |
| TCP/IP Version:           | IPv4                              |
| Protocol:                 | any                               |
| Source / Invert:          | unchecked                         |
| Source:                   | AllowedAuto                       |
| Destination / Invert:     | unchecked                         |
| Destination:              | any                               |
| Destination port range:   | 80 to 80                          |
| Log:                      | checked                           |
| Category:                 | ALLOWED                           |
| Description: DROP:        | ALLOW Service IPs (out)           |
| Source OS:                | any                               |
| No XMLRPC Sync:           | unchecked                         |
| Schedule:                 | none                              |
| Gateway:                  | default                           |

10) Add outgoing Firewall Rule to WAN

Firewall -> Rules -> WAN

| Field                     | Value                             |
|---------------------------|-----------------------------------|
| Action:                   | PASS                              |
| Disabled:                 | unchecked                         |
| Quick:                    | checked                           |
| Interface:                | WAN                               |
| Direction:                | out                               |
| TCP/IP Version:           | IPv4                              |
| Protocol:                 | any                               |
| Source / Invert:          | unchecked                         |
| Source:                   | AllowedAuto                       |
| Destination / Invert:     | unchecked                         |
| Destination:              | any                               |
| Destination port range:   | 443 to 443                        |
| Log:                      | checked                           |
| Category:                 | ALLOWED                           |
| Description: DROP:        | ALLOW Service IPs (out)           |
| Source OS:                | any                               |
| No XMLRPC Sync:           | unchecked                         |
| Schedule:                 | none                              |
| Gateway:                  | default                           |

11) Run the following to refresh the Available CRON job entries list.

``` bash
service configd restart
```

12) Add CRON entries for Block and Allow lists

System -> Settings -> CRON

  Update Allowed Destination Alias
  
 12) Add CRON entries for Block and Allow lists

System -> Settings -> CRON

  Update Auto Blocked Alias
