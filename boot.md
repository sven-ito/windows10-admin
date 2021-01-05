# Boot Procedure Windows 10

## General

1. PreBoot
2. Windows Boot Manager (OS Selection)
3. Windows OS Loader  (first drivers)
4. Windows NT OS Kernel (aditional drivers, registry, UI)

## BIOS

1. Valid MBR? 
2. MBR (Bootstrap Code)
3. VBR (on system volume - OR - System Reserved partition w/o letter)
4. %SystemDrive%\bootmgr (OS Selection; on system volume - OR - System Reserved partition w/o letter)
5. %SystemRoot%\system32\winload.exe (first drivers)
6. %SystemRoot%\system32\ntoskrnl.exe (aditional drivers, registry, UI)

NTLDR is deprecated/legacy (replaced by BOOTMGR / winload.exe or winresume.exe) -> uses boot.ini; see [Lifewire NTLDR article](https://www.lifewire.com/what-is-ntldr-2625949) and [Lifewire BOOTMGR article](https://www.lifewire.com/windows-boot-manager-bootmgr-2625813).

## UEFI

1. UEFI Firmware
2. Trusted/Secured Boot? -> validate bootloader signature
3. \EFI\Microsoft\Boot\bootmgfw.efi (OS Selection, BCD data also resides here)
4. %SystemRoot%\system32\winload.efi (first drivers)
5. %SystemRoot%\system32\ntoskrnl.exe (aditional drivers, registry, UI)