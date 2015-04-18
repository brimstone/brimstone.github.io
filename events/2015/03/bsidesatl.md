Bsides Atlanta
--------------
######Sat Mar 14 2015

Advanced SIEM Optimization
--------------------------
@reliaquest
- Security Incident & Event Management
- Similar to IDS/IPS
- Different than ELK somehow
- Need to keep feeding a SIEM install
- SIEM systems injest syslog, web server logs, router logs, etc
- Don't flood people with alerts
- filter filter filter
- log DNS on your network, especially for mobile users
- log when VMs are created
- attribute DHCP activity to users
- is there a way to log mysql access denied errors?
- is it easy to scrape pastebin, twitter, or google for the company?
- regular nmap scans
- honeypots, honey hashes, canery files/records
- threat sharing programs: alienvault, facebook
- pcap parsing with nield
- use commercial feeds as "bad data" and try to recreate an attack under your own control
- know where your A records go
- monitor unused ip address ranges

Operationalizing Threat Intelligence
------------------------------------
- goes to cons to "maintain threat situatiinal awareness"
- iso iso iso
- more time documenting than anything else
- policy
- don't conflate Threat, Vulnerability, and Risk.
- Threat * Probability * Business Impact = Risk
- colors are important to management
- Do I need to stop normal patch policies to patch this vuln?

Malware Infection Visualized
----------------------------
- sysmon 2.0+, carbon black
- these programs make neat graphs of what exes call which exes
- sysmon is free, but carbon black runs on linux
- google "googleupdate /ping"

Buy The Dip
-----------
@dearestleader
- compliance, no tech
- very finance centered
- wall street and consumers don't care about data breaches
- buy more insurance
- "people and creativity are your greatest assets"

Online, No One Knows You're Dead
--------------------------------
- Defensive Security Podcast
- need to make a paper copy of all personal assets
- need to make sure there's at least someone else on everything
- Google Inactive Account Manager
- Recommemdations
 - Legacy drawer (daveramsey.com)
 - Switch roles for a month once a year
 - Password/recovery keys
 - Password Manager
 - Life Insurance
 - Store shared digital memories someplace shared

Hacking 802.15.4
----------------
- apimote wifi hacking board
- packet in packet is kinda like vlan hopping
- need to becareful with native vlan access

The Art of Speaking with Muggles
--------------------------------
- southern fried security podcast
- SBAR Situation Background Analyis Recommend
-