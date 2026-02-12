# Ubuntu VNC Desktop

A minimal, stable Ubuntu desktop environment optimized and accessible directly in your browser.

## Based On

This image is based on [vemonet/docker-ubuntu-vnc-desktop](https://github.com/vemonet/docker-ubuntu-vnc-desktop) with modifications for being a more minimal base image.

### Changes from Original

**Removed:**
-  Chrome/Chromium browser
-  FFmpeg and media processing tools
-  Media players (VLC, etc.)
-  ARM architecture support
-  Web development tools
-  Unnecessary desktop applications

**Kept:**
-  Ubuntu 22.04 LTS base
-  LXDE lightweight desktop environment
-  x11vnc + noVNC for browser-based access
-  Supervisor for process management
-  Basic CLI tools
-  Terminal emulator

**Added Dependencies:** Included python3-websockify to ensure the web-to-VNC connection works without needing git.

### Deploy on DSRI OpenShift

Use the template in the [dsri-documentation](https://github.com/MaastrichtU-IDS/dsri-documentation) repository.

### Local Testing
```bash
# Build the image
docker build -t dsri-ubuntu-vnc:test .

# Run locally
docker run -d -p 6080:80 -e PASSWORD=test --name ubuntu-desktop dsri-ubuntu-vnc:tag

# Access in browser: http://localhost:6080

# Cleanup
docker stop ubuntu-desktop  && docker rm ubuntu-desktop 
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

Image available at: 

## Credits

Based on Vincent Emonet's [docker-ubuntu-vnc-desktop](https://github.com/vemonet/docker-ubuntu-vnc-desktop) project.  

## License

MIT License - see LICENSE file