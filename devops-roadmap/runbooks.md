# Step-by-step runbooks

One sub-tab per phase. Work them in order: each phase leaves running what the next one needs. Every command assumes the placeholders and IP plan below, so set those once and swap in your real values.

## Before you start

1. Snapshot the Proxmox host's config (`/etc/pve`) and your clean-state cluster nodes.
2. Fill in the placeholder table with your real values, then search-and-replace as you copy commands.
3. Keep a terminal log: `script -a ~/lab-$(date +%F).log` on your admin VM records everything you type.

## Placeholders

| Placeholder | Meaning | Example |
| --- | --- | --- |
| `<PVE_HOST>` | Proxmox host IP | 192.168.1.10 |
| `<NODE>` | Proxmox node name | pve |
| `<TEMPLATE_ID>` | VM ID of your golden image, converted to a template | 9000 |
| `<STORAGE>` | Proxmox storage for VM disks | local-lvm |
| `<BRIDGE>` | Proxmox network bridge | vmbr0 |
| `<GW>` | LAN gateway | 192.168.1.1 |
| `<NAS_IP>` | Your existing NAS VM | 192.168.1.15 |
| `lab.internal` | Private DNS zone for the lab | lab.internal |

## IP plan

| Host | IP (example) | Built in |
| --- | --- | --- |
| admin (your workstation VM) | .19 | Phase 1 |
| dns | .20 | Phase 2 |
| gitea | .21 | Phase 1 |
| squid | .22 | Phase 2 |
| lb (Nginx) | .30 | Phase 2 |
| web1, web2 | .31, .32 | Phase 2 |
| runner | .40 | Phase 4 |
| harbor | .41 | Phase 4 |
| vault1 to vault3 | .42 to .44 | Phase 4 |
| k8s cp1 to cp3 | .50 to .52 | Phase 5 |
| k8s w1 to w3 | .53 to .55 | Phase 5 |

Use your own subnet. Reserve these addresses in your router's DHCP so nothing else takes them.
