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

**Traffic Flow Breakdown:**
- **Source IP:** 192.51.100.15 (Client computer)
- **Destination IP:** 203.0.113.2 (DNS server)
- **Protocol:** UDP (for DNS queries) / ICMP (for error responses)
- **Port:** 53 (DNS service port)
- **Error Pattern:** Consistent "udp port 53 unreachable" across multiple retry attempts

**Key Observations:**
1. Multiple DNS resolution attempts over 4-minute window
2. All UDP packets to port 53 resulted in ICMP unreachable responses
3. Query ID 35084 remained consistent across attempts
4. Error message lengths varied, indicating different response handling

---

## Incident Report

### Part 1: Problem Summary

**The UDP protocol reveals that:** DNS requests to resolve www.yummyrecipesforme.com are failing to reach the DNS server on port 53.

**Network analysis shows ICMP error message:** "udp port 53 unreachable"

**Port 53 is used for:** DNS (Domain Name System) service, which translates domain names into IP addresses.

**Most likely issue:** The DNS server at 203.0.113.2 is not responding on port 53, either due to service failure, server downtime, or firewall blocking.

### Part 2: Detailed Analysis

**Time incident occurred:** 13:24:32 (1:24 PM) based on tcpdump timestamps

**How IT team became aware:** Multiple customers reported being unable to access www.yummyrecipesforme.com, receiving "destination port unreachable" errors when attempting to load the webpage.

**Investigation actions taken:** 
- Reproduced the issue by attempting to visit the website
- Confirmed same error occurred during testing
- Used tcpdump network analyzer to capture and analyze network traffic
- Identified failure patterns in DNS resolution process

**Key findings:**
- UDP packets sent to DNS server (203.0.113.2) on port 53 are failing
- ICMP error messages consistently indicate "udp port 53 unreachable"
- Multiple retry attempts (at 13:24, 13:26, and 13:28) all resulted in identical errors
- DNS resolution process is completely failing, preventing browsers from obtaining IP addresses

**Root cause analysis:** The DNS server at 203.0.113.2 is either down, experiencing technical issues, or port 53 is being blocked by a firewall configuration. This prevents the DNS service from responding to domain name resolution requests, making the website inaccessible to users even though the web server itself may be functioning properly.

**Recommended next steps:**
1. Check DNS server status and logs
2. Verify firewall rules for port 53 traffic
3. Test connectivity to backup DNS servers
4. Contact DNS service provider if using external service
5. Implement temporary DNS failover if available

---

## Technical Skills Demonstrated

**Network Protocols:**
- TCP/IP model understanding
- UDP protocol analysis
- ICMP error message interpretation
- DNS resolution process knowledge

**Analysis Tools:**
- tcpdump packet capture and analysis
- Network traffic pattern recognition
- Log file interpretation

**Incident Response:**
- Systematic troubleshooting methodology
- Professional incident documentation
- Root cause analysis
- Technical communication

**Problem-Solving Approach:**
- Hypothesis formation based on symptoms
- Data collection and analysis
- Pattern recognition in network behavior
- Solution prioritization

---

## About This Analysis

This case study demonstrates the practical application of network security knowledge in a real-world scenario. The investigation showcases the ability to:

- Quickly identify network protocol issues
- Use appropriate tools for traffic analysis
- Document findings in professional incident reports
- Communicate technical issues clearly to stakeholders
- Provide actionable recommendations for resolution

The systematic approach taken in this analysis reflects industry best practices for cybersecurity incident response and network troubleshooting.
