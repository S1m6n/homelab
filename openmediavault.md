
[openmediavault]: https://www.openmediavault.org  

# Preparing the NAS Server

>[openmediavault] is the next-generation network-attached storage (NAS) solution based on Debian Linux. It is a simple and easy-to-use out-of-the-box solution that allows anyone to install and manage a Network Attached Storage system without requiring deep technical knowledge.

## VM Parameters:
>CPU: 2 vCPU  
RAM: 2048 MB  
Disk: 32 GB

Before installation, I want the VM to have direct access to the SSD. To achieve this, follow these steps:

- Use the Proxmox shell to find the ID of the disk you want to attach to the VM.
```sh
ls -l /dev/disk/by-id/
```
My result:  
`ata-Samsung_SSD_860_PRO_256GB_S42VNF0K933060P`

- Next, edit the configuration file. In my case, the VM has ID 104:
```sh
nano /etc/pve/qemu-server/104.conf
```
And add the following line:
```sh
scsi1: /dev/disk/by-id/ata-Samsung_SSD_860_PRO_256GB_S42VNF0K933060P
```
This will give the VM direct access to the disk.  
![1](Screenshots/openmediavault/1.png)

### Configuring openmediavault via the Web Interface

After logging in, changing the admin password, and performing system updates, I completed the following steps:

- Created user `s1m6n`  
![2](Screenshots/openmediavault/2.PNG)

- Formatted the disk  
![3](Screenshots/openmediavault/3.PNG)  
![4](Screenshots/openmediavault/4.PNG)

- Created the file system  
![5](Screenshots/openmediavault/5.PNG)  
![6](Screenshots/openmediavault/6.PNG)

- Mounted the file system  
![7](Screenshots/openmediavault/7.PNG)  
Result:  
![8](Screenshots/openmediavault/8.PNG)

- Enabled SMB  
![9](Screenshots/openmediavault/9.PNG)

- Created a shared folder  
![10](Screenshots/openmediavault/10.PNG)  
![11](Screenshots/openmediavault/11.PNG)

Thanks to this configuration, the newly created network drive can be mounted using the credentials of the user `s1m6n`.  
![12](Screenshots/openmediavault/12.PNG)  
![13](Screenshots/openmediavault/13.PNG)  
![14](Screenshots/openmediavault/14.PNG)
