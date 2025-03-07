# LPIC-2 Exam 201 Objectives

## Topic 200: Capacity Planning
### 200.1 Measure and Troubleshoot Resource Usage (weight: 6)
#### Description	Candidates should be able to measure hardware resource and network bandwidth, identify and troubleshoot resource problems.
Key Knowledge Areas:

Measure CPU usage.
Measure memory usage.
Measure disk I/O.
Measure network I/O.
Measure firewalling and routing throughput.
Map client bandwidth usage.
Match / correlate system symptoms with likely problems.
Estimate throughput and identify bottlenecks in a system including networking.
The following is a partial list of the used files, terms and utilities:

* [iostat](../TXT%20FILES/iostat.md)

* [iotop](../TXT%20FILES/iotop.md)

* [vmstat](../TXT%20FILES/vmstat.md)

* [netstat](../TXT%20FILES/netstat.md)

* [ss](../TXT%20FILES/ss.md)

* [iptraf]()

* [pstree, ps](../TXT%20FILES/ps.md)

* [w](../TXT%20FILES/w.md)

* [lsof](../TXT%20FILES/lsof.md)

* [top](../TXT%20FILES/top.md)

* [htop](../TXT%20FILES/htop.md)

* [uptime](../TXT%20FILES/uptime.md)

* [sar](../TXT%20FILES/sar.md)

* [swap](../TXT%20FILES/swap.md)

* [processes blocked on I/O](../TXT%20FILES/File-systems-Cocepts/LPIC2-201/processes%20blocked%20on%20IO.md)

* [blocks in](../TXT%20FILES/File-systems-Cocepts/LPIC2-201/blocks%20in.md)

* [blocks out](../TXT%20FILES/File-systems-Cocepts/LPIC2-201/blocks%20out.md)

### 200.2 Predict Future Resource Needs (weight: 2)
#### Description	Candidates should be able to monitor resource usage to predict future resource needs.

Key Knowledge Areas:

Use monitoring and measurement tools to monitor IT infrastructure usage.
Predict capacity break point of a configuration.
Observe growth rate of capacity usage.
Graph the trend of capacity usage.
Awareness of monitoring solutions such as Icinga2, Nagios, collectd, MRTG and Cacti
The following is a partial list of the used files, terms and utilities:

* [diagnose](../TXT%20FILES/File-systems-Cocepts/LPIC2-201/diagnose.md)

* [predict growth](../TXT%20FILES/File-systems-Cocepts/LPIC2-201/predict%20growth.md)

* [resource exhaustion](../TXT%20FILES/File-systems-Cocepts/LPIC2-201/resource%20exhaustion.md)

## Topic 201: Linux Kernel
### 201.1 Kernel components (weight: 2)
#### Description	Candidates should be able to utilise kernel components that are necessary to specific hardware, hardware drivers, system resources and requirements. This objective includes implementing different types of kernel images, understanding stable and longterm kernels and patches, as well as using kernel modules.

Key Knowledge Areas:

Kernel 2.6.x, 3.x and 4.x documentation
The following is a partial list of the used files, terms and utilities:


* [/usr/src/linux/](../TXT%20FILES/File-systems-Cocepts/LPIC2-201/usr-src-linux-.md)

* [/usr/src/linux/Documentation/](../TXT%20FILES/File-systems-Cocepts/LPIC2-201/usr-src-linux-Documentation-.md)

* [zImage](../TXT%20FILES/File-systems-Cocepts/LPIC2-201/zImage.md)

* [bzImage](../TXT%20FILES/File-systems-Cocepts/LPIC2-201/bzImage.md)

* [xz compression](../TXT%20FILES/File-systems-Cocepts/LPIC2-201/xz%20compression.md)
 
### 201.2 Compiling a Linux kernel (weight: 3)
#### Description	Candidates should be able to properly configure a kernel to include or disable specific features of the Linux kernel as necessary. This objective includes compiling and recompiling the Linux kernel as needed, updating and noting changes in a new kernel, creating an initrd image and installing new kernels.

Key Knowledge Areas:

/usr/src/linux/
Kernel Makefiles
Kernel 2.6.x, 3.x and 4.x make targets
Customize the current kernel configuration.
Build a new kernel and appropriate kernel modules.
Install a new kernel and any modules.
Ensure that the boot manager can locate the new kernel and associated files.
Module configuration files
Use DKMS to compile kernel modules.
Awareness of dracut
The following is a partial list of the used files, terms and utilities:

* [mkinitrd](../TXT%20FILES/File-systems-Cocepts/LPIC2-201/mkinitrd.md)

* [mkinitramfs](../TXT%20FILES/File-systems-Cocepts/LPIC2-201/mkinitramfs.md)

* [make](../TXT%20FILES/make.md)

* [make targets (all, config, xconfig, menuconfig, gconfig, oldconfig, mrproper, zImage, bzImage, modules, modules_install, rpm-pkg, binrpm-pkg, deb-pkg)](../TXT%20FILES/File-systems-Cocepts/LPIC2-201/make%20targets.md)

* [gzip](../TXT%20FILES/gzip.md)

* [bzip2](../TXT%20FILES/bzip2.md)

* [module tools](../TXT%20FILES/File-systems-Cocepts/LPIC2-201/module%20tools.md)

* [/usr/src/linux/.config](../TXT%20FILES/File-systems-Cocepts/LPIC2-201/usr-src-linux-.config.md)

* [/lib/modules/kernel-version/]()

* [depmod](../TXT%20FILES/depmod.md)

* [dkms](../TXT%20FILES/File-systems-Cocepts/LPIC2-201/dkms.md)
 
### 201.3 Kernel runtime management and troubleshooting (weight: 4)
#### Description	Candidates should be able to manage and/or query a 2.6.x, 3.x or 4.x kernel and its loadable modules. Candidates should be able to identify and correct common boot and run time issues. Candidates should understand device detection and management using udev. This objective includes troubleshooting udev rules.
Key Knowledge Areas:

Use command-line utilities to get information about the currently running kernel and kernel modules.
Manually load and unload kernel modules.
Determine when modules can be unloaded.
Determine what parameters a module accepts.
Configure the system to load modules by names other than their file name.
/proc filesystem
Content of /, /boot/ , and /lib/modules/
Tools and utilities to analyse information about the available hardware
udev rules
The following is a partial list of the used files, terms and utilities:


* [/lib/modules/kernel-version/modules.dep](../TXT%20FILES/File-systems-Cocepts/LPIC2-201/lib-modules-kernel-version-modules.dep.md)

* [module configuration files in /etc/](../TXT%20FILES/File-systems-Cocepts/LPIC2-201/module%20configuration%20files%20in%20-etc-.md)

* [/proc/sys/kernel/](../TXT%20FILES/File-systems-Cocepts/LPIC2-201/-proc-sys-kernel-.md)

* [/sbin/depmod](../TXT%20FILES/File-systems-Cocepts/LPIC2-201/-sbin-depmod.md)

* [/sbin/rmmod](../TXT%20FILES/File-systems-Cocepts/LPIC2-201/-sbin-rmmod.md)

* [/sbin/modinfo](../TXT%20FILES/File-systems-Cocepts/LPIC2-201/-sbin-modinfo.md)

* [/bin/dmesg](../TXT%20FILES/File-systems-Cocepts/LPIC2-201/-bin-dmesg.md)

* [/sbin/lspci](../TXT%20FILES/File-systems-Cocepts/LPIC2-201/-sbin-lspci.md)

* [/usr/bin/lsdev](../TXT%20FILES/File-systems-Cocepts/LPIC2-201/-usr-bin-lsdev.md)

* [/sbin/lsmod](../TXT%20FILES/File-systems-Cocepts/LPIC2-201/-sbin-lsmod.md)

* [/sbin/modprobe](../TXT%20FILES/File-systems-Cocepts/LPIC2-201/-sbin-modprobe.md)

* [/sbin/insmod](../TXT%20FILES/File-systems-Cocepts/LPIC2-201/-sbin-insmod.md)

* [/bin/uname](../TXT%20FILES/File-systems-Cocepts/LPIC2-201/-bin-uname.md)

* [/usr/bin/lsusb](../TXT%20FILES/File-systems-Cocepts/LPIC2-201/-usr-bin-lsusb.md)

* [/etc/sysctl.conf, /etc/sysctl.d/](../TXT%20FILES/File-systems-Cocepts/LPIC2-201/-etc-sysctl.conf%2C%20-etc-sysctl.d-.md)

* [/sbin/sysctl](../TXT%20FILES/File-systems-Cocepts/LPIC2-201/sysctl.md)

* [udevmonitor](../TXT%20FILES/File-systems-Cocepts/LPIC2-201/udevmonitor.md)

* [udevadm monitor](../TXT%20FILES/File-systems-Cocepts/LPIC2-201/udevadm%20monitor.md)

* [/etc/udev/](../TXT%20FILES/File-systems-Cocepts/LPIC2-201/-etc-udev.md)
 
## Topic 202: System Startup
### 202.1 Customising system startup (weight: 3)
#### Description	Candidates should be able to query and modify the behaviour of system services at various targets / run levels. A thorough understanding of the systemd, SysV Init and the Linux boot process is required. This objective includes interacting with systemd targets and SysV init run levels.

Key Knowledge Areas:

Systemd
SysV init
Linux Standard Base Specification (LSB)
The following is a partial list of the used files, terms and utilities:


* [/usr/lib/systemd/](../TXT%20FILES/File-systems-Cocepts/LPIC2-201/usr-lib-systemd-.md)

* [/etc/systemd/](../TXT%20FILES/File-systems-Cocepts/LPIC2-201/-etc-systemd-.md)

* [/run/systemd/](../TXT%20FILES/File-systems-Cocepts/LPIC2-201/-run-systemd-.md)

* [systemctl](../TXT%20FILES/systemctl.md)

* [systemd-delta](../TXT%20FILES/File-systems-Cocepts/LPIC2-201/systemd-delta.md)

* [/etc/inittab](../TXT%20FILES/File-systems-Cocepts/LPIC2-201/-etc-inittab-.md)

* [/etc/init.d/](../TXT%20FILES/File-systems-Cocepts/LPIC2-201/-etc-init.d-.md)

* [/etc/rc.d/](../TXT%20FILES/File-systems-Cocepts/LPIC2-201/-etc-rc.d-.md)

* [chkconfig](../TXT%20FILES/chkconfig.md)

* [update-rc.d](../TXT%20FILES/File-systems-Cocepts/LPIC2-201/update-rc.d.md)

* [init and telinit](../TXT%20FILES/init.md)
 
### 202.2 System recovery (weight: 4)
#### Description	Candidates should be able to properly manipulate a Linux system during both the boot process and during recovery mode. This objective includes using both the init utility and init-related kernel options. Candidates should be able to determine the cause of errors in loading and usage of bootloaders. GRUB version 2 and GRUB Legacy are the bootloaders of interest. Both BIOS and UEFI systems are covered.
Key Knowledge Areas:

BIOS and UEFI
NVMe booting
GRUB version 2 and Legacy
grub shell
boot loader start and hand off to kernel
kernel loading
hardware initialisation and setup
daemon/service initialisation and setup
Know the different boot loader install locations on a hard disk or removable device.
Overwrite standard boot loader options and using boot loader shells.
Use systemd rescue and emergency modes.
The following is a partial list of the used files, terms and utilities:


* [mount](../TXT%20FILES/mount.md)

* [fsck](../TXT%20FILES/fsck.md)

* [inittab, telinit and init with SysV init](../TXT%20FILES/File-systems-Cocepts/LPIC2-201/inittab%2C%20telinit%20and%20init%20with%20SysV%20init.md)

* [The contents of /boot/, /boot/grub/ and /boot/efi/](../TXT%20FILES/File-systems-Cocepts/LPIC2-201/The%20contents%20of%20-boot-%2C%20-boot-grub-%20and%20-boot-efi-.md)

* [EFI System Partition (ESP)](../TXT%20FILES/File-systems-Cocepts/LPIC2-201/EFI%20System%20Partition%20(ESP).md)

* [GRUB](../TXT%20FILES/File-systems-Cocepts/LPIC2-201/GRUB.md)

* [grub-install](../TXT%20FILES/File-systems-Cocepts/LPIC2-201/grub-install.md)

* [efibootmgr](../TXT%20FILES/File-systems-Cocepts/LPIC2-201/efibootmgr.md)

* [UEFI shell](../TXT%20FILES/File-systems-Cocepts/LPIC2-201/UEFI%20shell.md)

* [initrd, initramfs](../TXT%20FILES/File-systems-Cocepts/LPIC2-201/initrd%2C%20initramfs.md)

* [Master boot record](../TXT%20FILES/File-systems-Cocepts/LPIC2-201/Master%20boot%20record.md)

* [systemctl](../TXT%20FILES/systemctl.md)
 
### 202.3 Alternate Bootloaders (weight: 2)
#### Description	Candidates should be aware of other bootloaders and their major features.
Key Knowledge Areas:

SYSLINUX, ISOLINUX, PXELINUX
Understanding of PXE for both BIOS and UEFI
Awareness of systemd-boot and U-Boot
The following is a partial list of the used files, terms and utilities:


* [syslinux](../TXT%20FILES/File-systems-Cocepts/LPIC2-201/syslinux.md)

* [extlinux](../TXT%20FILES/File-systems-Cocepts/LPIC2-201/extlinux.md)

* [isolinux.bin](../TXT%20FILES/File-systems-Cocepts/LPIC2-201/isolinux.bin.md)

* [isolinux.cfg](../TXT%20FILES/File-systems-Cocepts/LPIC2-201/isolinux.cfg.mdv)

* [isohdpfx.bin](../TXT%20FILES/File-systems-Cocepts/LPIC2-201/isohdpfx.bin.md)

* [efiboot.img](../TXT%20FILES/File-systems-Cocepts/LPIC2-201/efiboot.img.md)

* [pxelinux.0](../TXT%20FILES/File-systems-Cocepts/LPIC2-201/pxelinux.0.md)

* [pxelinux.cfg/](../TXT%20FILES/File-systems-Cocepts/LPIC2-201/pxelinux.cfg-.md)

* [uefi/shim.efi](../TXT%20FILES/File-systems-Cocepts/LPIC2-201/uefi-shim.efi.md)

* [uefi/grubx64.efi](../TXT%20FILES/File-systems-Cocepts/LPIC2-201/uefi-grubx64.efi.md)
 
## Topic 203: Filesystem and Devices
### 203.1 Operating the Linux filesystem (weight: 4)
#### Description	Candidates should be able to properly configure and navigate the standard Linux filesystem. This objective includes configuring and mounting various filesystem types.

Key Knowledge Areas:

The concept of the fstab configuration
Tools and utilities for handling swap partitions and files
Use of UUIDs for identifying and mounting file systems
Understanding of systemd mount units
The following is a partial list of the used files, terms and utilities:


* [/etc/fstab](../TXT%20FILES/File-systems-Cocepts/LPIC1-101/-etc-fstab.md)

* [/etc/mtab](../TXT%20FILES/File-systems-Cocepts/LPIC2-201/-etc-mtab.md)

* [/proc/mounts](../TXT%20FILES/File-systems-Cocepts/LPIC2-201/-proc-mounts.mdv)

* [mount and umount](../TXT%20FILES/File-systems-Cocepts/LPIC2-201/mount%20and%20umount.md)

* [blkid](../TXT%20FILES/File-systems-Cocepts/LPIC2-201/blkid.md)

* [sync](../TXT%20FILES/File-systems-Cocepts/LPIC2-201/sync.md)

* [swapon](../TXT%20FILES/swapon.md)

* [swapoff](../TXT%20FILES/swapoff.md)

### 203.2 Maintaining a Linux filesystem (weight: 3)
#### Description	Candidates should be able to properly maintain a Linux filesystem using system utilities. This objective includes manipulating standard filesystems and monitoring SMART devices.

Key Knowledge Areas:

Tools and utilities to manipulate and ext2, ext3 and ext4
Tools and utilities to perform basic Btrfs operations, including subvolumes and snapshots
Tools and utilities to manipulate XFS
Awareness of ZFS
The following is a partial list of the used files, terms and utilities:

* [mkfs (mkfs.*)](../TXT%20FILES/File-systems-Cocepts/LPIC2-201/mkfs%20(mkfs.).md)

* [mkswap](../TXT%20FILES/File-systems-Cocepts/LPIC2-201/mkswap.md)

* [fsck (fsck.*)](../TXT%20FILES/File-systems-Cocepts/LPIC2-201/fsck%20(fsck.).md)

* [tune2fs, dumpe2fs and debugfs](../TXT%20FILES/File-systems-Cocepts/LPIC2-201/tune2fs.md)

* [btrfs, btrfs-convert](../TXT%20FILES/File-systems-Cocepts/LPIC2-201/btrfs%2C%20btrfs-convert.md)

* [xfs_info, xfs_check, xfs_repair, xfsdump and xfsrestore](../TXT%20FILES/File-systems-Cocepts/LPIC2-201/xfs_info%2C%20xfs_check%2C%20xfs_repair%2C%20xfsdump%20and%20xfsrestore.md)

* [smartd, smartctl](../TXT%20FILES/File-systems-Cocepts/LPIC2-201/smartd%2C%20smartctl.md)

### 203.3 Creating and configuring filesystem options (weight: 2)
#### Description	Candidates should be able to configure automount filesystems using AutoFS. This objective includes configuring automount for network and device filesystems. Also included is creating filesystems for devices such as CD-ROMs and a basic feature knowledge of encrypted filesystems.

Key Knowledge Areas:

autofs configuration files
Understanding of automount units
UDF and ISO9660 tools and utilities
Awareness of other CD-ROM filesystems (HFS)
Awareness of CD-ROM filesystem extensions (Joliet, Rock Ridge, El Torito)
Basic feature knowledge of data encryption (dm-crypt / LUKS)
The following is a partial list of the used files, terms and utilities:

* [/etc/auto.master](../TXT%20FILES/File-systems-Cocepts/LPIC2-201/-etc-auto.master.md)

* [/etc/auto(dir)](../TXT%20FILES/File-systems-Cocepts/LPIC2-201/-etc-auto.%5Bdir%5D.md)

* [mkisofs](../TXT%20FILES/File-systems-Cocepts/LPIC2-201/mkisofs.md)

* [cryptsetup](../TXT%20FILES/File-systems-Cocepts/LPIC2-201/cryptsetup.md)

## Topic 204: Advanced Storage Device Administration
### 204.1 Configuring RAID (weight: 3)
#### Description	Candidates should be able to configure and implement software RAID. This objective includes using and configuring RAID 0, 1 and 5.

Key Knowledge Areas:

Software RAID configuration files and utilities
The following is a partial list of the used files, terms and utilities:


* [mdadm.conf](../TXT%20FILES/File-systems-Cocepts/LPIC2-201/mdadm.conf.md)

* [mdadm](../TXT%20FILES/File-systems-Cocepts/LPIC2-201/mdadm.md)

* [/proc/mdstat](../TXT%20FILES/File-systems-Cocepts/LPIC2-201/-proc-mdstat.md)

* [partition type 0xFD](../TXT%20FILES/File-systems-Cocepts/LPIC2-201/partition%20type%200xFD.md)

### 204.2 Adjusting Storage Device Access (weight: 2)
#### Description	Candidates should be able to configure kernel options to support various drives. This objective includes software tools to view & modify hard disk settings including iSCSI devices.

Key Knowledge Areas:

Tools and utilities to configure DMA for IDE devices including ATAPI and SATA
Tools and utilities to configure Solid State Drives including AHCI and NVMe
Tools and utilities to manipulate or analyse system resources (e.g. interrupts)
Awareness of sdparm command and its uses
Tools and utilities for iSCSI
Awareness of SAN, including relevant protocols (AoE, FCoE)
The following is a partial list of the used files, terms and utilities:


* [hdparm, sdparm](../TXT%20FILES/hdparm.md)

* [nvme](../TXT%20FILES/File-systems-Cocepts/LPIC2-201/nvme.md)

* [tune2fs](../TXT%20FILES/tune2fs.md)

* [fstrim](../TXT%20FILES/File-systems-Cocepts/LPIC2-201/fstrim.md)

* [sysctl](../TXT%20FILES/sysctl.md)

* [/dev/hd*, /dev/sd*, /dev/nvme*](../TXT%20FILES/File-systems-Cocepts/LPIC2-201/-dev-hd%2C%20-dev-sd%2C%20-dev-nvme.md)

* [iscsiadm, scsi_id, iscsid and iscsid.conf](../TXT%20FILES/File-systems-Cocepts/LPIC2-201/iscsiadm%2C%20scsi_id%2C%20iscsid%20and%20iscsid.conf.md)

* [WWID, WWN, LUN numbers](../TXT%20FILES/File-systems-Cocepts/LPIC2-201/WWID%2C%20WWN%2C%20LUN%20numbers.md)

### 204.3 Logical Volume Manager (weight: 3)
#### Description	Candidates should be able to create and remove logical volumes, volume groups, and physical volumes. This objective includes snapshots and resizing logical volumes.

Key Knowledge Areas:

Tools in the LVM suite
Resizing, renaming, creating, and removing logical volumes, volume groups, and physical volumes
Creating and maintaining snapshots
Activating volume groups
The following is a partial list of the used files, terms and utilities:


* [/sbin/pv*](../TXT%20FILES/File-systems-Cocepts/LPIC2-201/-sbin-pv.md)

* [/sbin/lv*](../TXT%20FILES/File-systems-Cocepts/LPIC2-201/-sbin-lv.md)

* [/sbin/vg*](../TXT%20FILES/File-systems-Cocepts/LPIC2-201/-sbin-vg.md)

* [mount](../TXT%20FILES/mount.md)

* [/dev/mapper/](../TXT%20FILES/File-systems-Cocepts/LPIC2-201/-dev-mapper-.md)

* [lvm.conf](../TXT%20FILES/File-systems-Cocepts/LPIC2-201/lvm.conf.md) 

## Topic 205: Networking Configuration
### 205.1 Basic networking configuration (weight: 3)
#### Description	Candidates should be able to configure a network device to be able to connect to a local, wired or wireless, and a wide-area network. This objective includes being able to communicate between various subnets within a single network including both IPv4 and IPv6 networks.

Key Knowledge Areas:

Utilities to configure and manipulate ethernet network interfaces
Configuring basic access to wireless networks
The following is a partial list of the used files, terms and utilities:


* [ip](../TXT%20FILES/ip.md)

* [ifconfig](../TXT%20FILES/ifconfig.md)

* [route](../TXT%20FILES/route.md)

* [arp](../TXT%20FILES/arp.md)

* [iw](../TXT%20FILES/File-systems-Cocepts/LPIC2-201/iw.md)

* [iwconfig](../TXT%20FILES/iwconfig.md)

* [iwlist](../TXT%20FILES/File-systems-Cocepts/LPIC2-201/iwlist.md)

### 205.2 Advanced Network Configuration (weight: 4)
#### Description	Candidates should be able to configure a network device to implement various network authentication schemes. This objective includes configuring a multi-homed network device and resolving communication problems.
Key Knowledge Areas:

Utilities to manipulate routing tables
Utilities to configure and manipulate ethernet network interfaces
Utilities to analyse the status of the network devices
Utilities to monitor and analyse the TCP/IP traffic
The following is a partial list of the used files, terms and utilities:

* [ip](../TXT%20FILES/ip.md)

* [ifconfig](../TXT%20FILES/ifconfig.md)

* [route](../TXT%20FILES/route.md)

* [arp](../TXT%20FILES/arp.md)

* [ss](../TXT%20FILES/ss.md)

* [netstat](../TXT%20FILES/netstat.md)

* [lsof](../TXT%20FILES/lsof.md)

* [ping, ping6](../TXT%20FILES/File-systems-Cocepts/LPIC2-201/ping%2C%20ping6.md)

* [nc](../TXT%20FILES/File-systems-Cocepts/LPIC2-201/nc.md)

* [tcpdump](../TXT%20FILES/tcpdump.md)

* [nmap](../TXT%20FILES/File-systems-Cocepts/LPIC2-201/nmap.md)

### 205.3 Troubleshooting network issues (weight: 4)
#### Description	Candidates should be able to identify and correct common network setup issues, to include knowledge of locations for basic configuration files and commands.

Key Knowledge Areas:

Location and content of access restriction files
Utilities to configure and manipulate ethernet network interfaces
Utilities to manage routing tables
Utilities to list network states.
Utilities to gain information about the network configuration
Methods of information about the recognised and used hardware devices
System initialisation files and their contents (Systemd and SysV init)
Awareness of NetworkManager and its impact on network configuration
The following is a partial list of the used files, terms and utilities:

* [ip](../TXT%20FILES/ip.md)

* [ifconfig](../TXT%20FILES/ifconfig.md)

* [route](../TXT%20FILES/route.md)

* [ss](../TXT%20FILES/ss.md)

* [netstat](../TXT%20FILES/netstat.md)

* [/etc/network/, /etc/sysconfig/network-scripts/](../TXT%20FILES/File-systems-Cocepts/LPIC2-201/-etc-network%2C%20-etc-sysconfig-network-scripts-.md)

* [ping, ping6](../TXT%20FILES/ping.md)

* [traceroute, traceroute6](../TXT%20FILES/traceroute.md)

* [mtr](../TXT%20FILES/File-systems-Cocepts/LPIC2-201/mtr.md)

* [hostname](../TXT%20FILES/hostname.md)

* [System log files such as /var/log/syslog, /var/log/messages and the systemd journal]()

* [dmesg](../TXT%20FILES/dmesg.md)

* [/etc/resolv.conf](../TXT%20FILES/File-systems-Cocepts/LPIC2-201/-etc-resolv.conf.md)

* [/etc/hosts](../TXT%20FILES/File-systems-Cocepts/LPIC2-201/-etc-hosts.md)

* [/etc/hostname, /etc/HOSTNAME](../TXT%20FILES/File-systems-Cocepts/LPIC2-201/-etc-hostname%2C%20-etc-HOSTNAME.md)

* [/etc/hosts.allow, /etc/hosts.deny](../TXT%20FILES/File-systems-Cocepts/LPIC2-201/-etc-hosts.allow%2C%20-etc-hosts.deny.md)

## Topic 206: System Maintenance
### 206.1 Make and install programs from source (weight: 2)
#### Description	Candidates should be able to build and install an executable program from source. This objective includes being able to unpack a file of sources.

Key Knowledge Areas:

Unpack source code using common compression and archive utilities.
Understand basics of invoking make to compile programs.
Apply parameters to a configure script.
Know where sources are stored by default.
The following is a partial list of the used files, terms and utilities:


* [/usr/src/](../TXT%20FILES/File-systems-Cocepts/LPIC2-201/-usr-src-.md)

* [gunzip](../TXT%20FILES/gunzip.md)

* [gzip](../TXT%20FILES/gzip.md)

* [bzip2](../TXT%20FILES/bzip2.md)

* [xz](../TXT%20FILES/xz.md)

* [tar](../TXT%20FILES/tar.md)

* [configure](../TXT%20FILES/File-systems-Cocepts/LPIC2-201/configure.md)

* [make](../TXT%20FILES/make.md)

* [uname](../TXT%20FILES/uname.md)

* [install](../TXT%20FILES/install.md)

* [patch](../TXT%20FILES/patch.md)

### 206.2 Backup operations (weight: 3)
#### Description	Candidates should be able to use system tools to back up important system data.
Key Knowledge Areas:

Knowledge about directories that have to be included in backups
