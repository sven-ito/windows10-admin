# Filesystem - NTFS

## Facts

* current version 3.1 (since Windows XP, also commonly called NTFS 5.1)
* MBR Partitition identification code is "07" (same as HPFS from OS/2)

### Archticeture / Parts

* A cluster (or allocation unit) is the smallest amount of disk space that can be allocated to hold a file.
* (Allocation) Bitmap ($Bitmap) describes which clusters are available/free
* uses Access Control Lists (ACLs) for permissions
* Master File Table (MFT, $MFT) per partition -> serves as table of contents
* Journaling File System -> via NTFS log ($LogFile); format changed with Windows 8.1 to "2.0" (not backwards-compatible to "1.0")
* since Vista: NTFS symbolic links, transactional NTFS (discouraged by developers), partition shrinking, self-healing
* comes with a series of metadata files (e.g. $Boot, $MFT, $Bitmap)

#### Make Metadata Files visible

(from Admin Shell, all details for drive C:, also lists metadata files)

```
fsutil volume allocationreport C:
```

* Also various third party tools can do this (e.g. WinHex, 7-Zip); however, recent security patches might prevent it

#### Boot Mechanism

* MBR / GPT are possible
* [Microsoft - Tool - Conversion: MBR -> GPT](https://docs.microsoft.com/de-de/windows/deployment/mbr-to-gpt)
* Booting from GPT requires UEFI and a 64 Bit OS
* GPT requires a special UEFI partition (usually no drive letter, ~100 MB, NTFS); don't mix up with Windows Recocery / RE partition
* BIOS -> MBR -> (Exec Code) -> System Partition Boot Sector (VBR) -> NTldr (NTFS.sys; NToskrnl.exe) -> Boot.ini / BCD

#### System Volume Information Folder

Exists on every drive; contains:

* System Restore Points
* Volume Shadow Copy
* Indexing Service Database
* NTFS Disk Quota Settings
* Distributed Link Tracking Service Database
* DFS Replication and File deduplication service database

#### Repair (CHKDSK)

##### found.000 Folders

Take ownership as admin (execute cmd.exe as admin) so that you can delete them:

```
takeown /f C:\found.001 /R
```

##### Run CHKDSK on partitions without letter (e.g. recovery partition)

* Acronis Disk Director can do this.
* The exact raw command, however, is unclear.

### Numbers / Limits

* Maximum partition size is 2TB (MBR limitation)
* maximum implemented filesize is 8PB (-2MB); in theory it can be up to 16 EiB (-1KB)
* Up to 1024 hard links can reference the same file (may only reference files on the same volume due to MFT)
* NTFS is optimized for 4K clusters (compression feature in particular)

### Hints

* Linux/BSD driver (NTFS-3G) can read/write
* MacOS driver can only read

## Documentation

* [Wikipedia Page - Good Overview](https://en.wikipedia.org/wiki/NTFS)
* [Microsoft - NTFS Overview](https://docs.microsoft.com/en-us/windows-server/storage/file-server/ntfs-overview)
* [Microsoft - NTFS Technical Reference](https://docs.microsoft.com/en-us/previous-versions/windows/it-pro/windows-server-2003/cc758691(v=ws.10)?redirectedfrom=MSDN)
* [Microsoft - What is NTFS?](https://docs.microsoft.com/en-us/previous-versions/windows/it-pro/windows-server-2003/cc778410(v=ws.10))
* [Microsoft - How NTFS Works](https://docs.microsoft.com/en-us/previous-versions/windows/it-pro/windows-server-2003/cc781134(v=ws.10))
* [Microsoft - NTFS Tools and Settings](https://docs.microsoft.com/en-us/previous-versions/windows/it-pro/windows-server-2003/cc757759(v=ws.10))
* [Microsoft - Tools - fsutil](https://docs.microsoft.com/en-us/windows-server/administration/windows-commands/fsutil)
* [NTFS Internals - Reverse Engineered](https://thestarman.pcministry.com/asm/mbr/IntNTFSfs.htm)
* [Forensics Blog A - NTFS Physical Structure](https://www.datarecoveryunion.com/how-ntfs-file-system-works-ntfs-physical-structure/)
* [Forensics Blog B - Journaling 1](https://countuponsecurity.com/2016/05/30/digital-forensics-ntfs-indx-and-journaling/)
* [Forensics Blog B - Journaling 2](https://countuponsecurity.com/2017/05/25/digital-forensics-ntfs-change-journal/)
* [Forensics Blog C - Journaling 3](https://dfir.ru/2019/02/16/how-the-logfile-works/)


