# SEED Firewall Evasion Lab (VPN) - CyberRangeCZ Sandbox Definition

Topology: `vpn-client` (client-net 10.10.1.0/24) and `vpn-server` (server-net 10.10.2.0/24)
are separated by `inet-router`, which also connects `target-net` 10.10.3.0/24 holding
`blocked-target` (10.10.3.11, Apache on port 80).

Provisioning applies:
- vpn-client: UFW `deny out on <real iface> to 10.10.3.11`, `/opt/seed-vpn/vpnclient` (0755)
- vpn-server: `net.ipv4.ip_forward=1`, NAT `MASQUERADE` on the real interface, `/opt/seed-vpn/vpnserver` (0755)
- blocked-target: web server

## Instructor solution (not provisioned)

vpn-server:
    sudo /opt/seed-vpn/vpnserver &
    sudo ifconfig tun0 192.168.53.1/24 up

vpn-client:
    sudo /opt/seed-vpn/vpnclient 10.10.2.11 &
    sudo ifconfig tun0 192.168.53.5/24 up
    sudo route add -net 10.10.3.0/24 tun0
    curl http://10.10.3.11
