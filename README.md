# Cybersecurity Incident Analysis 📓

## Overview
This repository showcases cybersecurity incident response and network traffic analysis skills through detailed case studies. Each analysis demonstrates practical application of network protocol knowledge, threat detection, and professional incident documentation.

## Skills Demonstrated
- Network traffic analysis using tcpdump
- DNS and ICMP protocol troubleshooting
- Incident response documentation
- Root cause analysis
- Network security assessment

---

## Case Study: DNS Server Failure Investigation

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

## Incident Report

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

## Technical Skills Demonstrated

**Network Analysis:**
- TCP/IP model layer analysis (Network and Transport layers)
- Protocol identification and behavior analysis
- Network troubleshooting using command-line tools

**Incident Response:**
- Systematic investigation methodology
- Professional documentation of findings
- Risk assessment and prioritization

**Security Assessment:**
- Attack vector identification (DoS possibilities)
- Service availability impact analysis
- Infrastructure vulnerability assessment

---

## Professional Impact

This analysis demonstrates the ability to identify and diagnose network service failures quickly, providing actionable intelligence for incident response teams. The systematic approach to packet analysis and clear documentation enables rapid escalation and resolution of critical infrastructure issues.

The investigation methodology presented here adheres to industry-standard practices for network security analysis and incident documentation.
