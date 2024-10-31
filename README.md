# FreePBX-17-Install-Script-Debian12
Automated install guide and script for setting up FreePBX 17 on Debian 12. Installs all dependencies, Sangoma repositories, and optional DAHDI/Wanpipe drivers, creating a scalable, open-source telephony platform ideal for personal and enterprise use.

## FreePBX 17 Installation Guide on Debian 12

This guide will walk you through the complete installation of FreePBX 17 on a Debian 12 system using a dedicated installation script. This script installs all required dependencies and sets up the Sangoma repository for commercial modules.

## Step 1: Prepare the Debian 12 Host

1. **Download and Install Debian 12** on your host or virtual machine, ensuring it has network connectivity.
2. Once installed, **log in to the system** as the `root` user or a user with `sudo` privileges.

## Step 2: Run the FreePBX Installation Script

1. **SSH into the Debian 12 system** as the `root` user.

2. **Navigate to the temporary directory**:
   ```bash
   cd /tmp
   ```

3. **Download the installation script**:
   ```bash
   wget https://github.com/FreePBX/sng_freepbx_debian_install/raw/master/sng_freepbx_debian_install.sh -O /tmp/sng_freepbx_debian_install.sh
   ```

4. **Run the installation script**:
   ```bash
   bash /tmp/sng_freepbx_debian_install.sh
   ```

## Step 3: Monitor the Installation Process

- The script will install all dependencies, set up the Sangoma repository, and configure FreePBX on Debian.
- The installation may take around **30 minutes or more** based on system performance and internet speed.

## Step 4: Check Installation Logs

Logs are available at:
```bash
/var/log/pbx/freepbx17-install-<date-timestamp>.log
```

## Step 5: Optional Arguments for Custom Installation

To customize the installation, you can add optional flags to the script command:

- **DAHDI Support**:
   ```bash
   bash /tmp/sng_freepbx_debian_install.sh --dahdi
   ```
   Use this if you plan to install DAHDI drivers for Sangoma cards, locking the kernel version to avoid updates.

- **Development/Testing Repository**:
   ```bash
   bash /tmp/sng_freepbx_debian_install.sh --testing
   ```

- **Skip FreePBX or Asterisk Installation**:
   ```bash
   bash /tmp/sng_freepbx_debian_install.sh --nofreepbx --noasterisk
   ```

- **Open Source Modules Only**:
   ```bash
   bash /tmp/sng_freepbx_debian_install.sh --opensourceonly
   ```

## Step 6: Checking Kernel Compatibility for DAHDI/Wanpipe Drivers

If you need DAHDI support in the future, ensure the system’s kernel version is compatible.

- **Check the latest DAHDI supported version**:
   ```bash
   apt-cache search dahdi | grep -E "^dahdi-linux-kmod-[0-9]" | awk '{print $1}' | awk -F'-' '{print $4"-"$5}' | sort -n | tail -1
   ```

- **Check the latest Wanpipe supported version**:
   ```bash
   apt-cache search wanpipe | grep -E "^kmod-wanpipe-[0-9]" | awk '{print $1}' | awk -F'-' '{print $3"-"$4}' | sort -n | tail -1
   ```

- **Check current kernel version**:
   ```bash
   apt-cache show linux-headers-$(uname -r) | sed -n -e 's/Package: linux-headers-\([[:digit:].-]*\).*/\1/' -e 's/-\$//p'
   ```

## Final Steps

Once the installation is complete, FreePBX 17 should be ready for use. Access the FreePBX admin interface by opening a web browser and entering the IP address of your server.

--- 

Enjoy using your FreePBX 17 setup!
```
