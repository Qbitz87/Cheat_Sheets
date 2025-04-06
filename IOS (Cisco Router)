## Navigating Modes
```bash
# User EXEC Mode >
enable                     # Enter Privileged EXEC mode

# Privileged EXEC Mode #
disable                    # Return to User EXEC mode
configure terminal         # Enter Global Configuration mode (abbr: conf t)
copy running-config startup-config # Save current config (abbr: copy run start, wr)
show <command>             # Execute verification commands (e.g., show ip route)
reload                     # Reboot the router

# Global Configuration Mode (config)#
hostname <name>            # Set router hostname
interface <type/number>    # Enter Interface Configuration mode (e.g., interface g0/0)
line <type> <number>       # Enter Line Configuration mode (e.g., line console 0)
router <protocol> <id>     # Enter Router Configuration mode (e.g., router ospf 1)
ip route ...               # Configure static routes
enable secret <password>   # Set encrypted privileged mode password
banner motd #<msg>#        # Set Message of the Day banner
exit                       # Go back one level

# Interface Configuration Mode (config-if)#
ip address <ip> <mask>   # Set IPv4 address
ipv6 address <ipv6/len>  # Set IPv6 address
description <text>         # Add interface description
no shutdown                # Enable interface (make active)
shutdown                   # Disable interface
speed <auto|10|100|1000>   # Set interface speed (use ? for options)
duplex <auto|half|full>    # Set interface duplex (use ? for options)
exit                       # Return to Global Config mode

# Line Configuration Mode (config-line)#
password <password>        # Set line password (console, vty)
login                      # Enable password checking on login (for console/vty)
transport input <ssh|telnet|all|none> # Define allowed protocols for VTY lines
exit                       # Return to Global Config mode

# Router Configuration Mode (config-router)#
network <ip> <wildcard> area <id> # Example for OSPF
exit                       # Return to Global Config mode

# General Navigation
end                        # Return directly to Privileged EXEC mode from any sub-config mode
Ctrl+Z                     # Same as 'end'
Ctrl+C                     # Abort current command/input
```

## Basic Configuration
```bash
# In Global Configuration Mode (config)#
hostname <RouterName>          # Set the device hostname
enable secret <StrongPassword> # Set the encrypted privileged EXEC password
banner motd # Warning Text #   # Set login banner (use any delimiting char like #)
no ip domain-lookup            # Disable DNS lookup for mistyped commands
service password-encryption    # Encrypts non-secret passwords in config (weak)

# Console Port Security
line console 0
 password <ConsolePassword>
 login
 exec-timeout <min> <sec>      # Set console inactivity timeout (e.g., 5 0 for 5 min)

# VTY Lines (Telnet/SSH) Security
line vty 0 4                   # Select first 5 VTY lines (adjust range as needed)
 password <VtyPassword>
 login
 transport input ssh          # Allow only SSH (recommended)
 exec-timeout <min> <sec>      # Set VTY inactivity timeout
```

## Interface Configuration
```bash
# In Interface Configuration Mode (config-if)#
description <Purpose of Interface>     # Document the interface's role
ip address <ip_address> <subnet_mask>  # Assign IPv4 address
ipv6 address <ipv6_address/prefix>     # Assign IPv6 address
ipv6 enable                            # Enable IPv6 processing on the interface (needed for link-local)
no shutdown                            # Enable the interface (bring it up)
shutdown                               # Disable the interface (bring it down)
speed <auto | 10 | 100 | 1000>         # Set interface speed (if supported)
duplex <auto | half | full>            # Set interface duplex (if supported)
clock rate <bps>                       # Set clock rate on DCE serial links (e.g., 64000)
encapsulation <type>                   # Set WAN encapsulation (e.g., ppp, hdlc, frame-relay)
```

## Routing Configuration
```bash
# In Global Configuration Mode (config)#
# Static Routes
ip route <dest_net> <mask> <next_hop_ip | exit_interface>   # IPv4 static route
ipv6 route <dest_prefix/len> <next_hop_ipv6 | exit_interface> # IPv6 static route

# OSPF Example
router ospf <process_id>               # Enable OSPF (e.g., router ospf 1)
 router-id <ip_address>               # Manually set router ID (recommended)
 network <network> <wildcard> area <id> # Advertise networks in OSPF

# EIGRP Example
router eigrp <as_number>               # Enable EIGRP (e.g., router eigrp 100)
 network <network> [wildcard]         # Advertise networks in EIGRP
 no auto-summary                      # Disable auto-summary (recommended)
```

## Verification (Show Commands)
```bash
# In Privileged EXEC Mode #
show running-config            # Display current active configuration (abbr: sh run)
show startup-config            # Display configuration saved in NVRAM (abbr: sh start)
show ip interface brief        # Summary of interface IPv4 status and IPs (abbr: sh ip int br)
show ipv6 interface brief      # Summary of interface IPv6 status and IPs
show interfaces                # Detailed status for all interfaces (abbr: sh int)
show interfaces <type/number>  # Detailed status for a specific interface
show ip route                  # Display IPv4 routing table (abbr: sh ip ro)
show ipv6 route                # Display IPv6 routing table
show protocols                 # Display Layer 3 protocol status on interfaces
show version                   # System info, IOS version, uptime (abbr: sh ver)
show cdp neighbors             # Show connected Cisco devices (abbr: sh cdp nei)
show cdp neighbors detail      # Detailed CDP information
show ip protocols              # Show routing protocol parameters (OSPF, EIGRP, etc.)
show history                   # Show command history for the current session
show clock                     # Show system time/date
show logging                   # Show system log buffer (abbr: sh log)
```

## Saving & Managing Configuration
```bash
# In Privileged EXEC Mode #
copy running-config startup-config # Save current config to NVRAM (abbr: copy run start, wr)
erase startup-config           # Delete the startup configuration (abbr: erase start)
reload                         # Reboot the router (prompts to save if needed)
copy <source_url> <dest_url>   # Copy files (e.g., copy tftp: running-config)
```

## Management & Security (SSH Example)
```bash
# In Global Configuration Mode (config)#
ip domain-name <yourdomain.com>   # Required for RSA key generation
crypto key generate rsa         # Generate RSA keys (choose modulus size, e.g., 2048)
ip ssh version 2                # Use SSHv2 (more secure)

username <admin_user> secret <AdminPassword> # Create local user for SSH login
line vty 0 4
 transport input ssh
 login local                    # Use local user database for VTY login
```

## Troubleshooting
```bash
# In Privileged EXEC Mode #
ping <ip_address | hostname>   # Test L3 connectivity (ICMP Echo)
traceroute <ip_addr | host>  # Trace network path (abbr: trace)
show controllers <int>       # Show hardware details, check serial cable type (DCE/DTE)
show processes cpu             # Check CPU utilization
show memory                    # Check memory utilization
debug <protocol | feature>     # Enable real-time debugging (USE WITH CAUTION!)
undebug all                    # Disable all debugging (abbr: u all, no debug all)
```

---
