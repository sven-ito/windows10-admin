# Windows Update

## Check if Windows System files are "sane"

Checks if the system / update files are still valid / not damaged:

```
sfc /scannow
```

## Log File

In order to determine what exactly went wrong, review the log files:

You can create a log file based on ETL files with this tool: [Get-WindowsUpdateLog](https://docs.microsoft.com/de-de/powershell/module/windowsupdate/get-windowsupdatelog?view=win10-ps&preserve-view=tru)