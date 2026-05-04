## VLAN Guest Network Failure (Outage Incident)

Yup... 
Took down the network while configuring guest vlan. 
Here's the break down:
## Summary
During the initial attempt to deploy a guest network using VLAN segmentation,
a misconfiguration caused a loss of network connectivity for all devices except for
pfsense(_thank god_).

## Change Introduced
- Created new VLAN for guest network 
- Modified switch port config to support VLAN tagging 
- Updated pfSense interface config for VLAN assignment 

## Impact
- Lost connection to wired device connected to switch immediately after pushing new config 
- Clients unable to obtain IP addresses (DHCP failure) 
- Loss of internet connectivity across affected devices 
- Wireless SSID broadcasted but provided no usable network access 

## Odd / Unexpected Behavior
- Hardwiring directly into pfSense still provided network access 
- Only two switch ports were assigned VLAN tags, but no ports provided network access 
- Suggested broader VLAN/trunk misconfiguration affecting entire switch behavior 

## pfSense Observations
- No firewall logs indicating new VLAN traffic during incident window 
- No DHCP logs for affected VLAN during incident timeframe 
- Confirmed pfSense remained operational via direct connection 

## Switch Observations
- Lost management console access immediately after configuration change 
- Regained access only after assigning static IP directly to switch 
- Behavior consistent with VLAN tagging / trunk configuration issue affecting management and client traffic 

## Recovery
- Initial attempt to access switch via static IP failed 
- Switch required physical power cycle to restore management access 
- After reboot, regained switch access and restored connectivity 
- Reverted VLAN/trunk configuration to previous working state
- Confirmed full network restoration (DHCP + internet + inter-device connectivity)

## Lesson Learned
Big takeaway from this is that VLAN changes can take the whole network down if you don’t stage them properly first. I didn’t validate the switch trunk config before applying it across the board, which basically broke communication between pfSense and everything else. Also learned that switch management access can get wiped out if VLAN tagging is off, so you’re forced into physical recovery steps like a power cycle just to get back in. Going forward I’ll definitely be testing VLAN changes on a single port first and taking config backups before touching anything that affects the trunk.
