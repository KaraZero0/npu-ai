# PERSONAL INFRASTRUCTURE & CONTEXT (EXAMPLE)

Copy this file to `context.md` (gitignored) to give `npu-ai` awareness of your setup.

## Local Workstation
- **OS**: Arch Linux / EndeavourOS (KDE Plasma 6 Wayland)
- **CPU / NPU**: Intel Core Ultra (Intel AI Boost NPU via `intel_vpu`)
- **Shell & Tools**: Zsh, `pacman` / `yay`, `btop`, `lsd`, `bat`

## Remote Hosts (Optional)
1. **Home Server (`homelab`)**:
   - IP: `<TAILSCALE_IP>` (Tailscale) / `192.168.1.100` (LAN)
   - Services: Docker Compose, Prometheus, Grafana, Ollama
2. **Edge Node (`rpi`)**:
   - Hostname: `dietpi` | IP: `192.168.1.50`
