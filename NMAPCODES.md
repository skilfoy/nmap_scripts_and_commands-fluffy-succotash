# Table of Contents
- [Port Scanning Techniques](#port-scanning-techniques)
  - [Ping Scan](#ping-scan)
  - [TCP SYN scan](#tcp-syn-scan)
  - [TCP connect scan](#tcp-connect-scan)
  - [TCP NULL](#tcp-null)
  - [SCTP INIT scan](#sctp-init-scan)
  - [UDP scan](#udp-scan)
- [Host Scanning](#host-scanning)
  - [Identify Hostnames](#identify-hostnames)
  - [OS Scanning](#os-scanning)
  - [Version Detection](#version-detection)
  - [Verbosity](#verbosity)
- [Brute Forcing Passwords](#brute-forcing-passwords)

# Port Scanning Techniques

## Ping Scan
    nmap -sP
- no packets sent
- reverse-DNS resolution

## TCP SYN scan
    nmap -sS
- does not complete connections with network
  - helps avoid detection
- send SYN packet, awaits response
  - *acknowledgement* => open port
  - *no response* => filtered port
  - *RST/reset* => non-listening port

## TCP connect scan
    nmap -sT
- alternative when SYN scan is not an option
- sends connect system call to connect with the network
- uses a call to push information for every connection attempt
- slower scan, takes longer than SYN scan

## TCP NULL
    nmap -sN
- takes advantage of TCP RFC loophole
  - scan without SYN, RST, or ACK bits triggers a response:
    - no response => *open port*
    - RST packet response => *closed port*
- navigate through firewalls and network/router filters
- somewhat good for stealth, but still identified by IDS

## SCTP INIT scan
    nmap -sY
- covers SIGTRAN and SS7 services
- provides combination of UDP and TCP protocols
- like SYN scan - very fast
- does not complete SCTP processes - good for privacy
- sends INIT Chunk to target, await response
  - INIT-ACK chunk => *open port*
  - ABORT chunk => *non-listening port*
  - multiple transmissions sent with **no response** => *filtered*

## UDP scan
    nmap -sU
- used for scanning UDP devices
  - DNS, DHCP, SNMP - highly targeted by attackers - important to scan
- can run concurrently with SYN scan
- send UDP packet to every targeted port
  - except for ports 53 and 161, empty packet is sent
  - *no response* => port open

# Host Scanning

## Identify Hostnames
    nmap -sL
- executes DNS query
- returns hostnames wihtout sending packet to host

## OS Scanning
    nmap -O
- sends UDP and TCP packets to analyze response
  - checks against internal database of operating systems
    - if match is found, nmap gives OS, version, provider's name

## Version Detection
    nmap -sV
- uses information from open port to tell the version of the software on the computer

## Verbosity
    nmap -v [range from -4 to 4]
- **Level -4** - no output - will not see response packets
- **Level -3** - above + provides error messages showing failures
- **Level -2** - above + warnings and any other error messages
- **Level -1** - above + run-time information such as start time, version, and statistics
- **Level 0** - default - displays sent and received packets and other information
- **Level 1** - above + protocol, flags, and timing
- **Level 2** - more detailed information about sent and received packets
- **Level 3** - complete raw transfer of both sent and received packets
- **Level 4** - above + more information

# Brute Forcing Passwords
#### Brute authentication credentials of a server
    nmap --script brute -Pn <target>
- Other scripts include:
  - http-brute, snmp-brute, oracle-brute, etc.

# DoS Attacks
#### Flood host with several requests to test if it crashes or fails to service other genuine requests:

    nmap --script dos -Pn <target>

#### Launch active DoS attack on target host for indefinite period of time:
   
    nmap --max-parallelism 750 -Pn --script http_slowloris script-args http-slowloris.runforever=true

