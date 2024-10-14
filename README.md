# Docker Installation Issue and Resolution Report

## Issue Overview
After installing Docker on Ubuntu 22.04, the service failed to start with the error:


### Root Cause
The root cause was related to `iptables` using `nftables` by default, which caused Docker's network bridge to fail.

## Steps to Resolve

1. **Switch to `iptables-legacy`**:
    - Run the following commands to switch:
      ```bash
      sudo update-alternatives --set iptables /usr/sbin/iptables-legacy
      sudo update-alternatives --set ip6tables /usr/sbin/ip6tables-legacy
      ```

2. **Flush iptables**:
    ```bash
    sudo iptables -F
    sudo iptables -t nat -F
    ```

3. **Restart Docker**:
    ```bash
    sudo systemctl restart docker
    ```

## Conclusion
After switching to `iptables-legacy` and restarting Docker, the service successfully started and ran Docker containers.

---

**Feel free to clone this repository or contribute your fixes!**

