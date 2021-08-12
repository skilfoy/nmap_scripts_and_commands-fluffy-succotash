# Port Scanning Techniques

## nmap -sP <ip>
### Ping Scan
- no packets sent
- reverse-DNS resolution

##nmap -sS
###TCP SYN scan
- does not complete connections with network
  - helps avoid detection
- send SYN packet, awaits response
  - *acknowledgement* => open port
  - *no response* => filtered port
  - *RST/reset* => non-listening port

## nmap -sT
### TCP connect scan
- alternative when SYN scan is not an option
- sends connect system call to connect with the network
- uses a call to push information for every connection attempt
- slower scan, takes longer than SYN scan

## nmap -sN
### TCP NULL
- takes advantage of TCP RFC loophole
  - scan without SYN, RST, or ACK bits triggers a response:
    - no response => *open port*
    - RST packet response => *closed port*
- navigate through firewalls and network/router filters
- somewhat good for stealth, but still identified by IDS

## nmap -sY
### SCTP INIT scan
- covers SIGTRAN and SS7 services
- provides combination of UDP and TCP protocols
- like SYN scan - very fast
- does not complete SCTP processes - good for privacy
- sends INIT Chunk to target, await response
  - INIT-ACK chunk => *open port*
  - ABORT chunk => *non-listening port*
  - multiple transmissions sent with **no response** => *filtered*

## nmap -sU
### UDP scan
- used for scanning UDP devices
  - DNS, DHCP, SNMP - highly targeted by attackers - important to scan
- can run concurrently with SYN scan
- send UDP packet to every targeted port
  - except for ports 53 and 161, empty packet is sent
  - *no response* => port open

#Host Scanning

## nmap -sL <ip>
### Identify Hostnames
- executes DNS query
- returns hostnames wihtout sending packet to host

## nmap -O <ip>
### OS Scanning
- sends UDP and TCP packets to analyze response
  - checks against internal database of operating systems
    - if match is found, nmap gives OS, version, provider's name

## nmap -sV <ip>
### Version Detection





