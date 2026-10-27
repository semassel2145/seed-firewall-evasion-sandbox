# VPN binaries (required before pooling)

Place these two files here, then commit them:

- `vpnclient`
- `vpnserver`

Download them from the SEED Labs "Firewall Evasion" lab page (or build them from
the lab's sample code on an Ubuntu 24.04 x86_64 machine so they match the sandbox images).

The playbook copies them to `/opt/seed-vpn/` with mode `0755`.
The `copy` tasks fail if either file is missing, which stops a broken sandbox from being handed to trainees.
