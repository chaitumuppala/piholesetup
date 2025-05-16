# piholesetup

Pi-hole Setup on Raspberry Pi
This README summarizes the steps taken to set up Pi-hole on a Raspberry Pi Zero 2 and configure networking for DNS-based ad blocking.

Table of Contents
Overview
Prerequisites
Installation Steps
Network Configuration
Static IP Setup
DNS Configuration
Troubleshooting
DNS Resolution Issues
Network Connectivity
IPv6 DNS Issues
Validation
Overview
Pi-hole is a network-wide ad blocker that acts as a DNS sinkhole to block unwanted content before it reaches your devices. This guide documents the setup process on a Raspberry Pi Zero 2.

Prerequisites
Raspberry Pi Zero 2 with Raspbian OS installed
Network connection
Router access (for DHCP configuration)
Installation Steps
Update package repositories (with IPv4 forcing due to DNS issues):

Configure static IP address using NetworkManager:

Prevent DNS overrides from DHCP:

Apply network configuration:

Install Pi-hole:

Network Configuration
Static IP Setup
Used NetworkManager (instead of dhcpcd) to configure static IP address at 192.168.68.120
Created persistent DNS settings that wouldn't be overwritten by ACT Fibernet's DNS servers
Restarted NetworkManager with: sudo systemctl restart NetworkManager
DNS Configuration
Configured router's DHCP server to distribute Pi-hole IP (192.168.68.120) as DNS server
Set client devices to use Pi-hole for DNS resolution
For Windows clients with persistent IPv6 DNS settings, used these commands:
Troubleshooting
DNS Resolution Issues
Fixed ACT Fibernet DNS redirection issues by forcing IPv4 for apt:
Made this setting permanent by creating configuration file:
Network Connectivity
Identified correct network service (NetworkManager instead of networking.service)
Verified static IP configuration with: ip addr
Tested DNS resolution with: nslookup doubleclick.net
IPv6 DNS Issues
Identified issues with IPv6 DNS servers bypassing Pi-hole
Disabled IPv6 DNS on client devices using:
Restored normal DNS settings after testing with:
Validation
Verified Pi-hole installation by accessing admin dashboard at http://192.168.68.120/admin
Tested ad blocking by visiting ad-heavy websites
Confirmed DNS resolution was properly routing through Pi-hole
For more information on Pi-hole configuration and features, visit: https://docs.pi-hole.net/
