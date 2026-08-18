# Stage 2: MBR, UEFI & Bootloader Fundamentals

## 1. What is a Bootloader?

A **bootloader** is a specialized software program stored on a storage device (SSD, NVMe, HDD, USB) whose primary responsibility is to **load the operating system kernel and its initial RAM disk into memory and transfer CPU execution to it**.

```text
+---------------------+           +------------------------+           +---------------+
| System Firmware     | ========> | Bootloader             | ========> | Linux Kernel  |
| (Legacy BIOS / UEFI)|           | (GRUB 2 / systemd-boot)|           | (vmlinuz)     |
+---------------------+           +------------------------+           +---------------+
```

---

## 2. Common Linux Bootloaders

| Bootloader | Full Name | Primary Use Case |
| :--- | :--- | :--- |
| **GRUB 2** | **GRand Unified Bootloader** (v2) | The universal standard bootloader across mainstream distributions (Ubuntu, Fedora, Debian, RHEL, openSUSE, Arch). Supports multiboot, scriptable menus, and dynamic module loading. |
| **systemd-boot** | (Formerly Gummiboot) | A minimal, fast, text-only UEFI boot manager popular on Arch Linux and modern UEFI systems. |
| **ISOLINUX / SYSLINUX** | SYSLINUX Project | Designed specifically for booting from removable media, Live USBs, and ISO installation images. |
| **DAS U-Boot** | Universal Boot Loader | The industry standard bootloader for embedded Linux devices, Single Board Computers (Raspberry Pi, BeagleBone), and IoT appliances. |

---

## 3. Legacy BIOS/MBR vs. Modern UEFI/GPT

Modern computing has shifted from legacy BIOS with MBR partitioning to UEFI with GPT partitioning.

```text
  LEGACY BIOS / MBR PATH                    MODERN UEFI / GPT PATH
+-------------------------+               +-------------------------+
|      Legacy BIOS        |               |      UEFI Firmware      |
+------------┬------------+               +------------┬------------+
             │                                         │
             ▼                                         ▼
+-------------------------+               +-------------------------+
|   Master Boot Record    |               |  EFI System Partition   |
| (First 512-byte Sector) |               |  (ESP - FAT32 formatted)|
+------------┬------------+               +------------┬------------+
             │                                         │
             ▼                                         ▼
+-------------------------+               +-------------------------+
|   GRUB Stage 1 / 1.5    |               |  grubx64.efi Binary     |
+------------┬------------+               +------------┬------------+
             │                                         │
             ▼                                         ▼
+-------------------------+               +-------------------------+
|  GRUB Stage 2 (/boot)   |               |  GRUB Menu / Config     |
+------------┬------------+               +------------┬------------+
             │                                         │
             ▼                                         ▼
+-------------------------+               +-------------------------+
|   Linux Kernel & Init   |               |   Linux Kernel & Init   |
+-------------------------+               +-------------------------+
```

---

## 4. BIOS/MBR vs. UEFI/GPT Detailed Comparison

| Feature | Legacy BIOS + MBR | Modern UEFI + GPT |
| :--- | :--- | :--- |
| **Partition Table** | **MBR** (Master Boot Record) | **GPT** (GUID Partition Table) |
| **Max Disk Size** | **2 Terabytes (2 TB)** limit | **9.4 Zettabytes (9.4 ZB)** |
| **Partition Limit** | 4 Primary partitions (or 3 Primary + Extended) | Up to **128 partitions** (standard) |
| **Bootloader Location** | Sector 0 of disk (only 446 bytes available for code) | File on FAT32 partition (`/boot/efi/EFI/<distro>/`) |
| **Processor Mode** | Runs in **16-bit Real Mode** | Runs in **32-bit or 64-bit Protected Mode** |
| **Security** | None (Vulnerable to boot sector rootkits) | **Secure Boot** (cryptographic signature verification) |
| **Configuration** | Static sector pointers | Boot entries stored in motherboard NVRAM |

---

## 5. The Role of the Boot Menu

When the bootloader initializes, it provides an interactive menu (or splash screen) allowing you to:
1. **Choose an Operating System**: Dual-booting Linux alongside Windows or another Linux distribution.
2. **Select a Kernel Version**: Boot into an older, stable kernel if a newly upgraded kernel causes driver regressions.
3. **Recovery / Rescue Mode**: Boot into maintenance targets to repair filesystems or reset forgotten root passwords.
4. **Pass Kernel Parameters**: Modify boot behavior dynamically (e.g., adding `nomodeset` for GPU troubleshooting or `init=/bin/bash`).

Once a selection is confirmed, the bootloader loads **two critical files** into system RAM:
- The **Linux Kernel image** (`vmlinuz`)
- The **Initial RAM Disk** (`initramfs` or `initrd`)