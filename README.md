# opnsense
OpnSense Custom Auto Block bad acting IP Addresses

Create an Alias called AutoBlockedIPs.

Firewall -> Aliases -> 

Add outgoing Firewall Rule to WAN

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
|---------------------------|-----------------------------------|

Add incoming Firewall Rule to WAN

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
|---------------------------|-----------------------------------|

