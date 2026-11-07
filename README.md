# CIP-B101 – Lab 1B: PC System Fundamentals, Disk Sectors and Partition Analysis

**International Cybersecurity and Digital Forensics Academy (ICDFA)**

---

## Student Information

| Field | Details |
|---|---|
| **Student Name** | Sharon Omowumi |
| **Registration Number** | [FDFC2617050 |
| **Course Code** | CIP-B101 |
| **Course Title** | Basic Computer Skills for Digital Forensics |
| **Laboratory Code** | Lab 1B |
| **Laboratory Title** | PC System Fundamentals, Disk Sectors and Partition Analysis |
| **Submission Date** | 5th November, 2026 |
| **Practical Environment** | Windows 10/11 Virtual Machine or Physical Computer |
| **Report Format** | PDF |

---

# 1. Introduction

This laboratory exercise focuses on the fundamental computer system concepts required for preliminary digital forensic investigations.

The purpose of this practical is to examine a computer system without modifying or compromising its existing data. The investigation involves identifying hardware and software specifications, examining running processes, inspecting disk structures, calculating partition sizes and identifying file systems.

The practical also explores how digital evidence can originate from different computer system layers, including user activities, applications, operating systems, storage devices and system memory.

Additionally, the laboratory examines the computer boot process and explains the differences between Master Boot Record (MBR) and GUID Partition Table (GPT) partitioning structures.

All practical activities are conducted using read-only inspection techniques. System information and partition details are collected through approved operating system utilities and commands.

The findings are documented through screenshots, calculations, technical observations and forensic interpretations.

## 1.1 Laboratory Objectives

The objectives of this laboratory are to:

1. Identify computer hardware, operating system, processor, memory and storage specifications.
2. Map potential digital evidence sources across different computer system layers.
3. Understand the differences between programs, processes and threads.
4. Calculate disk and partition sizes using sector information.
5. Inspect disk partition tables using safe, read-only commands.
6. Explain the PC boot process and distinguish between MBR and GPT.
7. Identify common file systems and understand their forensic importance.
8. Produce a structured forensic laboratory report supported by verifiable evidence.

---

# 2. Laboratory Environment and Tools

## 2.1 Practical Environment

| Component | Description |
|---|---|
| Host Operating System | [Insert host operating system] |
| Virtualisation Software | Oracle VM VirtualBox / Not Applicable |
| Examination Operating System | Windows 10/11 |
| System Architecture | [32-bit / 64-bit] |
| Examination Type | Preliminary system examination |
| Examination Approach | Read-only |
| Evidence Collection | Screenshots and command outputs |

## 2.2 Tools Used

| Tool | Purpose |
|---|---|
| System Information (`msinfo32`) | Identify operating system and hardware specifications |
| Command Prompt | Execute system identification commands |
| PowerShell | Retrieve disk, partition and volume information |
| Task Manager | Observe running applications and processes |
| `tasklist` | Identify running processes and their PIDs |
| Disk Management | Visually inspect disk and partition layouts |
| DiskPart | Inspect disk and partition information |
| Calculator / Python | Calculate partition sizes |
| Snipping Tool | Capture practical evidence screenshots |
| GitHub | Store and document laboratory work |

## 2.3 Evidence Handling and Safety Compliance

All examinations were performed using non-destructive inspection techniques.

The following safety precautions were observed:

- No partitions were created or deleted.
- No disks were formatted or resized.
- No existing data was intentionally modified.
- No destructive DiskPart commands were executed.
- Disk and partition information was collected using read-only inspection commands.
- Screenshots were captured to document the examination results.
- Personal identifiers and sensitive system information were excluded where unnecessary.

**Forensic principle:** The objective of this laboratory is to observe, identify, calculate, verify and document system information without compromising the integrity of the examined system.

---

# 3. Part A – System Identification and Evidence Layer Mapping

## 3.1 A1 – Basic System Specification

### Objective

To identify and document the computer's operating system, processor, memory, system architecture and BIOS/UEFI configuration.

### Procedure

1. Press `Windows + R`.
2. Type `msinfo32`.
3. Press Enter to open System Information.
4. Locate the following information:
   - OS Name
   - Version
   - System Type
   - Processor
   - BIOS Mode
   - Installed Physical Memory
   - Secure Boot State
5. Open Command Prompt.
6. Execute:

```cmd
systeminfo
```

7. Capture screenshots showing the system information and command output.

### Evidence A1 – System Information

**Screenshot 1: Windows System Information**

<img width="1548" height="853" alt="image" src="https://github.com/user-attachments/assets/11096c08-4d40-470a-a752-684cd15a637b" />

*Figure 1: System Information showing the operating system, processor, BIOS mode, installed memory and system architecture.*

**Screenshot 2: Systeminfo Command Output**

<img width="1181" height="955" alt="image" src="https://github.com/user-attachments/assets/59ef3721-c8a6-45cd-87a2-f4c24e0fcb1a" />

*Figure 2: System identification information collected using the Windows systeminfo command.*

### System Specification Results


| Specification | Observed Result |
|---|---|
| Operating System | Microsoft Windows 11 Pro |
| OS Version | 10.0.26300 N/A Build 26300 |
| System Type | x64-based PC |
| Processor | Intel64 Family 6 Model 154 Stepping 4 GenuineIntel ~2496 Mhz |
| Installed RAM | 4,077 MB |
| BIOS Mode | Legacy |
| Secure Boot State | Unsupported |
| Computer Name | SHARON-WIN11 |

### Forensic Interpretation

System identification provides an initial technical profile of the examined computer.

Operating system and hardware information helps investigators understand the environment in which digital evidence was generated.

Processor architecture and installed memory can influence the availability and interpretation of forensic artefacts. BIOS/UEFI information can also help determine how the system starts and which boot configuration is in use.

---

## 3.2 A2 – Storage Information

### Objective

To identify the physical storage devices, disk models, storage capacities, logical volumes and file systems.

### Procedure

Open PowerShell and execute the following commands individually.

**Command 1 – Identify physical disks**

```powershell
Get-Disk
```

**Command 2 – Identify disk models and capacities**

```powershell
Get-CimInstance Win32_DiskDrive |
Select-Object Model, Size, SerialNumber
```

**Command 3 – Identify partitions**

```powershell
Get-Partition
```

**Command 4 – Identify logical volumes**

```powershell
Get-Volume
```

**Command 5 – Identify logical disk information**

```powershell
Get-CimInstance Win32_LogicalDisk |
Select-Object DeviceID, VolumeName, FileSystem, Size, FreeSpace
```

Capture screenshots of the command outputs.

### Evidence A2 – Physical Disk Information

<img width="1118" height="633" alt="image" src="https://github.com/user-attachments/assets/22282f53-80e8-49b8-b341-95127f52edcd" />

*Figure 3: Physical disk model and storage capacity obtained through PowerShell.*

### Evidence A2 – Logical Volumes and File Systems

[Insert Screenshot Here]

*Figure 4: Logical volumes, file systems, total capacity and available storage.*

### Storage Observation Table

| Disk / Volume | Model or Drive | Total Size | File System | Free Space |
|---|---|---|---|---|
| Disk 0 | [Insert model] | [Insert size] | N/A | N/A |
| C: | [Insert volume] | [Insert size] | [NTFS / Other] | [Insert size] |
| D: | [Insert volume] | [Insert size] | [NTFS / Other] | [Insert size] |

*Add additional rows where necessary.*

### Forensic Interpretation

Storage examination is important because physical disks and logical volumes contain information that may be relevant to an investigation.

Examples include operating system files, user documents, deleted files, application data, file metadata and unallocated disk space.

Identifying the disk model and capacity also provides important context for later partition analysis and evidence verification.

---

## 3.3 A3 – Evidence Layer Mapping

### Objective

To identify the different computer system layers where digital evidence may be generated or stored.

Computer systems consist of multiple interconnected layers. User activities interact with applications, applications depend on the operating system, and the operating system communicates with hardware resources.

Evidence can therefore exist across multiple layers.

### Evidence Layer Mapping Table

| Layer / Source | Example Evidence | Where Evidence May Be Found | Forensic Importance |
|---|---|---|---|
| User Layer | Opened files, searches, typed information and login activities | Recent files, browser history and shell history | Helps establish user activities. |
| Application Layer | Document metadata, browser cache, application logs and chat records | Application folders, databases and cache directories | Identifies application usage and data creation. |
| Operating System Layer | Event logs, installed programs, registry entries and user profiles | Windows Event Viewer, Registry and system folders | Helps reconstruct system and account activities. |
| Disk / Storage Layer | Deleted files, file fragments, partitions and timestamps | File systems, unallocated space and disk images | Supports file recovery and timeline analysis. |
| Memory / Process Layer | Running processes, PIDs, malware and active network connections | RAM, Task Manager and process information | Helps identify live system behaviour. |
| Network Layer | Network connections, IP addresses and communication records | Network logs, firewall logs and connection tables | Helps investigate communications and network activity. |

### Explanation: Why Evidence Exists Across Multiple Layers

A single user action can generate evidence in several locations.

For example, when a user opens a document:

1. The user initiates the activity.
2. The application opens and processes the document.
3. The operating system records relevant activity and manages the application.
4. The disk stores the document and potentially related metadata.
5. System memory contains information about the running application and its activity.

Consequently, investigators should examine multiple evidence sources rather than relying on a single artefact.

### Forensic Interpretation

Evidence layer mapping provides a structured approach to preliminary digital investigations.

Correlating information from different layers can help investigators establish a more complete understanding of system activities and identify inconsistencies that may require further examination.

---

# 4. Part B – Program, Process and Thread Investigation

## 4.1 B1 – Observation of Running Processes

### Objective

To examine running processes and identify their process names, Process Identification Numbers (PIDs) and likely purposes.

### Procedure

1. Open Command Prompt.
2. Execute:

```cmd
tasklist
```

3. Observe the list of running processes.
4. Identify at least three processes.
5. Record their process names and PID values.
6. Capture a screenshot of the command output.

An alternative PowerShell command is:

```powershell
Get-Process |
Select-Object -First 20 Name, Id, CPU, WorkingSet
```

### Evidence B1 – Running Processes

[Insert Screenshot Here]

*Figure 5: Running Windows processes and associated Process Identification Numbers.*

### Process Observation Table

| Process Name | PID | Likely Purpose |
|---|---|---|
| [Process 1] | [PID] | [Explain purpose] |
| [Process 2] | [PID] | [Explain purpose] |
| [Process 3] | [PID] | [Explain purpose] |

### Forensic Interpretation

A process is an executing instance of a program.

Examining processes helps investigators identify which applications and services are currently active.

Unexpected processes, unusual resource consumption or suspicious process names may indicate potentially malicious activity.

Process information can also help investigators identify running applications during live forensic triage.

---

## 4.2 B2 – Difference Between Programs, Processes and Threads

### Program

A program is a collection of instructions stored on a computer, usually as an executable file.

It is not necessarily running simply because it exists on the computer.

**Example:** `notepad.exe` stored in the Windows operating system directory.

### Process

A process is an instance of a program that is currently executing.

It has its own process identification number, memory resources and execution environment.

**Example:** Opening Notepad creates a running Notepad process with an associated PID.

### Thread

A thread is the smallest unit of execution scheduled within a process.

A process can contain multiple threads that perform different tasks concurrently.

**Example:** A browser process may use separate threads to handle user input, page rendering and background activities.

### Comparison Table

| Feature | Program | Process | Thread |
|---|---|---|---|
| Meaning | Stored instructions | Running instance of a program | Execution unit within a process |
| State | Stored on disk | Active or executing | Executing within a process |
| Resources | Stored program files | Has process resources and memory | Shares process resources |
| Identification | File name | PID | Thread ID |
| Example | notepad.exe | Running Notepad | Notepad execution thread |

### Forensic Importance

Understanding the differences between programs, processes and threads is important during malware analysis and live forensic investigations.

A suspicious executable may exist on disk without currently executing. Examining running processes can help determine whether the program is active.

Thread-level examination can provide further insight into the behaviour of a process, especially when investigating malicious code or unusual application activity.

---

# 5. Part C – Disk Sector and Disk Size Calculation

## 5.1 Introduction to Disk Sectors

A disk sector is a fixed-size unit of storage used to organise and address data on a storage device.

Traditional disk calculations commonly use 512 bytes per sector, although modern storage devices may also use different logical and physical sector sizes.

Partition sizes can be calculated using the number of sectors occupied by a partition and the logical sector size.

### Disk Size Formula

**Total disk or partition size in bytes:**

```text
Number of sectors × Bytes per sector
```

**Convert bytes to gigabytes (GiB):**

```text
Total bytes ÷ 1024 ÷ 1024 ÷ 1024
```

For this report, binary gigabytes (GiB) are calculated using 1 GiB = 1,073,741,824 bytes.

---

## 5.2 C1 – Reproduction of the Course Slide Calculation

### Given Information

| Parameter | Value |
|---|---:|
| Sectors per Track | 400 |
| Number of Heads | 12 |
| Number of Cylinders | 17,000 |
| Bytes per Sector | 512 |

### Step 1 – Calculate Total Sectors

Formula:

```text
Total Sectors = Sectors per Track × Heads × Cylinders
```

Calculation:

```text
400 × 12 × 17,000

= 81,600,000 sectors
```

### Step 2 – Calculate Total Bytes

Formula:

```text
Total Bytes = Total Sectors × Bytes per Sector
```

Calculation:

```text
81,600,000 × 512

= 41,779,200,000 bytes
```

### Step 3 – Convert to Kilobytes

```text
41,779,200,000 ÷ 1024

= 40,800,000 KB
```

### Step 4 – Convert to Megabytes

```text
40,800,000 ÷ 1024

= 39,843.75 MB
```

### Step 5 – Convert to Gigabytes

```text
39,843.75 ÷ 1024

= 38.91 GiB (approximately)
```

### Calculation Summary

| Item | Calculation | Result |
|---|---|---:|
| Total Sectors | 400 × 12 × 17,000 | 81,600,000 |
| Total Bytes | 81,600,000 × 512 | 41,779,200,000 |
| Kilobytes | Bytes ÷ 1024 | 40,800,000 KB |
| Megabytes | KB ÷ 1024 | 39,843.75 MB |
| Gigabytes | MB ÷ 1024 | 38.91 GiB |

### Interpretation

The calculated disk capacity is approximately 38.91 GiB.

This calculation demonstrates how storage capacity can be derived from disk geometry and sector information.

The cylinder/head/sector calculation is a historical disk geometry method and should not be confused with the actual partition layout of a modern disk.

---

## 5.3 C2 – Actual Disk and Partition Size Calculation

### Objective

To identify at least two actual partitions from the examined computer's partition table and calculate their sizes using sector information.

This practical exercise is particularly important because the final assignment requires the identification and verification of partitions 1 and 2.

### Required Information

For each partition, collect:

- Partition number.
- Starting sector.
- Ending sector, where available.
- Total number of sectors.
- Logical sector size.
- File system, where available.
- Calculated partition size in GiB.

### Recommended PowerShell Commands

First, identify the disk and its logical sector size:

```powershell
Get-Disk |
Format-List Number, FriendlyName, PartitionStyle, Size, LogicalSectorSize, PhysicalSectorSize
```

Next, retrieve partition information:

```powershell
Get-Partition |
Format-Table DiskNumber, PartitionNumber, DriveLetter, Type, Offset, Size
```

These commands retrieve the disk and partition information without modifying the disk.

### Calculate Partition Sectors Using PowerShell

The following commands calculate the starting sector and sector count using the disk's logical sector size.

```powershell
$disk = Get-Disk -Number 0

Get-Partition -DiskNumber 0 | ForEach-Object {
    [PSCustomObject]@{
        PartitionNumber = $_.PartitionNumber
        StartSector = [math]::Floor($_.Offset / $disk.LogicalSectorSize)
        SectorCount = $_.Size / $disk.LogicalSectorSize
        SizeBytes = $_.Size
        SizeGiB = [math]::Round($_.Size / 1GB, 4)
    }
} | Format-Table -AutoSize
```

**Important:** In PowerShell, `1GB` represents 1,073,741,824 bytes. Therefore, the calculated value is in GiB, even though Windows commonly displays storage sizes using GB terminology.

### Alternative Linux Partition Table Command

For an approved Linux examination environment, the following command displays partition start and end sectors:

```bash
sudo fdisk -l
```

Additional disk information can be obtained using:

```bash
lsblk -o NAME,SIZE,TYPE,FSTYPE,START,SECTORS
```

Use the actual output to identify the first and second partitions.

### Evidence C2 – Partition Table

[Insert Screenshot Here]

*Figure 6: Partition table showing partition numbers, starting sectors, ending sectors and sector information.*

### Partition 1 Calculation

| Parameter | Value |
|---|---|
| Disk Number | [Insert disk number] |
| Partition Number | 1 |
| Starting Sector | [Insert value] |
| Ending Sector | [Insert value] |
| Sector Count | [Insert value] |
| Bytes per Sector | [Insert value] |
| File System | [Insert value] |

**Calculation:**

```text
Sector Count = Ending Sector - Starting Sector + 1

Partition Size (bytes) = Sector Count × Bytes per Sector

Partition Size (GiB) =
(Sector Count × Bytes per Sector) ÷ 1,073,741,824
```

**Insert actual calculation:**

```text
[Sector Count] × [Bytes per Sector]

= [Total bytes]

[Total bytes] ÷ 1,073,741,824

= [Calculated partition size] GiB
```

**Result:** Partition 1 has a calculated size of **[Insert result] GiB**.

### Evidence – Partition 1

[Insert Screenshot Here]

*Figure 7: Supporting partition table evidence and calculation for Partition 1.*

### Partition 2 Calculation

| Parameter | Value |
|---|---|
| Disk Number | [Insert disk number] |
| Partition Number | 2 |
| Starting Sector | [Insert value] |
| Ending Sector | [Insert value] |
| Sector Count | [Insert value] |
| Bytes per Sector | [Insert value] |
| File System | [Insert value] |

**Calculation:**

```text
Sector Count = Ending Sector - Starting Sector + 1

Partition Size (bytes) = Sector Count × Bytes per Sector

Partition Size (GiB) =
(Sector Count × Bytes per Sector) ÷ 1,073,741,824
```

**Insert actual calculation:**

```text
[Sector Count] × [Bytes per Sector]

= [Total bytes]

[Total bytes] ÷ 1,073,741,824

= [Calculated partition size] GiB
```

**Result:** Partition 2 has a calculated size of **[Insert result] GiB**.

### Evidence – Partition 2

[Insert Screenshot Here]

*Figure 8: Supporting partition table evidence and calculation for Partition 2.*

---

# 6. Part D – Safe Partition Table Inspection

## 6.1 D1 – Windows Disk Management

### Objective

To visually inspect the physical disk layout and identify existing partitions and volumes.

### Procedure

1. Press `Windows + R`.
2. Type:

```text
diskmgmt.msc
```

3. Press Enter.
4. Allow Disk Management to load.
5. Observe the available disks and their partitions.
6. Record the disk capacity, partition layout, drive letters and volume information.
7. Capture a screenshot.

### Evidence D1 – Disk Management

[Insert Screenshot Here]

*Figure 9: Windows Disk Management showing the physical disk and existing partition layout.*

### Observation

The Disk Management utility provides a graphical representation of the storage devices connected to the computer.

The examination focuses on identifying the number of partitions, their approximate sizes, file system information and available volumes.

---

## 6.2 D2 – PowerShell Partition Inspection

The following commands provide additional information about the disk and partition structure.

**Command 1:**

```powershell
Get-Disk
```

**Command 2:**

```powershell
Get-Partition
```

**Command 3:**

```powershell
Get-Volume
```

### Evidence D2 – PowerShell Output

[Insert Screenshot Here]

*Figure 10: PowerShell output showing physical disks, partition information and logical volumes.*

### Forensic Interpretation

PowerShell provides structured information about the storage configuration.

Combining the outputs of these commands helps distinguish physical disks, partitions and logical volumes.

The information also supports the manual calculations performed in Part C and the final verification exercise in Part G.

---

## 6.3 D3 – DiskPart Read-Only Inspection

### Objective

To inspect the disk and partition table using the Windows DiskPart utility.

### Procedure

Open Command Prompt as Administrator.

Execute the following commands individually:

**Command 1:**

```cmd
diskpart
```

**Command 2:**

```cmd
list disk
```

**Command 3:**

```cmd
select disk 0
```

**Command 4:**

```cmd
list partition
```

**Command 5:**

```cmd
exit
```

These commands are used to list and inspect the selected disk and its partitions.

**Safety warning:** Do not execute commands such as `clean`, `format`, `delete partition`, `create partition` or `convert` during this laboratory.

### Evidence D3 – DiskPart Output

[Insert Screenshot Here]

*Figure 11: DiskPart output showing the available disks and partition information.*

### Observation

DiskPart provides another method of examining the partition layout.

The `list disk` command identifies the available disks, while `list partition` displays the partitions associated with the selected disk.

The results can be compared with PowerShell and Disk Management to improve confidence in the collected observations.

---

# 7. Part E – MBR, GPT and PC Boot Process

## 7.1 E1 – Understanding the PC Boot Process

### Objective

To explain the sequence of events that occurs when a computer starts and transfers control to the operating system.

### Boot Process Explanation

**Stage 1 – Power-On**

The computer receives electrical power when the power button is pressed.

The motherboard, processor, memory and other hardware components begin their startup activities.

**Stage 2 – POST (Power-On Self-Test)**

The system performs initial hardware checks to determine whether essential components are functioning.

These checks may include processor, RAM and hardware detection.

**Stage 3 – BIOS/UEFI Firmware**

The system firmware initializes hardware and applies the configured startup settings.

It identifies available boot devices and determines the device from which the operating system should start.

CMOS-backed settings or firmware storage maintain configuration information such as system clock settings and boot preferences.

**Stage 4 – Boot Configuration and Partition Information**

The firmware follows the applicable boot method.

- Legacy BIOS systems generally use the MBR boot process.
- UEFI systems use EFI boot entries and an EFI System Partition, commonly formatted as FAT32.

**Stage 5 – Boot Loader / Boot Manager**

The boot loader or boot manager locates the operating system and prepares the required components for loading.

**Stage 6 – Kernel Loading**

The operating system kernel is loaded into memory.

The kernel initializes system resources, device drivers and essential operating system components.

**Stage 7 – Operating System Control**

The operating system completes startup and provides an environment for users, applications and system services.

### Boot Process Flow Diagram

```text
        COMPUTER POWER-ON
                |
                v
       POWER-ON SELF-TEST
              (POST)
                |
                v
        BIOS / UEFI FIRMWARE
                |
                v
       BOOT DEVICE SELECTION
                |
                v
       MBR / EFI BOOT METHOD
                |
                v
        BOOT LOADER / MANAGER
                |
                v
          KERNEL LOADING
                |
                v
       OPERATING SYSTEM STARTUP
                |
                v
        USER AND APPLICATIONS
```

### Forensic Relevance

Understanding the boot process helps forensic investigators identify how a computer loads its operating system.

Boot configuration information may help explain the presence of multiple operating systems, unusual boot entries or changes to startup configuration.

Investigators may also examine boot records and EFI structures when investigating boot-level malware or system compromise.

---

## 7.2 BIOS/UEFI Boot Mode Identification

### Objective

To identify whether the examined computer uses Legacy BIOS or UEFI firmware.

### Procedure

1. Press `Windows + R`.
2. Enter:

```text
msinfo32
```

3. Locate the BIOS Mode field.
4. Record whether the system uses UEFI or Legacy.
5. Capture a screenshot showing the result.

### Evidence E1 – BIOS/UEFI Mode

[Insert Screenshot Here]

*Figure 12: System Information showing the computer's BIOS mode.*

### Observation

| Parameter | Result |
|---|---|
| BIOS Mode | [UEFI / Legacy] |
| Secure Boot | [On / Off / Unsupported] |
| Partition Style | [GPT / MBR] |

**Note:** BIOS mode and partition style are related but are not identical. A UEFI system commonly uses GPT, but the two properties should be verified independently.

---

## 7.3 E2 – Comparison Between MBR and GPT

### Introduction

MBR and GPT are two partitioning schemes used to organise storage devices.

They differ in their structure, capacity limitations, partition management and recovery characteristics.

### MBR vs GPT Comparison Table

| Feature | MBR (Master Boot Record) | GPT (GUID Partition Table) |
|---|---|---|
| Introduction | Older partitioning scheme developed for early PC systems | Modern partitioning scheme |
| Boot Compatibility | Traditionally associated with Legacy BIOS | Commonly associated with UEFI |
| Maximum Disk Size | Approximately 2 TB with standard 512-byte sectors | Supports very large storage devices |
| Partition Limit | Traditionally four primary partitions | Commonly 128 partitions in standard Windows implementations |
| Partition Information | Stored in the first sector | Uses GPT headers and partition entry structures |
| Backup Information | No equivalent backup partition table | Backup GPT structures are stored near the end of the disk |
| Data Protection | Limited partition table redundancy | Includes CRC checksums for structural validation |
| Forensic Importance | Damage to sector 0 can affect partition interpretation | Backup structures can assist partition recovery and validation |

### Forensic Interpretation

MBR and GPT structures provide important information about how storage devices are organised.

When investigating an MBR-partitioned disk, sector 0 is particularly important because it contains the master boot record and partition entries.

GPT-partitioned disks contain additional structures, including a primary GPT header, partition entry array and backup structures.

These structures can be useful when investigating damaged partition tables or validating the organisation of a storage device.

---

# 8. Part F – File System Identification and Interpretation

## 8.1 Objective

To identify the file systems used by the examined computer and explain their importance in digital forensic investigations.

### Windows Commands

Execute the following PowerShell commands:

```powershell
Get-Volume
```

```powershell
Get-CimInstance Win32_LogicalDisk |
Select-Object DeviceID, FileSystem, Size, FreeSpace
```

Alternatively, use Command Prompt:

```cmd
wmic logicaldisk get caption,filesystem,size,freespace,volumename
```

### Evidence F1 – File System Identification

[Insert Screenshot Here]

*Figure 13: File system information obtained from the examined Windows volumes.*

### File System Observation Table

| Volume | File System | Total Size | Forensic Observation |
|---|---|---|---|
| C: | [Insert result] | [Insert size] | [Insert observation] |
| D: | [Insert result] | [Insert size] | [Insert observation] |

*Add additional rows where necessary.*

---

## 8.2 Common File Systems

### FAT / FAT32

FAT (File Allocation Table) is an older file system commonly used on removable storage devices.

FAT32 is frequently found on USB drives, memory cards and other portable storage media.

**Forensic importance:** FAT structures can contain directory entries, file allocation information and timestamps that may assist investigations.

### NTFS

NTFS (New Technology File System) is the standard file system used by modern Windows installations.

It supports features such as:

- Master File Table (MFT).
- File and directory metadata.
- Access control permissions.
- Alternate Data Streams.
- Journaling.
- File timestamps.

**Forensic importance:** NTFS contains metadata that can assist investigators in recovering files, analysing file activity and constructing timelines.

### ext Family

The ext family includes ext2, ext3 and ext4, which are commonly used by Linux systems.

These file systems use inodes to store information about files and directories.

**Forensic importance:** Inode metadata, directory structures and file allocation information can assist with Linux forensic analysis.

### XFS

XFS is a high-performance journaling file system commonly used in Linux environments.

**Forensic importance:** Its metadata and allocation structures are important when examining Linux storage devices.

### JFS

JFS (Journaled File System) is a journaling file system originally developed by IBM.

**Forensic importance:** Its journal and metadata structures may provide useful information during file system investigations.

### Btrfs

Btrfs is a modern Linux file system that supports advanced features such as snapshots, checksums and copy-on-write.

**Forensic importance:** Snapshots and metadata structures may preserve historical file system states that can be useful during an investigation.

### HFS+

HFS+ is an older file system associated with Apple macOS systems.

**Forensic importance:** It is relevant when examining older Mac computers and storage devices.

### File System Comparison

| File System | Common Usage | Forensic Importance |
|---|---|---|
| FAT/FAT32 | USB drives and removable media | Directory structures and file allocation information |
| NTFS | Windows computers | MFT, timestamps, permissions and journaling |
| ext2/ext3/ext4 | Linux computers | Inodes, metadata and file recovery |
| XFS | Linux/Unix-like systems | Journaling and metadata structures |
| JFS | Linux/Unix-like systems | Journal and file system metadata |
| Btrfs | Modern Linux systems | Snapshots, checksums and copy-on-write |
| HFS+ | Older macOS systems | Mac file system metadata and directory structures |

### Forensic Interpretation

File systems are essential to digital forensic investigations because they determine how files and directories are organised and how metadata is stored.

The type of file system affects the techniques available for examining, recovering and interpreting digital evidence.

Investigators must understand the file system before interpreting file timestamps, deleted files, metadata and allocation structures.

---

# 9. Part G – Final Practical Assignment: Partition 1 and Partition 2 Verification

## 9.1 Objective

The main objective of this assignment is to identify partitions 1 and 2 from an actual partition table, record their sector information, calculate their sizes in GiB and verify the calculated results against the operating system's reported storage information.

This section is a critical part of the laboratory assessment.

**Important:** Partition calculations must be supported by actual partition table evidence. Disk Management screenshots alone are not sufficient to demonstrate sector-based calculations.

## 9.2 Step 1 – Identify the Physical Disk

Execute:

```powershell
Get-Disk
```

Record the following:

| Parameter | Observation |
|---|---|
| Disk Number | [Insert result] |
| Disk Model | [Insert result] |
| Disk Size | [Insert result] |
| Partition Style | [GPT / MBR] |
| Logical Sector Size | [Insert result] |

### Evidence G1 – Physical Disk Identification

[Insert Screenshot Here]

*Figure 14: Physical disk identification and partition style.*

## 9.3 Step 2 – Inspect the Actual Partition Table

Execute:

```powershell
Get-Partition -DiskNumber 0
```

For additional information, execute:

```powershell
Get-Disk -Number 0 |
Format-List Number, FriendlyName, PartitionStyle, Size, LogicalSectorSize
```

Then execute:

```powershell
Get-Partition -DiskNumber 0 |
Format-Table PartitionNumber, DriveLetter, Type, Offset, Size
```

For a clearer start-sector and sector-count view, use the PowerShell calculation provided in Part C.

Alternatively, use an approved Linux environment and execute:

```bash
sudo fdisk -l
```

Record the partition table information for partitions 1 and 2.

### Evidence G2 – Actual Partition Table

[Insert Screenshot Here]

*Figure 15: Actual partition table identifying partitions 1 and 2 and their sector information.*

## 9.4 Step 3 – Partition 1 Identification

| Parameter | Recorded Value |
|---|---|
| Partition Number | 1 |
| Starting Sector | [Insert value] |
| Ending Sector | [Insert value] |
| Number of Sectors | [Insert value] |
| Logical Sector Size | [Insert value] bytes |
| File System | [Insert value] |
| Operating System Reported Size | [Insert value] |

### Partition 1 Calculation

Formula:

```text
Partition Size = Number of Sectors × Bytes per Sector
```

Convert to GiB:

```text
Partition Size (GiB) =
(Number of Sectors × Bytes per Sector)
÷ 1,073,741,824
```

Calculation:

```text
[Insert sector count] × [Insert sector size]

= [Insert total bytes]

[Insert total bytes] ÷ 1,073,741,824

= [Insert calculated size] GiB
```

**Final Partition 1 Size: [Insert calculated result] GiB**

### Evidence G3 – Partition 1 Calculation

[Insert Screenshot Here]

*Figure 16: Manual calculation of Partition 1 using the actual partition sector count.*

## 9.5 Step 4 – Partition 2 Identification

| Parameter | Recorded Value |
|---|---|
| Partition Number | 2 |
| Starting Sector | [Insert value] |
| Ending Sector | [Insert value] |
| Number of Sectors | [Insert value] |
| Logical Sector Size | [Insert value] bytes |
| File System | [Insert value] |
| Operating System Reported Size | [Insert value] |

### Partition 2 Calculation

Formula:

```text
Partition Size = Number of Sectors × Bytes per Sector
```

Convert to GiB:

```text
Partition Size (GiB) =
(Number of Sectors × Bytes per Sector)
÷ 1,073,741,824
```

Calculation:

```text
[Insert sector count] × [Insert sector size]

= [Insert total bytes]

[Insert total bytes] ÷ 1,073,741,824

= [Insert calculated size] GiB
```

**Final Partition 2 Size: [Insert calculated result] GiB**

### Evidence G4 – Partition 2 Calculation

[Insert Screenshot Here]

*Figure 17: Manual calculation of Partition 2 using the actual partition sector count.*

## 9.6 Step 5 – Verify Results Against Operating System Information

Compare the calculated partition sizes against the information reported by Windows Disk Management and PowerShell.

Execute:

```powershell
Get-Partition |
Format-Table DiskNumber, PartitionNumber, DriveLetter, Size
```

To examine the corresponding logical volumes:

```powershell
Get-Volume
```

### Partition Verification Table

| Parameter | Partition 1 | Partition 2 |
|---|---|---|
| Starting Sector | [Insert] | [Insert] |
| Ending Sector | [Insert] | [Insert] |
| Sector Count | [Insert] | [Insert] |
| Bytes per Sector | [Insert] | [Insert] |
| Calculated Size (GiB) | [Insert] | [Insert] |
| OS Reported Size | [Insert] | [Insert] |
| Verification Status | [Verified / Explain difference] | [Verified / Explain difference] |

### Evidence G5 – Operating System Verification

[Insert Screenshot Here]

*Figure 18: Operating system partition information used to verify the manually calculated partition sizes.*

## 9.7 Step 6 – Explain Any Differences

Calculated partition sizes and operating system-reported volume sizes may differ for several reasons.

**1. GB and GiB Differences**

Storage manufacturers commonly use decimal gigabytes:

```text
1 GB = 1,000,000,000 bytes
```

Windows and many forensic tools may display values using binary units:

```text
1 GiB = 1,073,741,824 bytes
```

**2. File System Overhead**

Some storage space is used for file system structures, metadata, journals and allocation information.

**3. Reserved Partitions**

Some disk space may be allocated to system partitions, recovery partitions and boot-related structures.

**4. Partition and Volume Differences**

A physical partition and its associated logical volume are not necessarily interchangeable concepts.

A partition can contain file system structures, reserved space and metadata that affect the usable capacity reported by the operating system.

### Final Verification Interpretation

[Insert your actual comparison and explain whether the calculated sizes agree with the operating system information.]

The comparison demonstrates how partition sizes can be independently calculated from sector information and checked against operating system reports.

---

# 10. Consolidated Evidence Register

The following table provides a record of the mandatory practical evidence required by the ICDFA laboratory manual.

| Evidence ID | Required Evidence | Screenshot / Section | Status |
|---|---|---|---|
| EVID-001 | System Information or systeminfo output | Figure 1–2 | [Pending / Complete] |
| EVID-002 | Disk model and storage capacity | Figure 3 | [Pending / Complete] |
| EVID-003 | Logical volume and file system information | Figure 4 | [Pending / Complete] |
| EVID-004 | Running processes and PID information | Figure 5 | [Pending / Complete] |
| EVID-005 | Disk and partition table inspection output | Figure 6, 9–11, 15 | [Pending / Complete] |
| EVID-006 | Partition 1 calculation and supporting evidence | Figure 7, 16 | [Pending / Complete] |
| EVID-007 | Partition 2 calculation and supporting evidence | Figure 8, 17 | [Pending / Complete] |
| EVID-008 | BIOS/UEFI boot mode evidence | Figure 12 | [Pending / Complete] |
| EVID-009 | File system identification evidence | Figure 13 | [Pending / Complete] |
| EVID-010 | Final report summary and conclusion | Section 11 | [Pending / Complete] |

---

# 11. Conclusion

This laboratory provided practical experience in identifying computer system specifications, examining running processes, inspecting storage devices and understanding partition structures from a digital forensic perspective.

The examination demonstrated how computer systems generate and store potential digital evidence across different layers, including user activities, applications, operating systems, storage devices and memory.

The process investigation introduced the differences between programs, processes and threads and highlighted the importance of process information during live forensic analysis.

The disk examination provided an understanding of sectors, partition structures and the mathematical methods used to calculate storage capacity. By identifying actual partitions and calculating their sizes using sector information, the practical demonstrated the importance of verifying operating system storage information against underlying partition table evidence.

The laboratory also examined the PC boot process, compared MBR and GPT partitioning schemes and introduced common file systems used by Windows, Linux and macOS systems.

Most importantly, the exercise reinforced the importance of evidence integrity and safe examination practices. All observations and calculations were performed using read-only methods without intentionally modifying or compromising the examined system.

**Overall, this laboratory strengthened my understanding of computer system fundamentals and demonstrated how hardware, operating systems, storage structures and file systems contribute to digital forensic investigations.**

---

# 12. References and Learning Resources

The following materials were used as supporting references for this laboratory.

1. ICDFA – Computer System Introduction course slides.
2. ICDFA – CIP-B101 Lab 1B: PC System Fundamentals, Disk Sectors and Partition Analysis.
3. Microsoft Documentation – Windows System Information.
4. Microsoft Documentation – PowerShell Storage Management.
5. Microsoft Documentation – Windows Disk Management and DiskPart.
6. Linux Manual Pages – `fdisk`, `lsblk`, `blkid` and `parted`.

### Additional Learning Resources

- [Microsoft Learn – Get-Disk](https://learn.microsoft.com/en-us/powershell/module/storage/get-disk)
- [Microsoft Learn – Get-Partition](https://learn.microsoft.com/en-us/powershell/module/storage/get-partition)
- [Microsoft Learn – Get-Volume](https://learn.microsoft.com/en-us/powershell/module/storage/get-volume)
- [Microsoft Learn – DiskPart](https://learn.microsoft.com/en-us/windows-server/administration/windows-commands/diskpart)
- [Linux fdisk Manual](https://man7.org/linux/man-pages/man8/fdisk.8.html)
- [Linux lsblk Manual](https://man7.org/linux/man-pages/man8/lsblk.8.html)

---

# 13. Declaration of Practical Work

I confirm that this laboratory report documents the practical work undertaken for CIP-B101 Lab 1B.

The system observations, command outputs, screenshots and calculations included in the final submitted report are intended to represent the actual results obtained from the approved examination environment.

All disk examination activities were conducted using read-only methods, and no destructive partition operations were performed.

**Student:** Sharon Omowumi

**Course:** CIP-B101 – Basic Computer Skills for Digital Forensics

**Laboratory:** Lab 1B – PC System Fundamentals, Disk Sectors and Partition Analysis

**Date:** [Insert Submission Date]

---

**End of Laboratory Report**
