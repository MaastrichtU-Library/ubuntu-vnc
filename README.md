# Ubuntu VNC Desktop

Ubuntu desktop environment with VNC access

## Purpose

Provides a lightweight Ubuntu desktop accessible via web browser for:
- fMRI analysis with FSL
- Running bash scripts  
- CLI-based neuroimaging tools
- Python scripting for data analysis

## Based On

This image is based on [vemonet/docker-ubuntu-vnc-desktop](https://github.com/vemonet/docker-ubuntu-vnc-desktop) with modifications for MRI workflows at Maastricht University.

### Changes from Original

**Removed:**
- ❌ Chrome/Chromium browser
- ❌ FFmpeg and media processing tools
- ❌ Media players (VLC, etc.)
- ❌ ARM architecture support
- ❌ Web development tools
- ❌ Unnecessary desktop applications

**Kept:**
- ✅ Ubuntu 20.04 LTS base
- ✅ LXDE lightweight desktop environment
- ✅ x11vnc + noVNC for browser-based access
- ✅ Supervisor for process management
- ✅ Basic CLI tools (git, vim, curl, wget)
- ✅ Terminal emulator

## Usage

### Deploy on DSRI OpenShift

Use the template in the [dsri-documentation](https://github.com/MaastrichtU-IDS/dsri-documentation) repository.

### Local Testing
```bash
# Build the image
docker build -t dsri-ubuntu-vnc:test .

# Run locally
docker run -d -p 6080:80 -e PASSWORD=test123 --name vnc-test dsri-ubuntu-vnc:test

# Access in browser: http://localhost:6080
# Password: test123

# Cleanup
docker stop vnc-test && docker rm vnc-test
```

## Persistent Storage

When deployed on DSRI, use the `/root/persistent` directory for files that should survive pod restarts.
```bash
# Example: Install software to persistent location
mkdir -p /root/persistent/bin

# Add to PATH
echo 'export PATH=/root/persistent/bin:$PATH' >> ~/.bashrc
```

## Container Registry

Image available at: `ghcr.io/maastrichtu-ids/ubuntu-vnc-desktop:latest`

## Credits

Based on Vincent Emonet's [docker-ubuntu-vnc-desktop](https://github.com/vemonet/docker-ubuntu-vnc-desktop) project.  
Adapted for MRI workflows at Maastricht University - Institute of Data Science.

## License

MIT License - see LICENSE file