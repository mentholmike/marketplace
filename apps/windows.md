---
id: windows
name: Windows (Docker)
category: gaming
description: Run Windows in Docker. A complete Windows 10/11 environment in your browser via noVNC.
image: dockur/windows:latest
ports: [8006]
environment:
  - name: VERSION
    description: Windows version to install (win10, win11, win10ltsc)
    required: false
    default: win11
  - name: RAM_SIZE
    description: RAM allocated to Windows (e.g., 4G, 8G)
    required: false
    default: 8G
  - name: CPU_CORES
    description: Number of CPU cores
    required: false
    default: "4"
  - name: DISK_SIZE
    description: Disk size in GB
    required: false
    default: "64"
volumes:
  - name: windows-data
    description: Windows data and configuration
    required: true
    default: ./windows/data
---

# Windows (Docker)

## Description
Run a full Windows 10 or 11 environment in Docker. Access it through your browser via noVNC — no extra software needed on the client.

## Ports
- **8006** — noVNC web interface

## Environment Variables
| Variable | Required | Default | Description |
|----------|----------|---------|-------------|
| `VERSION` | No | win11 | Windows version: win10, win11, win10ltsc |
| `RAM_SIZE` | No | 8G | RAM allocated to Windows |
| `CPU_CORES` | No | 4 | Number of CPU cores |
| `DISK_SIZE` | No | 64 | Disk size in GB |

## Volumes
| Volume | Description |
|--------|-------------|
| `windows-data` | Windows data and configuration |

## Docker Compose
```yaml
services:
  windows:
    image: dockur/windows:latest
    container_name: windows
    ports:
      - "8006:8006"
    environment:
      - VERSION=${VERSION:-win11}
      - RAM_SIZE=${RAM_SIZE:-8G}
      - CPU_CORES=${CPU_CORES:-4}
      - DISK_SIZE=${DISK_SIZE:-64}
    volumes:
      - ./windows/data:/storage
    devices:
      - /dev/kvm:/dev/kvm
    cap_add:
      - NET_ADMIN
    restart: unless-stopped
```

## Notes
- Access Windows at `http://your-server:8006` via noVNC
- First boot downloads and installs Windows — allow 20-30 minutes
- Requires KVM support on the host (nested virtualization)
- Enable in BIOS/UEFI: Intel VT-x/AMD-V or KVM
- For fullscreen, click the monitor icon in noVNC toolbar
- Default login is automatic (auto-logon enabled)
