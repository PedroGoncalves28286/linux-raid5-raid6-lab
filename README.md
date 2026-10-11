# Linux Software RAID 5 & RAID 6 — Debian and Rocky Linux

![Topic](https://img.shields.io/badge/Topic-Linux%20Administration-0A66C2) ![Storage](https://img.shields.io/badge/Storage-RAID%205%20%7C%20RAID%206-247A38) ![Tool](https://img.shields.io/badge/Tool-mdadm-orange) ![Type](https://img.shields.io/badge/Type-Hands--on%20Lab-555)

## Overview

This repository documents a hands-on Linux systems administration lab completed during a **Cybersecurity Specialist (CET)** training programme at **CINEL, Lisbon**, on **14 July 2025**.

The practical report covers software RAID configuration, validation and persistent mounting on **Debian** and **Rocky Linux**, using virtual disks in VirtualBox. The original illustrated report is provided in Portuguese.

📄 **[Read the full illustrated lab report (PDF)](Linux_Software_RAID5_RAID6_Debian_RockyLinux_Lab.pdf)**

## Learning objectives

- Create disk partitions with `fdisk` and verify them with `lsblk` and `partprobe`.
- Build **RAID 5** and **RAID 6** arrays with `mdadm`, including spare devices.
- Inspect array health with `/proc/mdstat` and `mdadm --detail`.
- Create **ext3/ext4** filesystems and mount RAID volumes.
- Configure array assembly and persistent mounts using `mdadm.conf`, filesystem UUIDs and `/etc/fstab`.
- Update the initramfs (`update-initramfs` on Debian; `dracut` on Rocky Linux) and validate after reboot.

## Lab environments

| Component | Details |
| --- | --- |
| Hypervisor | Oracle VirtualBox |
| Operating systems | Debian; Rocky Linux |
| RAID utility | `mdadm` |
| RAID 5 | Four active partitions and two spares; ext3; `/mnt/raid` |
| RAID 6 | Six active partitions and two spares; ext4; `/opt/dumdum` |
| Validation | `lsblk`, `blkid`, `/proc/mdstat`, `mdadm --detail`, `mount -a` |

> **Important:** The report records successive lab exercises. Device assignments and the use of `/dev/md0` vary between stages and machines; do not execute all commands sequentially on the same array.

## Representative commands

```bash
# Check block devices and RAID state
lsblk
cat /proc/mdstat
sudo mdadm --detail /dev/md0

# Identify filesystem UUID and check mounted volumes
sudo blkid /dev/md0
findmnt /mnt/raid
findmnt /opt/dumdum

# Validate fstab mounts (after reviewing the file)
sudo mount -a
```

## Repository structure

```text
.
├── README.md
└── Linux_Software_RAID5_RAID6_Debian_RockyLinux_Lab.pdf
```

## Notes and safety

This is a **learning portfolio / lab report**, not a production deployment guide. The report includes an `/etc/fstab` configuration error and its correction as part of the exercise. Some examples are specific to the virtual lab and should be reviewed before reuse. **RAID is not a substitute for backups.** Commands such as `fdisk`, `mdadm --create` and `mkfs` can destroy existing data: run them only on dedicated test devices.

## Author

**Pedro Gonçalves** — Cybersecurity Specialist training project (CINEL, Lisbon).

## Language

The README is in English for international accessibility; the PDF report is in **European Portuguese (pt-PT)**.

## Acknowledgement

Prepared as part of a practical training exercise at CINEL. This repository is a personal learning portfolio and is not an official CINEL publication.
