# Stage 1: BIOS & UEFI – The First Steps

## 1. System Power-On & Firmware Initialization

Although Linux runs on virtually every computer architecture (ARM, RISC-V, POWER, s390x, MIPS), standard desktop, laptop, and enterprise cloud servers predominantly use the **x86 / x86_64 architecture**.

When you press the computer's power button, the CPU has no operating system loaded in RAM. The motherboard triggers the system firmware—traditionally the **BIOS (Basic Input/Output System)** or modern **UEFI (Unified Extensible Firmware Interface)**.

```text
[ Power Button Pressed ]
           │
           ▼
[ CPU Jumps to Reset Vector ]
           │
           ▼
[ Firmware Executes from Motherboard ROM / Flash ]
  (BIOS or UEFI)
           │
           ▼
[ Power-On Self-Test (POST) ]
  ├── Initialize CPU registers & clock
  ├── Test & verify system RAM (Memory Check)
  ├── Initialize basic video display & keyboard
  └── Probe storage buses (NVMe, SATA, USB, PCIe)
           │
           ▼
[ Read CMOS / NVRAM Settings ]
  (Check boot device order, RTC date/time)
           │
           ▼
[ Locate & Launch Bootloader ]
  (From MBR Sector 0 or EFI System Partition)
```

---

## 2. What is the BIOS?

- **Definition**: **BIOS (Basic Input/Output System)** is firmware stored in a non-volatile Read-Only Memory (ROM) or Flash memory chip on the motherboard.
- **Role**: It is the very first program executed by the CPU upon startup.
- **Function**: Bridges basic hardware and software before any operating system is loaded.

---

## 3. The Power-On Self-Test (POST)

Immediately after power is stabilized, the firmware conducts a critical hardware diagnostic routine known as **POST (Power-On Self-Test)**:

1. **Hardware Verification**:
   - Checks the CPU, initializes system buses, and performs read/write checks across system RAM.
   - Detects connected input devices (keyboard, mouse) and basic video output (enabling screen display).
2. **Device Discovery**:
   - Scans internal storage controllers (NVMe drives, SATA SSDs/HDDs, RAID cards) and external ports (USB, optical drives, network cards).
3. **Error Reporting**:
   - If critical hardware is missing or malfunctioning (e.g., failed RAM or no GPU detected), POST halts and reports the issue via motherboard beep codes, diagnostic LED codes, or on-screen messages.

---

## 4. CMOS & NVRAM Configuration

After completing POST, the firmware reads hardware configurations stored in **CMOS** (or NVRAM in UEFI systems):
- **Real-Time Clock (RTC)**: Retains system date and time via a small coin-cell battery (CR2032).
- **Boot Priority Order**: Specifies the device sequence to check for a valid bootloader:
  ```text
  Boot Device Order:
  1. NVMe SSD (e.g., Samsung 990 PRO)
  2. Removable USB Drive
  3. Optical Drive (CD/DVD)
  4. Network Boot (PXE)
  ```

---

## 5. Handing Control to the Bootloader

Once the firmware identifies the primary bootable storage device:
- **On Legacy BIOS**: It reads the first 512-byte sector of the hard disk (**Master Boot Record / MBR**) into RAM at physical memory address `0x7C00` and transfers execution to it.
- **On Modern UEFI**: It loads a dedicated EFI bootloader executable (`.efi` file) from the **EFI System Partition (ESP)** into memory.

This marks the end of firmware execution and the start of the **Bootloader Stage**.