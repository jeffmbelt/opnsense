# opnsense

OpnSense Custom Auto Block bad acting IP Addresses as detected in the /var/log/filter.log file.

1) Copy actions_autoblock.conf to /usr/local/opnsense/service/conf/actions.d/
2) Copy rc.autoupdate /to /usr/local/etc/
3) Create an Alias called AutoBlockedIPs.

Firewall -> Aliases

| Field       | Value                              |
|-------------|------------------------------------|
| Enabled     | checked                            |
| Name        | AutoBlockedIPs                     |
| Type        | URL (IPs)                          |
| Content     | https://127.0.0.1/block-ips.txt    |
| Statistics  | unchecked                          |
| Description | Auto Block Bad Acting IP Addresses |

4) Add outgoing Firewall Rule to WAN

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
| Source:                   | AutoBlockedIPs                    |
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

5) Add incoming Firewall Rule to WAN

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
| Destination:              | AutoBlockedIPs                    |
| Destination port range:   | any to any                        |
| Log:                      | checked                           |
| Category:                 | Blocked                           |
| Description: DROP:        | Blocked Bad Acting IPs (In)       |
| Source OS:                | any                               |
| No XMLRPC Sync:           | unchecked                         |
| Schedule:                 | none                              |
| Gateway:                  | default                           |

Run the following to refresh the Available CRON job entries list.

``` bash
service configd restart
```
