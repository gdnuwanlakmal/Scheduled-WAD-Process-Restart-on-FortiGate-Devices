# Scheduled WAD Process Restart on FortiGate Devices
This guide provides a script to automatically restart the Web Application Daemon (WAD) on FortiGate devices every 12 hours. It includes versions for both setups with and without VDOMs. This is a temporary workaround to address WAD-related issues until a permanent fix is implemented.
### ✅ For FortiGate Devices Without VDOMs
```shell
config system auto-script
    edit restart_wad
        set interval 43200         # Interval in seconds (12 hours)
        set repeat 356             # Number of times to repeat
        set start auto             # Start automatically on boot
        set script 'diag test app wad 99'  # Restart WAD process
    next
end
```
### ✅ For FortiGate Devices With VDOMs
```shell
config system auto-script
    edit restart_wad
        set interval 43200
        set repeat 356
        set start auto
        set script '
config global
diag test app wad 99'
    next
end
```
### 🔄 Notes:
* 43200 seconds = 12 hours

* The script will run 356 times → roughly 6 months

* diag test app wad 99 restarts the WAD process

* Modify interval and repeat as per your requirements

* Important: Remove this script once a permanent fix is applied to avoid unnecessary WAD restarts
