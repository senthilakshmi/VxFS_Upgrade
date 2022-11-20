# Veritas File system Upgrade (Ex: ver. 6 to 7)

<!-- Author : Senthil Kumar M (unix.senthil@gmail.com) -->

## Pre-requisites:-

**Process :** Ensure the Change record is fully approved and ready for implementation.  Make sure the implementation date is accurate.

**Technical :** Ensure the server is patched to the latest version && the relevant patch fix is installed.

**Note :** This document is designed for Solaris Operating Environment.

##  Steps :-
1. Ensure the alert Suppression is in place before the start of the activity
1. Take relevant backups and configuration updates
1. If mirroring available, detach the OS and SAN mirrors
1. Check the VxFS package _version_ 
    > **modinfo | grep -i vx** 
1. Pull the report of existing VxFS in the server 
    > **df -n |grep -i vxfs**
1. If the mountpoint is not existing, mount it 
    > **mount -F vxfs /dev/vx/dsk/diskgroup/volume /mountpoint** 
1. Check the VxFS file system version 
    > **fstyp -v <raw_device_filesystem> | grep -i version**
1. Ensure the server is patched to the latest
1. Upgrade the file system 
    ```
    /opt/VRTS/bin/vxupgrade -n <version_number> -r <raw_vxfs> <mountpoint>
    ```
1. Wait for the upgrade to complete ( It takes 5 to 10 seconds to upgrade a 200G file system )
1. Verify the VxFS file system version 
    > **fstyp -v <raw_device_filesystem> | grep -i version**
1. Update the relevant team to validate the applications
1. Attach the mirrors
1. Validate the pre and post checks
1. Stop the alert suppression

---
Reference : https://www.veritas.com/support/en_US/article.100022735

---
