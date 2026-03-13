# Common C2 Ports Used for Malicious Remote Access and Beacons

Malicious actors often use command and control (C2) servers to remotely manage compromised systems, such as through beacons that periodically "phone home" for instructions or to exfiltrate data. These communications frequently leverage common network ports to blend in with legitimate traffic or exploit specific vulnerabilities.

Ports can be categorized into two main types: **standard ports** (used to mimic normal services like web browsing) and **non-standard ports** (often associated with specific malware or tools).

## Standard Ports Often Abused for C2

These are well-known ports for legitimate protocols but frequently hijacked to hide malicious traffic.

| Port       | Protocol       | Common Use in Malware/C2                  | Examples/Notes                                                                 |
|------------|----------------|-------------------------------------------|--------------------------------------------------------------------------------|
| 21         | TCP (FTP)      | File transfer for payloads or exfiltration | Used by trojans like DarkFTP for control channels.                             |
| 22         | TCP (SSH)      | Secure remote access tunneling            | Malware may tunnel C2 over SSH to evade detection.                             |
| 23         | TCP (Telnet)   | Insecure remote access                    | Older malware uses for backdoor access; seen in ICS attacks.                   |
| 25         | TCP (SMTP)     | Email-based exfiltration or callbacks     | Non-standard use in tools like WellMail.                                       |
| 53         | TCP/UDP (DNS)  | DNS tunneling for stealthy beacons        | Common for data exfiltration; hard to detect in normal DNS traffic.            |
| 80         | TCP (HTTP)     | Web-based beacons and callbacks           | Widely used to blend with web traffic; e.g., Stuxnet callbacks.                |
| 443        | TCP (HTTPS)    | Encrypted C2 channels                     | Most common for secure, hidden communications; e.g., in botnets like TrickBot. |
| 6667       | TCP (IRC)      | Botnet control channels                   | Historically used for IRC-based C2 in trojans like Bionet.                     |

## Non-Standard Ports Commonly Associated with Malware

These are often used by specific trojans, RATs (Remote Access Trojans), or tools like Cobalt Strike and Metasploit for beacons and remote access.

| Port          | Protocol | Common Use in Malware/C2         | Examples/Notes                                                  |
|---------------|----------|----------------------------------|-----------------------------------------------------------------|
| 135           | TCP/UDP  | Propagation and control          | Exploited by worms like Blaster.                                |
| 139           | TCP      | Network resource access          | Used for spreading via shared drives.                           |
| 1080          | TCP      | Virus propagation                | Associated with MyDoom.                                         |
| 1214          | TCP      | P2P file sharing backdoors       | Linked to KAZAA trojans.                                        |
| 2140/3150     | TCP      | Deep Throat RAT                  | Backdoor access and control.                                    |
| 2404          | TCP      | Custom C2                        | Observed in recent threat reports.                              |
| 4444          | TCP      | Metasploit default               | Common in penetration testing tools abused maliciously.         |
| 7443/8443/8848| TCP      | Alternative HTTPS-like           | Variants for encrypted C2 to avoid standard port blocks.        |
| 8888          | TCP      | Custom tools like Sliver         | Default for some C2 frameworks.                                 |
| 31337         | TCP      | Back Orifice                     | Elite (leet) port for classic RATs.                             |
| 41337         | UDP      | Non-standard custom              | Used in ICMP-based C2 like ICMP-GOSH.                           |
| 50050/60000   | TCP      | High-port C2                     | Ephemeral ports for dynamic beacons.                            |

### Additional Notes
- Attackers prefer ports that are typically allowed through firewalls (e.g., 80/443) to maintain stealth.
- In industrial control systems (ICS), additional ports like 44818 (Ethernet/IP) or OPC ranges (1024-4999, 49152-65535) may be targeted.
- Tools like Cobalt Strike often customize profiles to use these or other ports.
- This list is not exhaustive — attackers can use virtually any port. Detection should rely on behavioral analysis rather than port numbers alone.

Use this information for defensive purposes only, such as configuring firewalls, intrusion detection systems, or network monitoring.# Common C2 Ports Used for Malicious Remote Access and Beacons

Malicious actors often use command and control (C2) servers to remotely manage compromised systems, such as through beacons that periodically "phone home" for instructions or to exfiltrate data. These communications frequently leverage common network ports to blend in with legitimate traffic or exploit specific vulnerabilities.

Ports can be categorized into two main types: **standard ports** (used to mimic normal services like web browsing) and **non-standard ports** (often associated with specific malware or tools).

## Standard Ports Often Abused for C2

These are well-known ports for legitimate protocols but frequently hijacked to hide malicious traffic.

| Port       | Protocol       | Common Use in Malware/C2                  | Examples/Notes                                                                 |
|------------|----------------|-------------------------------------------|--------------------------------------------------------------------------------|
| 21         | TCP (FTP)      | File transfer for payloads or exfiltration | Used by trojans like DarkFTP for control channels.                             |
| 22         | TCP (SSH)      | Secure remote access tunneling            | Malware may tunnel C2 over SSH to evade detection.                             |
| 23         | TCP (Telnet)   | Insecure remote access                    | Older malware uses for backdoor access; seen in ICS attacks.                   |
| 25         | TCP (SMTP)     | Email-based exfiltration or callbacks     | Non-standard use in tools like WellMail.                                       |
| 53         | TCP/UDP (DNS)  | DNS tunneling for stealthy beacons        | Common for data exfiltration; hard to detect in normal DNS traffic.            |
| 80         | TCP (HTTP)     | Web-based beacons and callbacks           | Widely used to blend with web traffic; e.g., Stuxnet callbacks.                |
| 443        | TCP (HTTPS)    | Encrypted C2 channels                     | Most common for secure, hidden communications; e.g., in botnets like TrickBot. |
| 6667       | TCP (IRC)      | Botnet control channels                   | Historically used for IRC-based C2 in trojans like Bionet.                     |
| 995        | TCP (POP3S)    | Encrypted email protocol abuse for C2     | Frequently used by Qakbot/Qbot for callbacks and beacons.                      |

## Non-Standard Ports Commonly Associated with Malware

These are often used by specific trojans, RATs (Remote Access Trojans), or tools like Cobalt Strike and Metasploit for beacons and remote access.

| Port          | Protocol | Common Use in Malware/C2                  | Examples/Notes                                                                 |
|---------------|----------|-------------------------------------------|--------------------------------------------------------------------------------|
| 135           | TCP/UDP  | Propagation and control                   | Exploited by worms like Blaster.                                               |
| 139           | TCP      | Network resource access                   | Used for spreading via shared drives.                                          |
| 1080          | TCP      | Virus propagation                         | Associated with MyDoom.                                                        |
| 1214          | TCP      | P2P file sharing backdoors                | Linked to KAZAA trojans.                                                       |
| 2140/3150     | TCP      | Deep Throat RAT                           | Backdoor access and control.                                                   |
| 2222          | TCP      | Alternative SSH or custom C2              | Seen in Qakbot campaigns, botnets, and some SSH-tunneled backdoors.            |
| 2404          | TCP      | Custom C2                                 | Observed in recent threat reports.                                             |
| 2708          | TCP/UDP  | Custom or rare C2                         | Occasionally referenced in malware samples; less common/highly variable.       |
| 32103         | TCP      | High-port custom C2                       | Commonly configured in Qakbot/Qbot for beaconing and control.                  |
| 4444          | TCP      | Metasploit default                        | Common in penetration testing tools abused maliciously.                         |
| 5001          | TCP      | Non-standard backdoor/C2                  | Associated with older trojans (e.g., Sockets des Troie) and some custom tools. |
| 61202         | TCP      | High-port custom C2                       | Observed in Qakbot and related banking trojan campaigns for beacons.           |
| 7443/8443/8848| TCP      | Alternative HTTPS-like                    | Variants for encrypted C2 to avoid standard port blocks.                       |
| 8888          | TCP      | Custom tools like Sliver                  | Default for some C2 frameworks.                                                |
| 31337         | TCP      | Back Orifice                              | Elite (leet) port for classic RATs.                                            |
| 41337         | UDP      | Non-standard custom                       | Used in ICMP-based C2 like ICMP-GOSH.                                          |
| 50050/60000   | TCP      | High-port C2                              | Ephemeral ports for dynamic beacons.                                           |

### Additional Notes
- Attackers prefer ports that are typically allowed through firewalls (e.g., 80/443) or mimic legitimate encrypted services (e.g., 995 for secure email) to maintain stealth.
- High/non-standard ports like 32103, 61202, etc., are especially common in banking trojans such as **Qakbot** (Qbot), which dynamically configures lists of ports/IPs for resilience.
- In industrial control systems (ICS), additional ports like 44818 (Ethernet/IP) or OPC ranges (1024-4999, 49152-65535) may be targeted.
- Tools like Cobalt Strike often customize profiles to use these or other ports.
- This list is not exhaustive — attackers can use virtually any port. Detection should rely on behavioral analysis, TLS fingerprinting, domain generation algorithms (DGA), and traffic patterns rather than port numbers alone.