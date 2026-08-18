# The Linux Kernel: Architecture & Early Initialization

## 1. The Kernel Takes Control

Once the bootloader (such as GRUB 2) places the compressed kernel image (`vmlinuz`) and the Initial RAM Disk (`initramfs`) into system RAM, it transfers CPU execution to the kernel's decompression routine.

As the central core of the operating system, the **Linux Kernel** immediately takes ownership of the hardware, transitioning the machine from a raw firmware state into a managed computing platform.

```text
+-------------------------------------------------------------------------+
|                  EARLY KERNEL INITIALIZATION SEQUENCE                   |
+-------------------------------------------------------------------------+
|                                                                         |
|  [ Bootloader Loads vmlinuz + initramfs into RAM ]                      |
|                                │                                        |
|                                ▼                                        |
|  [ Kernel Self-Decompression ]                                          |
|    └─ Extracts compiled kernel code into executable memory space        |
|                                │                                        |
|                                ▼                                        |
|  [ start_kernel() Entry Point (init/main.c) ]                           |
|    ├── Memory Setup: Page tables, virtual memory, buddy/slab allocators |
|    ├── CPU Configuration: SMP multi-core detection & CPU scheduling     |
|    ├── Hardware Probing: PCIe, ACPI, USB, storage buses (NVMe/SATA)     |
|    └── Command-Line Parsing: Reads boot parameters from /proc/cmdline   |
|                                │                                        |
|                                ▼                                        |
|  [ Early Userspace (initramfs Execution) ]                              |
|    ├── Mounts temporary RAM filesystem (rootfs / tmpfs)                 |
|    ├── udev loads exact storage & filesystem drivers                    |
|    └── Unlocks LUKS/LVM and mounts real disk partition to /sysroot      |
|                                │                                        |
|                                ▼                                        |
|  [ switch_root & Launching PID 1 ]                                      |
|    └─ Pivots to real root filesystem and executes /sbin/init (systemd)  |
|                                                                         |
+-------------------------------------------------------------------------+
```

---

## 2. Core Kernel Responsibilities During Startup

During early startup, the kernel's primary function is to initialize and "claim" every critical hardware subsystem:

### 1. Memory Management (VMM)
- **Physical to Virtual Mapping**: Maps physical RAM into a virtual address space.
- **Isolation**: Establishes the strict barrier between **Kernel Space (Ring 0)** and **User Space (Ring 3)**.
- **Allocators**: Initializes core kernel memory allocators (Buddy Allocator for page frames, Slab Allocator for object caching).

### 2. Processor & Multi-Core Setup (SMP)
- **Symmetric Multi-Processing (SMP)**: Identifies all physical CPU sockets, hardware cores, and hyperthreads.
- **Process Scheduler**: Starts the Completely Fair Scheduler (CFS / EEVDF) to distribute CPU execution time slices across processes.

### 3. I/O Subsystems & Bus Probing
- Detects the system bus architecture (PCIe, USB, I2C, SPI) and discovers connected controllers (NVMe storage, SATA host adapters, network interfaces, GPUs).

### 4. Parsing Kernel Command-Line Parameters
- Reads startup arguments supplied by the bootloader (viewable after boot via `cat /proc/cmdline`), such as:
  ```bash
  root=UUID=4a8f9b... ro quiet splash nomodeset
  ```

---

## 3. The Bridge: Early Userspace to Real Root

The kernel does not operate entirely on its own; it orchestrates the creation of **early userspace**:

```text
+-----------------------+           +-----------------------+
|   TEMPORARY ROOT      |           |    PERMANENT ROOT     |
|     (initramfs)       |           |     (Physical Disk)   |
|                       |           |                       |
| • Stored in RAM       | ────────> | • Stored on NVMe/SSD  |
| • udev driver loader  |  switch_  | • Full OS filesystem  |
| • Storage unlocker    |   root    | • System daemons      |
| • Mounts real root    |           | • User accounts/apps  |
+-----------------------+           +-----------------------+
```

1. **Temporary Root in RAM**: The kernel unpacks `initramfs` to run early setup scripts without needing access to the physical hard drive yet.
2. **Driver Discovery**: `udev` detects attached storage controllers and inserts the required driver modules (`.ko` files).
3. **Mounting Real Storage**: Once the physical disk partition is identified and checked, it is mounted to `/sysroot`.
4. **The Handoff**: The kernel performs `switch_root`, discards the temporary `initramfs` from RAM, and executes **`/sbin/init`** from the real disk as the very first user-space process (**PID 1**).

---

## 4. Key Takeaways

- The bootloader passes control to the kernel along with `initramfs` and command-line parameters.
- The kernel's `start_kernel()` function initializes CPU scheduling, virtual memory, and hardware buses.
- Early userspace (`initramfs`) resolves the storage dependency dilemma by loading disk drivers before mounting the real root (`/`).
- The kernel transitions from early RAM boot to permanent storage by launching `/sbin/init` (PID 1).