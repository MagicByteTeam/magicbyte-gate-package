# MagicByte Gate — Installation Guide

MagicByte Gate is a self-hosted Web Application Firewall (WAF) that filters and monitors HTTP traffic between your web applications and the internet, protecting against SQL injection, XSS, RCE, brute force, and other attacks.

## Requirements

- Linux (Ubuntu 20.04+ / Debian 11+ recommended)
- Python 3.7+
- Docker 20.0+ (installer can install it automatically)
- Docker Compose (plugin or standalone)
- At least 2 GB of free disk space
- Root access

## Quick Install

```bash
curl -fsSL -o install.sh https://github.com/MagicByteTeam/magicbyte-gate-package/releases/latest/download/install.sh
sudo bash install.sh
```

The installer will ask for:
- Installation path (default: `/data/magicbyte-gate`)
- HTTP port (default: `80`)
- HTTPS port (default: `443`)
- Admin email and password

After installation the management panel is available at:

```
https://<your-server-ip>:2443/
```

## Managing the Installation

Run the installer again to access management options:

```bash
sudo bash install.sh
```

Available actions:
- **Install** — fresh installation
- **Upgrade** — update to the latest version
- **Uninstall** — remove MagicByte Gate and all data
- **Repair** — fix common issues (migrations, permissions, nginx, admin password reset)
- **Restart** — restart all containers
- **Backup** — create a backup of data and configuration

Or pass the action directly:

```bash
sudo bash install.sh install
sudo bash install.sh upgrade
sudo bash install.sh restart
sudo bash install.sh backup
```

## Manual Installation

If you prefer to install manually without the installer:

```bash
# Download the compose file
curl -fsSL -o docker-compose.yml https://github.com/MagicByteTeam/magicbyte-gate-package/releases/latest/download/docker-compose.release.yml

# Create .env file
cat > .env <<EOF
APP_KEY=base64:$(openssl rand -base64 32)
DB_PASSWORD=$(openssl rand -base64 24)
ADMIN_EMAIL=admin@yourdomain.com
ADMIN_PASSWORD=yourpassword
HTTP_PORT=80
HTTPS_PORT=443
EOF

# Start
docker compose up -d
```

## Troubleshooting

**Check container status:**
```bash
docker ps
docker logs magicbyte-gate-app
```

**Repair options (via installer):**
```bash
sudo bash install.sh repair
```

**Use English language:**
```bash
sudo bash install.sh --en
```
