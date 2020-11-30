# Silver Peak Edge Connect EVE-NG Bootsrap
Quickly bootstrap a Silver Peak Virtual Edge Connect in EVE-NG assigning a desired Orchestrator, registering with Account/Key, and assigning MAC addresses to interfaces (up to 9 total: mgmt0, wan/lan0-3).

# Requirements
- Python3:  all script files reference #!/usr/bin/python3, modify if necessary 
- Public Python packages used: python-dotenv, colored, requests, os, getpass, time, urllib3, ipaddress
- Additional local modules called by silverpeak-eve-ec-bootstrap.py:
    - ecosHelp.py -- Basic API calls to Silver Peak Edge Connect OS
    - silverpeak_ec_assign_orch.py -- Function for assigning an Orchestrator and Account to an Edge Connect
        - can be run on it's own
    - silverpeak_ec_automap.py -- Function for assigning available MAC addresses to interfaces based on incrementing MAC's
        - can be run on it's own


# Quick Start

1. Set Environment Variables
```
export ORCH_URL="<ORCH-URL-OR-IP>" 
export ACCOUNT="<ORCH-ACCOUNT-NAME>" 
export ACCOUNT_KEY="<ORCH-ACCOUNT-KEY>" 
```
Also modeled in dotenv.txt and can be set in a .env file


2. Add Silver Peak Edge Connect nodes to your EVE-NG lab
- Change number of interfaces as desired (default is 4, auto-map supports up to 9)
- Change console to 'vnc' (default is 'telnet')
- Connect the first interface on each Edge Connect (e0) to be able to reach Orchestrator outside of EVE-NG (e.g. Management(Cloud0))
- Open the console to each Edge Connect to obtain it's IP address


# Syntax

Run the script and then enter each Edge Connect mgmt0 IP address to be bootstrapped. The script will check that the IP entered is a valid IP address and that it can currently ping the address.

When entry is complete mark 'n' and then confirm 'y' to proceed with the confirmed IP's.

Example:

```
> python3 silverpeak_eve_ec_boostrap.py
> Please enter IP of Edge Connect (e.g. 10.1.30.100): 10.1.30.67
PING 10.1.30.67 (10.1.30.67): 56 data bytes

--- 10.1.30.67 ping statistics ---
1 packets transmitted, 1 packets received, 0.0% packet loss, 1 packets out of wait time
round-trip min/avg/max/stddev = 3.389/3.389/3.389/0.000 ms
> 10.1.30.67: Edge Connect has been added to list for bootstrap
> Do you want to enter more Edge Connects? (y/n): n
> These are the Edge Connects that will be bootstrapped:
> 10.1.30.15
> 10.1.30.69
> Proceed? (y/n): y
```


# Behavior
Script prompts for confirmation under certain scenarios

# Validated Silver Peak Code Versions
-   Orchestrator 9.0+
-   ECOS 9.0+

Reporting Issues:
If you have bugs or other issues file them [here](issues).
