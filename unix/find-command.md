# find command

Examples of [find](https://www.redhat.com/sysadmin/linux-find-command) command.

## Find by Content

The following command finds content of the file:

```bash
find . -name "*log" -exec grep -Hi SELinux {} \
```

Output:

```bash
17:48:48,665 DEBUG blivet:              SELinuxFS.supported: supported: False ;
17:48:48,665 DEBUG blivet: getFormat('selinuxfs') returning SELinuxFS instance with object id 133
17:48:48,741 INFO blivet: set SELinux context for newly mounted filesystem root at / to system_u:object_r:root_t:s0
17:48:48,741 INFO blivet: set SELinux context for newly mounted filesystem lost+found directory at /lost+found to system_u:object_r:lost_found_t:s0
17:48:48,765 INFO blivet: set SELinux context for newly mounted filesystem root at /boot to system_u:object_r:boot_t:s0
17:48:48,765 INFO blivet: set SELinux context for newly mounted filesystem lost+found directory at /boot/lost+found to system_u:object_r:lost_found_t:s0
17:48:48,777 INFO blivet: set SELinux context for newly mounted filesystem root at /dev to system_u:object_r:device_t:s0
```