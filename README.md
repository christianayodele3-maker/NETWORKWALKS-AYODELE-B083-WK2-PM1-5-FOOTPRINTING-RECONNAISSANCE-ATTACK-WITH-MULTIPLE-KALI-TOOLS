# NETWORKWALKS-AYODELE-B083-WK2-PM1-5-FOOTPRINTING-RECONNAISSANCE-ATTACK-WITH-MULTIPLE-KALI-TOOLS
# Footprinting & Network Scanning: Penetration Testing Project

**Pentester:** Samuel Ayodele    
**Program:** Networkwalks, Cybersecurity  
**Date:** 24 September 2026  

> The full penetration testing report is submitted separately as a document. This README is a summary of the work.

## Overview
This project covers the first two phases of a penetration test: footprinting (information gathering) and network scanning, done with tools in Kali Linux.

## Scope and Authorization
| Target | Permission |
|--------|-----------|
| networkwalks.com | Written permission secured |
| My own local LAN | Own network |

Only test systems you own or have written permission to test.

## Part 1: Footprinting (networkwalks.com)

| Tool | Command | Purpose | Finding |
|------|---------|---------|---------|
| whois | `whois networkwalks.com` | Domain registration details |Registrar: GoDaddy. Created 6 Nov 2019, expires 6 Nov 2027. Name servers: Hostgator. Owner hidden by privacy service. DNSSEC unsigned. |
| whatweb | `whatweb networkwalks.com` | Fingerprint web technologies |Apache server running WordPress 7.1.2 with Download Manager 3.3.58 plugin. Uses jQuery and Bootstrap. IP 192.232.216.135. Redirects HTTP to HTTPS. |
| nslookup | `nslookup networkwalks.com` | Resolve domain to IP address |Resolves to IP 192.232.216.135 (matches whatweb). Answered by DNS server 8.8.8.8 (non-authoritative). |
| curl | `curl -I https://networkwalks.com` | Read HTTP response headers |HTTP/2 200 OK. Apache (version hidden). Secure, HttpOnly cookie. WordPress API exposed. Missing security headers (HSTS, X-Frame-Options, CSP). |
| wafw00f | `wafw00f networkwalks.com` | Detect a WAF |Behind a ModSecurity (SpiderLabs) Web Application Firewall, detected with 2 requests (wafw00f v2.4.2). |
| dnsrecon | `dnsrecon -d networkwalks.com` | Enumerate DNS records |A record: 192.232.216.135. NS: ns6135/ns6136.hostgator.com. MX: mail.networkwalks.com (same IP). SPF record present. No DNSSEC. Name servers expose BIND version 9.16.23-RH. |

Screenshots are in the `screenshots/` folder.

## Part 2: Network Scanning (Zenmap, my own LAN)
- **Network configuration:** <!-- your IP, subnet, gateway -->
- **Active hosts discovered:** <!-- number of hosts and their IPs -->
- **IP and MAC addresses:** <!-- list of what you collected -->
- **Network topology:** 


 


## Recommendations
- Limit the technology and version details exposed in HTTP headers.
- Keep the WAF rules and web server software up to date.
- Remove unused DNS records and subdomains.
- Keep a record of the devices on your network and investigate unknown hosts.
- Enable security headers (HSTS, X-Frame-Options, X-Content-Type-Options, CSP).
- Hide WordPress and plugin version numbers and keep them updated.
- Enable DNSSEC.
- Hide the BIND version on the name servers.
## Conclusion
This project gave me hands-on practice with the first stages of a penetration test. Using six Kali Linux tools (whois, whatweb, nslookup, curl, wafw00f and dnsrecon), I gathered information about networkwalks.com without attacking it: its registration details, technologies, IP address, HTTP headers, DNS records, and the fact that it sits behind a ModSecurity WAF. I then used Zenmap on my own local network to find active hosts and record their IP and MAC addresses.

The main lesson is that a lot can be learned about a target before any exploitation, just from public information and network responses. I also learned that good reporting matters: each finding should say what was done, what was found, what it means, what risk it creates, and how to reduce it. Finally, all of this work must stay within an authorized scope, and mine was done with written permission and on my own network for learning purposes.

## Disclaimer
This work was done for educational purposes with permission from the target owner.
