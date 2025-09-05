# Linux System Administration - Essential Tasks

## Project Overview
This project demonstrates proficiency in Linux system administration by setting up and managing a Linux environment with essential configurations. It includes disk management, Logical Volume Management (LVM), user management, networking configurations, and file permissions.

## Author
Divya M

## Objectives
- Implement disk mounting and LVM for efficient storage management
- Manage users and permissions to ensure security
- Configure network settings for seamless connectivity
- Use key Linux commands for troubleshooting and performance monitoring

## Table of Contents
1. [Introduction](#introduction)
2. [Disk Mounting and Management](#disk-mounting-and-management)
3. [Logical Volume Management (LVM)](#logical-volume-management-lvm)
4. [File Permissions and Management](#file-permissions-and-management)
5. [Disk Management](#disk-management)
6. [Networking Commands](#networking-commands)
7. [User Management](#user-management)
8. [Conclusion](#conclusion)

## Introduction
Linux system administration is a crucial skill for managing servers and IT infrastructure. This project demonstrates essential Linux administration tasks, including disk mounting, LVM, file permissions, disk management, networking commands, and user management.

1. Disk Mounting and Management

 Objective
Learn how to mount and manage storage devices in Linux.

**Key Steps:**
1.  Identified available disks using `lsblk` and `fdisk -l`.
2.  Created a new partition on `/dev/xvdx` using `fdisk`.
3.  Formatted the partition with the `ext4` filesystem using `mkfs.ext4 /dev/xvdx1`.
4.  Created a mount point: `mkdir /mnt`.
5.  Mounted the partition temporarily: `mount /dev/xvdx1 /mnt`.
6.  Made the mount persistent by adding an entry to `/etc/fstab`.

Commands:
lsblk
fdisk -l
fdisk /dev/xvdx
mkfs.ext4 /dev/xvdx1
mkdir /mnt
mount /dev/xvdx1 /mnt
echo "/dev/xvdx1 /mnt ext4 defaults 0 0" >> /etc/fstab

2. Logical Volume Management (LVM)

Objective: Create and manage flexible storage using LVM.

Key Steps:
Created a Physical Volume (PV): pvcreate /dev/xvdx1

Created a Volume Group (VG): vgcreate divya_vg /dev/xvdx1

Created a Logical Volume (LV): lvcreate -L 1G -n divya_lv divya_vg

Formatted the LV: mkfs.ext4 /dev/divya_vg/divya_lv

Mounted the LV: mount /dev/divya_vg/divya_lv /mnt

Extended the LV by 2GB: lvextend -L +2G /dev/divya_vg/divya_lv

Made the LV mount persistent via /etc/fstab.

Commands:
pvcreate /dev/xvdx1
vgcreate divya_vg /dev/xvdx1
lvcreate -L 1G -n divya_lv divya_vg
mkfs.ext4 /dev/divya_vg/divya_lv
mount /dev/divya_vg/divya_lv /mnt
lvextend -L +2G /dev/divya_vg/divya_lv
# Add to /etc/fstab: /dev/divya_vg/divya_lv /mnt ext4 defaults 0 0

3. File Permissions and Management

Objective: Understand and manage Linux file permissions and ownership.

Key Concepts:
Permission Classes: User (u), Group (g), Others (o)

Permission Types: Read (r=4), Write (w=2), Execute (x=1)

Special Permissions: SUID, SGID, Sticky Bit

Tasks Performed:

Viewed permissions: ls -l

Modified permissions using symbolic (chmod u+x) and numeric (chmod 755) modes.

Changed file ownership: chown user:group filename

Applied special permissions:

SUID: chmod u+s file (Runs as file owner)

SGID: chmod g+s directory (New files inherit group)

Sticky Bit: chmod +t directory (Only owner can delete)

Commands:
ls -l
chmod 755 file
chmod u+x script.sh
chown divya:developers data.txt
chmod u+s /usr/bin/special_program
chmod g+s /shared_directory
chmod +t /tmp

4. Disk Management and Monitoring

Objective: Monitor disk usage, health, and I/O performance.

Tasks Performed:

Checked disk space: df -h

Checked inode usage: df -i

Checked directory size: du -sh /path/to/dir

Formatted a partition: mkfs.ext4 /dev/xvdx2

Monitored disk health: smartctl -a /dev/xvdx

Monitored I/O performance with iostat and iotop

Commands:
df -h
df -i
du -sh /home
sudo mkfs.ext4 /dev/xvdx2
sudo apt install smartmontools
sudo smartctl -a /dev/xvdx
sudo apt install sysstat iotop
iostat -x 1
sudo iotop

5. Networking Configuration

Objective: Configure and troubleshoot network settings.

Tasks Performed:

Checked IP configuration: ip addr

Tested network connectivity: ping google.com -c 4

Installed and used ifconfig from the net-tools package.

Viewed the routing table: route -n or ip route show

Commands:
ip addr
ping google.com -c 4
sudo apt update && sudo apt install net-tools
ifconfig
route -n

6. User Management

Objective: Manage user and group accounts.

Tasks Performed:

Added a new user with a custom UID and home directory: useradd -u 30001 -c "testuser" -d /home/app -s /bin/bash app

Set a user password: passwd app

Modified user comment: usermod -c "hello world" app

Created a group: groupadd webapp

Added a user to a group: usermod -aG webapp app

Deleted a user and their home directory: userdel -r app

Commands:
useradd -u 30001 -c "testuser" -d /home/app -s /bin/bash app
passwd app
id app
usermod -c "hello world" app
groupadd webapp
usermod -aG webapp app
userdel -r app
📸 Screenshots
Screenshots for each major step are available in the media/ directory, demonstrating the successful execution of all commands and configurations.

✅ Conclusion
This project successfully demonstrates a wide range of essential Linux system administration skills. By completing these tasks, I have gained practical, hands-on experience in configuring, managing, and troubleshooting a Linux environment, forming a solid foundation for managing production servers and IT infrastructure.