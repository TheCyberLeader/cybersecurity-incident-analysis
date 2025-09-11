# Cybersecurity Incident Analysis 📓

## Overview
This showcases cybersecurity incident response and network traffic analysis skills through **educational case studies and simulated scenarios**. Each analysis demonstrates practical application of network protocol knowledge, threat detection, and professional incident documentation.

## Skills Demonstrated
- Network traffic analysis using tcpdump and Wireshark
- DNS and ICMP protocol troubleshooting
- DoS/DDoS attack identification and analysis
- TCP SYN flood attack investigation
- Incident response documentation
- Root cause analysis
- Network security assessment

---

## Case Study 1: DNS Server Failure Investigation
**Note: This is an educational simulation designed to demonstrate network analysis skills**

### Scenario
Multiple customers reported inability to access www.yummyrecipesforme.com, receiving "destination port unreachable" errors. As a cybersecurity analyst, I investigated the network traffic to identify the root cause of this service disruption.

### Network Traffic Analysis

**tcpdump Log Data:**
13:24:32.192571 IP 192.51.100.15.52444 > 203.0.113.2.domain: 35084+ A?
yummyrecipesforme.com. (24)
13:24:36.098564 IP 203.0.113.2 > 192.51.100.15: ICMP 203.0.113.2
udp port 53 unreachable length 254
13:26:32.192571 IP 192.51.100.15.52444 > 203.0.113.2.domain: 35084+ A?
yummyrecipesforme.com. (24)
13:27:15.934126 IP 203.0.113.2 > 192.51.100.15: ICMP 203.0.113.2
udp port 53 unreachable length 320
13:28:32.192571 IP 192.51.100.15.52444 > 203.0.113.2.domain: 35084+ A?
yummyrecipesforme.com. (24)
13:28:50.022967 IP 203.0.113.2 > 192.51.100.15: ICMP 203.0.113.2
udp port 53 unreachable length 150

### Technical Analysis

**Protocol Identification:**
- **UDP Protocol:** Used for DNS queries from browser to DNS server
- **ICMP Protocol:** Used for error message responses from DNS server
- **DNS Flags:** Query ID 35084+ with "A?" flag indicating DNS A record lookup

**Traffic Pattern Analysis:**
- **Log Structure:** Each incident shows 2 lines for outgoing UDP request, followed by 2 lines for ICMP error response
- **Error Consistency:** All attempts result in "udp port 53 unreachable" message
- **DNS Functionality:** Plus sign (+) after query ID indicates UDP message flags, "A?" indicates DNS A record request flag

---

## Incident Report: DNS Server Failure Investigation

### Part 1: Problem Summary

As part of the DNS protocol, the UDP protocol was used to contact the DNS server to retrieve the IP address for the domain name of yummyrecipesforme.com. The ICMP protocol was used to respond with an error message, indicating issues contacting the DNS server. 

The UDP message going from the browser to the DNS server is shown in the first two lines of every log event. The ICMP error response from the DNS server to the browser is displayed in the third and fourth lines of every log event with the error message, "udp port 53 unreachable." 

Since port 53 is associated with DNS protocol traffic, this indicates an issue with the DNS server. Issues with performing the DNS protocol are further evident because the plus sign after the query identification number 35084 indicates flags with the UDP message and the "A?" symbol indicates flags with performing DNS protocol operations. 

Due to the ICMP error response message about port 53, it is highly likely that the DNS server is not responding. This assumption is further supported by the flags associated with the outgoing UDP message and domain name retrieval.

### Part 2: Detailed Analysis

**Incident Timeline:** The incident occurred today at 1:24 p.m. (13:24:32 timestamp)

**Initial Report:** Customers notified the organization that they received the message "destination port unreachable" when they attempted to visit the website yummyrecipesforme.com.

**Current Status:** The cybersecurity team providing IT services to their client organization are currently investigating the issue so customers can access the website again.

**Investigation Findings:** During our investigation into the issue, we conducted packet sniffing tests using tcpdump. In the resulting log file, we found that DNS port 53 was unreachable.

**Next Steps:** The next step is to identify whether the DNS server is down or traffic to port 53 is blocked by the firewall.

**Suspected Root Cause:** The DNS server might be down due to a successful Denial of Service (DoS) attack or a misconfiguration. A DoS attack could flood the DNS server with requests, making it unable to respond to legitimate traffic. Alternatively, a firewall misconfiguration could be blocking traffic on port 53.

---

## Key Technical Insights

**Network Protocol Understanding:**
- DNS resolution process requires UDP communication on port 53
- ICMP provides network error messaging when services are unreachable
- DNS flags in packet headers provide diagnostic information about query types

**Diagnostic Methodology:**
- tcpdump analysis reveals communication failures at the network layer
- Pattern recognition across multiple failed attempts confirms a systematic issue
- Protocol-specific error messages pinpoint exact service failure

**Security Implications:**
- DNS service disruption affects all web traffic to affected domains
- Could indicate a targeted DoS attack against critical infrastructure
- Requires immediate investigation to restore service availability

---


## Case Study 2: SYN Flood DoS Attack Analysis
**Note: This is an educational simulation designed to demonstrate DoS attack analysis skills**

### Scenario
A travel agency's website experienced service disruption when employees reported connection timeout errors. As a security analyst, I investigated unusual network traffic patterns using Wireshark to identify the cause of the service interruption.

### Network Traffic Analysis

**Attack Pattern Identified:**
Based on Wireshark log analysis, the incident shows characteristics of a **SYN Flood DoS Attack**.

**Key Evidence:**
- Large volume of TCP SYN requests from single IP address (203.0.113.0)
- Web server overwhelmed by abnormal traffic volume
- Legitimate employee connections failing with timeout errors
- [RST, ACK] packets indicating connection resets
- HTTP/1.1 504 Gateway timeout errors

### Technical Analysis

**TCP Three-Way Handshake Process:**
1. **SYN:** Client sends synchronization request to server
2. **SYN-ACK:** Server acknowledges and reserves resources for connection
3. **ACK:** Client confirms connection establishment

**Attack Mechanism:**
The malicious actor (203.0.113.0) sent continuous SYN packets without completing the handshake, causing the server to exhaust available connection resources while waiting for ACK responses that never arrived.

---

## Incident Report: SYN Flood DoS Attack

### Section 1: Attack Identification

**One potential explanation for the website's connection timeout error message is:** A DoS attack. The logs show that the web server stops responding after it is overloaded with SYN packet requests. This event could be a type of DoS attack called SYN flooding.

**The logs show that:** A single IP address (203.0.113.0) sent an abnormally high volume of TCP SYN requests to port 443 without completing the three-way handshake process.

**This event could be:** A direct DoS attack aimed at overwhelming server resources and preventing legitimate users from accessing the website.

### Section 2: Attack Impact Analysis

**TCP Three-Way Handshake Process:**
When website visitors try to establish a connection with the web server, a three-way handshake occurs using the TCP protocol. The handshake consists of three steps:

1. **SYN packet** is sent from the source to the destination, requesting to connect.

2. **SYN-ACK packet** - The destination replies to the source with a SYN-ACK packet to accept the connection request. The destination will reserve resources for the source to connect.

3. **ACK packet** - A final ACK packet is sent from the source to the destination acknowledging the permission to connect.

**Attack Mechanism:**
In the case of a SYN flood attack, a malicious actor will send a large number of SYN packets all at once, which overwhelms the server's available resources to reserve for the connection. When this happens, there are no server resources left for legitimate TCP connection requests.

**Impact Analysis:**
The logs indicate that the web server has become overwhelmed and is unable to process the visitors' SYN requests. The server is unable to open a new connection to new visitors who receive a connection timeout message.

**Evidence from Traffic Analysis:**
- Source IP 203.0.113.0 sending excessive SYN requests to port 443
- Web server initially responding normally, then becoming overwhelmed
- Legitimate employee connections failing with timeout errors
- Server eventually stops responding to all connection attempts
  
**What happens when a malicious actor sends a large number of SYN packets:**
The server allocates resources for each SYN request, expecting to receive corresponding ACK packets. When the attacker sends only SYN packets without completing handshakes, the server's connection table fills up with half-open connections, exhausting available resources for legitimate traffic.

**Log analysis indicates:**
- Initial normal traffic between employees and web server
- Gradual increase in SYN requests from attacker IP
- Progressive degradation of legitimate connections
- Complete service failure as server resources became exhausted
- Error messages including "504 Gateway Timeout" and [RST, ACK] connection resets

**Impact on server performance:**
The attack prevented legitimate employees from accessing sales webpages, disrupting business operations and potentially affecting customer service capabilities.

---

## Immediate Response Actions Taken

**Mitigation Steps:**
1. **Server Recovery:** Temporarily took web server offline to clear connection table
2. **IP Blocking:** Configured firewall to block malicious IP address (203.0.113.0)
3. **Traffic Monitoring:** Continued packet capture to monitor for attack evolution

**Limitations of Current Solution:**
IP blocking provides only temporary protection as attackers can easily spoof different source addresses to bypass firewall rules.

**Recommended Long-term Security Measures:**
- Implement SYN flood protection mechanisms (SYN cookies, rate limiting)
- Deploy DDoS mitigation services
- Configure intrusion detection systems for early attack detection
- Establish incident response procedures for rapid attack mitigation

## Technical Skills Demonstrated Across Case Studies

**Network Protocol Analysis:**
- DNS/ICMP troubleshooting and error interpretation
- TCP three-way handshake analysis and connection state monitoring
- UDP communication pattern analysis
- HTTP/HTTPS traffic examination

**Traffic Analysis Tools:**
- tcpdump packet capture and log interpretation
- Wireshark network protocol analysis
- Network performance metrics assessment
- Pattern recognition in network behavior

**Attack Detection & Classification:**
- DoS/DDoS attack identification
- SYN flood attack pattern recognition
- DNS service failure analysis
- Network anomaly detection

**Incident Response:**
- Systematic investigation methodology
- Emergency mitigation implementation
- Professional incident documentation
- Risk assessment and impact analysis
- Security control deployment

**Technical Communication:**
- Professional report writing for technical and management audiences
- Clear documentation of complex network issues
- Actionable recommendations for security improvements
- Evidence-based root cause analysis

---

## Key Learning Outcomes & Professional Impact

**Analytical Capabilities:**
These case studies demonstrate the ability to quickly diagnose different types of network failures and security incidents using systematic approaches. The investigations showcase competency in moving from symptom identification to root cause analysis within professional timeframes.

**Technical Proficiency:**
The exercises illustrate practical application of network security concepts across multiple protocol layers (Network, Transport, Application) and different attack vectors. This includes both passive monitoring scenarios (DNS failure) and active attack situations (DoS).

**Professional Readiness:**
The documentation standards and investigation methodologies reflect industry expectations for cybersecurity analysts. Each case study follows structured incident response procedures and produces actionable intelligence for security teams.

**Problem-Solving Approach:**
Both scenarios demonstrate the ability to:
- Rapidly assess network issues using appropriate diagnostic tools
- Differentiate between infrastructure failures and malicious activities
- Implement immediate protective measures while planning long-term solutions
- Communicate technical findings clearly to different stakeholder groups

**Business Impact Understanding:**
The analyses show awareness of how technical issues affect organizational operations, from customer-facing website availability to employee productivity, demonstrating the ability to prioritize security responses based on business impact.

These educational exercises collectively showcase the analytical thinking, technical competency, and professional communication skills essential for cybersecurity incident response roles.
