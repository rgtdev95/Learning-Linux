# Stage 3: The Boot Loader in Action

## 1. The Multi-Stage Boot Challenge

A hard drive's Master Boot Record (MBR) is exactly **512 bytes** in size:
- **446 bytes**: Bootloader code
- **64 bytes**: Partition table (4 entries $\times$ 16 bytes)
- **2 bytes**: Boot signature (`0x55AA`)

Because 446 bytes is far too small to include filesystem drivers (such as ext4, XFS, or Btrfs), network stacks, and interactive graphical menus, traditional bootloaders operate in **multiple sequential stages**.

---

## 2. GRUB 2 Execution Stages

```text
BIOS / MBR System:
┌─────────────────────────────────────────────────────────────┐
│ Stage 1: boot.img (Sector 0 / MBR - 446 bytes)              │
│   └─ Reads sector offset and loads Stage 1.5 into RAM       │
└──────────────────────────────┬──────────────────────────────┘
                               │
                               ▼
┌─────────────────────────────────────────────────────────────┐
│ Stage 1.5: core.img (Stored in MBR gap / Post-MBR sectors)  │
│   └─ Contains basic filesystem drivers (ext4, xfs, btrfs)   │
│   └─ Able to read the Linux filesystem and load Stage 2     │
└──────────────────────────────┬──────────────────────────────┘
                               │
                               ▼
┌─────────────────────────────────────────────────────────────┐
│ Stage 2: /boot/grub2/ (Stored on real disk filesystem)      │
│   └─ Parses /boot/grub2/grub.cfg configuration file         │
│   └─ Displays interactive graphical / text menu             │
│   └─ Loads vmlinuz and initramfs into RAM                   │
└─────────────────────────────────────────────────────────────┘

UEFI / GPT System:
┌─────────────────────────────────────────────────────────────┐
│ UEFI Application: /boot/efi/EFI/<distro>/grubx64.efi        │
│   └─ Single self-contained EFI executable                   │
│   └─ Has built-in filesystem support; directly reads config │
└─────────────────────────────────────────────────────────────┘
```

---

## 3. The Interactive GRUB Menu

At Stage 2, GRUB presents the boot menu to the user:

```text
                             GNU GRUB version 2.06
 ┌───────────────────────────────────────────────────────────────────────────┐
 │*Ubuntu, with Linux 6.8.0-40-generic                                       │
 │ Advanced options for Ubuntu                                               │
 │ Memory test (memtest86+x64.efi)                                           │
 │ UEFI Firmware Settings                                                    │
 └───────────────────────────────────────────────────────────────────────────┘
    Use the ↑ and ↓ keys to select which entry is highlighted.
    Press enter to boot the selected OS, 'e' to edit the commands
    before booting or 'c' for a command-line.
```

### Key Interactive Actions:
- **Pressing `Enter`**: Boots the default highlighted kernel immediately.
- **Pressing `e` (Edit Mode)**: Opens the GRUB parameter editor. This allows system administrators to append temporary kernel parameters:
  - `single` or `1`: Boots into single-user recovery mode.
  - `init=/bin/bash`: Bypasses standard init to spawn an emergency root shell (used for password recovery).
  - `nomodeset`: Disables kernel video mode setting when troubleshooting display driver issues.
  - `quiet splash`: Suppresses detailed boot messages to show a graphical splash screen.

---

## 4. Handoff: Loading the Linux Kernel

Once the user selects a boot entry (or the timeout expires):

1. **Memory Allocation**: GRUB reads the compressed kernel file (`/boot/vmlinuz-<version>`) and the Initial RAM Disk image (`/boot/initramfs-<version>.img`) from disk and copies them into system RAM.
2. **Passing Parameters**: GRUB prepares the kernel command line (e.g., `root=UUID=... ro quiet splash`).
3. **Execution Transfer**: GRUB jumps CPU execution to the memory start address of the kernel and terminates itself.

---

## 5. Kernel Self-Decompression & Hardware Probing

The Linux kernel file is named **`vmlinuz`** (the `z` signifies that it is a compressed executable, historically compressed with gzip/xz/zstd).

```text
[ GRUB Transfers Control to Kernel ]
                 │
                 ▼
[ Kernel Self-Decompression Routine Runs ]
  (Decompresses kernel code from RAM into memory)
                 │
                 ▼
[ Kernel Initializes Core Subsystems ]
  ├── Memory Management (Page tables & virtual memory)
  ├── CPU Scheduler & Multi-core detection
  ├── Built-in Device Drivers
  └── ACPI Power Management
                 │
                 ▼
[ Handoff to Initial RAM Disk (initramfs) ]
```

Once decompressed and initialized, the kernel begins probing for attached hardware devices, preparing for the next challenge: **mounting the root filesystem (`/`)**.