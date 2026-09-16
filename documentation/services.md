# Network Services

## DHCP

SERVER1 provides centralized DHCP services.

**Server:**

```text
192.168.20.10

## DNS

SERVER2 provides DNS services. 

**Servers:**

```text
192.168.20.11

| Hostname | IP Adress |
|----------|-----------|
| server1.lab.local | 192.168.20.10 |
| server2.lab.local | 192.168.20.11 |
| server3.lab.local | 192.168.20.12 |
| dhcp.lab.local | 192.168.20.10 |
| dns.lab.local | 192.168.20.11 |
| files.lab.local | 192.168.20.12 |

## FTP/TFT

SERVER3 provides FTP and TFTP services. 

**Servers:**

```text
192.168.20.12

## Syslog

The Security VLAN contains the centralized Syslong server

**Servers:**

```text
192.168.30.10

