# Brave Browser and System Optimization Guide

## 1. Brave Browser Optimizations

### 1.1 Enable Brave Commands in Omnibox
1. Open Brave browser
2. Navigate to `brave://flags`
3. Search for `#brave-commands-omnibox`
4. Set to "Enabled"
5. Restart Brave

### 1.2 Enable Experimental QUIC Protocol
1. Navigate to `brave://flags`
2. Search for `#enable-quic`
3. Set to "Enabled"
4. Restart Brave

### 1.3 Enable Auto Dark Mode for Web Contents
1. Navigate to `brave://flags`
2. Search for `#enable-force-dark`
3. Choose your preferred option (e.g., "Enabled with simple RGB-based inversion")
4. Restart Brave

### 1.4 Change DNS Settings
1. Go to Brave Settings > Privacy and security > Security
2. Scroll down to "Use secure DNS"
3. Select "Google (Public DNS)"

## 2. System-Level Optimizations

### 2.1 Install Preload
```bash
sudo apt-get update
sudo apt-get install preload
sudo systemctl enable preload
sudo systemctl start preload
```

### 2.2 Install and Configure Zram
```bash
sudo apt-get update
sudo apt-get install zram-config

# Edit zram configuration
sudo nano /etc/systemd/zram-generator.conf

# Add the following content:
[zram0]
zram-size = min(ram / 2, 2048)
compression-algorithm = zstd
swap-priority = 100
fs-type = swap

# Save and exit (Ctrl+X, then Y, then Enter)
```

### 2.3 Adjust Swappiness
```bash
echo 'vm.swappiness=80' | sudo tee -a /etc/sysctl.conf
sudo sysctl -p
```

### 2.4 Enable Compressed Transparent Huge Pages
```bash
echo 'GRUB_CMDLINE_LINUX_DEFAULT="$GRUB_CMDLINE_LINUX_DEFAULT transparent_hugepage=madvise"' | sudo tee -a /etc/default/grub
sudo update-grub
```

### 2.5 Apply Changes
```bash
sudo reboot
```

## 3. Additional Brave Optimizations

### 3.1 Enable Hardware Acceleration
1. Go to Settings > Additional settings > System
2. Turn on "Use hardware acceleration when available"

### 3.2 Adjust Content Settings
1. Go to Settings > Additional settings > Privacy and security > Site Settings
2. Disable unnecessary permissions and features

### 3.3 Manage Extensions
1. Go to `brave://extensions/`
2. Disable or remove unused extensions
3. Keep necessary extensions updated

### 3.4 Clear Browsing Data Regularly
1. Go to Settings > Privacy and security > Clear browsing data
2. Select appropriate time range and data types
3. Click "Clear data"

### 3.5 Enable Prefetch
1. Go to Settings > Privacy and security > Security
2. Turn on "Use a prediction service to load pages more quickly"

### 3.6 Optimize Brave Shields
1. Click the Brave icon in the address bar
2. Adjust settings for optimal balance between security and speed

### 3.7 Use Brave Ads (optional)
1. Go to Settings > Brave Rewards
2. Turn on Brave Ads if comfortable

### 3.8 Keep Brave Updated
1. Go to Settings > About Brave
2. Check for updates and install if available

## 4. Verification and Monitoring

### 4.1 Verify Zram Configuration
```bash
cat /proc/swaps
```

### 4.2 Check Swappiness Value
```bash
cat /proc/sys/vm/swappiness
```

### 4.3 Check Transparent Huge Pages Status
```bash
cat /sys/kernel/mm/transparent_hugepage/enabled
```

### 4.4 Monitor System Performance
```bash
sudo apt-get install htop
htop
```

## Notes:
- Always backup important data before making system-level changes.
- Monitor your system's performance after applying these optimizations.
- If you experience any issues, you can revert the changes by removing the added lines from the configuration files.
- Consider using lightweight alternatives for your desktop environment and applications if you're still experiencing slowdowns.
- Regularly clear browser caches and temporary files to manage memory usage.
