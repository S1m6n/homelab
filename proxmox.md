[Proxmox Virtual Environment]: https://www.proxmox.com/en/products/proxmox-virtual-environment/overview  
[Proxmox repositories]: https://pve.proxmox.com/wiki/Package_Repositories  

# Proxmox Virtual Environment

>[Proxmox Virtual Environment] is a complete, open-source server management platform for enterprise virtualization. It tightly integrates the KVM hypervisor and Linux Containers (LXC), software-defined storage and networking functionality, on a single platform.  


### Proxmox VE Configuration:

After installation, log in to your new PVE host via the web interface and use the Shell.

### System update and configuration of [Proxmox repositories]:

>Configure the repositories, to update the system.

#### Enabling the Proxmox VE No-Subscription Repository:

Edit the file `/etc/apt/sources.list`:
```sh
nano /etc/apt/sources.list
```
Add at the end of the file:
```sh
deb http://download.proxmox.com/debian/pve bookworm pve-no-subscription
```

#### Disabling the official Enterprise Repository:  
Edit the file `/etc/apt/sources.list.d/pve-enterprise.list`:
```sh
nano /etc/apt/sources.list.d/pve-enterprise.list
```
Ensure it looks like this:
```sh
#deb https://enterprise.proxmox.com/debian/pve bookworm pve-enterprise
```

#### Disabling the Ceph Squid Enterprise Repository:  
Edit the file `/etc/apt/sources.list.d/ceph.list`:
```sh
nano /etc/apt/sources.list.d/ceph.list
```
Ensure it looks like this:
```sh
#deb https://enterprise.proxmox.com/debian/ceph-quincy bookworm enterprise
```

System update:
```sh
apt update && apt full-upgrade -y
```

#### Configuring power button behavior:
>Optional step that makes the 'poweroff' command execute when the power button is pressed.

Edit the file `/etc/systemd/logind.conf`:
```sh
nano /etc/systemd/logind.conf
```
Uncomment the line:
```sh
HandlePowerKey=poweroff
```
Save the changes and exit.

Reload the service:
```sh
systemctl restart systemd-logind
```
