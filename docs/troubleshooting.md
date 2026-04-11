# Troubleshooting Guide - Helpdesk Lab

## Boot Issues
### No bootable device found
1. Verify RAM is sufficient (minimum 4GB for Windows 10/11)
2. Check boot order (Optical should be first)
3. Try disabling EFI for Windows 10 VMs
4. Verify ISO is not corrupted

## Network Issues
### VMs cannot communicate
1. Ensure all VMs use same Internal Network name
2. Verify IP addresses are in same subnet (192.168.1.x)
3. Check Windows Firewall (disable temporarily for testing)

## Domain Join Issues
### Cannot join domain
1. Verify DNS points to DC (192.168.1.10)
2. Run: `nslookup corp.local`
3. Check if using Windows Home (needs Pro)
