# Environment

This document describes the operating system, runtime, and network environment
used for the Raspberry Pi Kubernetes cluster.

---

## Control Machine (kubectl)

- **Host:** ro6bx (Linux desktop)
- **Network:** USB Wi-Fi adapter
- **Static IPv4:** 192.168.1.86/24
- **Gateway:** 192.168.1.254
- **Config Method:** NetworkManager (`nmcli`)
- **Kubeconfig:** `~/.kube/config` copied from `rpi-master:/etc/kubernetes/admin.conf`

---

## Cluster Nodes

All Raspberry Pi nodes use wired Ethernet with OS-level static IPv4 set via Netplan.

| Node Name     | Role          | IPv4 Address      | OS                | Kernel               | Container Runtime          | Kubernetes |
|--------------|---------------|-------------------|-------------------|----------------------|----------------------------|-----------|
| rpi-master   | control-plane | 192.168.1.116/24  | Ubuntu 22.04.5 LTS| 5.15.0-1092-raspi     | containerd://1.7.28        | v1.31.14  |
| rpi-worker1  | worker        | 192.168.1.117/24  | Ubuntu 22.04.5 LTS| 5.15.0-1092-raspi     | containerd://1.7.28        | v1.31.14  |
| rpi-worker2  | worker        | 192.168.1.115/24  | Ubuntu 22.04.5 LTS| 5.15.0-1092-raspi     | containerd://1.7.28        | v1.31.14  |
| rpi-worker3  | worker        | 192.168.1.118/24  | Ubuntu 22.04.5 LTS| 5.15.0-1092-raspi     | containerd://1.7.28        | v1.31.14  |

---

## Network Characteristics

- **Topology:** Single LAN
- **Gateway:** 192.168.1.254
- **DNS:** 1.1.1.1, 8.8.8.8
- **IP Persistence:** Static (Netplan on Pis, NetworkManager on desktop)
- **SSH:** Supported by hostname and IP

---

## Rationale

Static IP addressing is used to:
- Prevent Kubernetes node IP churn
- Preserve SSH stability (known_hosts)
- Simplify cluster operations and troubleshooting
- Avoid dependency on ISP-managed router configuration
