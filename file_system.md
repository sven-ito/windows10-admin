# Filesystem - NTFS

## System Volume Information Folder

Contains:

* System Restore Points
* Volume Shadow Copy
* Indexing Service Database
* NTFS Disk Quota Settings
* Distributed Link Tracking Service Database
* DFS Replication and File deduplication service database

## Master File Table (MFT)

# Filesystem - GPT vs. MBR

## Convert from MBR to GPT

https://docs.microsoft.com/de-de/windows/deployment/mbr-to-gpt

# Filesystem - CHKDSK

## found.000 Folders

Take ownership as admin (execute cmd.exe as admin) so that you can delete them:

```
takeown /f C:\found.001 /R
```

## Run CHKDSK on partitions without letter (e.g. recovery partition)

Acronis Disk Director can do this.
The exact raw command, however, is unclear.

