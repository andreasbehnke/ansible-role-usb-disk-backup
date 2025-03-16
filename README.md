# Ansible Role: Backup to inexpensive USB disks

Provide rsync backup support for clients which perform the backup using inexpensive USB disks. Backup of ansible host in group ```backup_source``` will start when USB device is plugged in USB port of client. A desktop message shows up on startup, error or success of backup.

For each host a backup log file is created in ```/var/lib/backup/[hostname].log```

## Groups
This rule supports two groups of hosts. All hosts that have files that need to be backed up go into the backup_sources group. To all hosts (workstation or desktop computers) which will serve as a backup target, this rule should be applied.

## Backup Sources
Backup source can be any server in your network. This server should be in the ansible inventory group named by variable ```backup_source_group_name``` which defaults to ```backup_source```. Each backup source must provide the following variables:

```
backup_sources:
    - path: "/path/to/files"
      rsync_opts: "-aRH --exclude='lost+found' ..."
      user: "username"
    - path: ...

    ...

```

Multiple backup backup sources can be defined for each host.

## Backup Controller
The backup controller is the client, which will perform an automatic backup of all sources every time an USB disk drives is being plugged in. The following ansible inventory variables must be set for controller client:

```
backup_headless: [true|false] # if desktop notifications should be displayed, default true
backup_device:
    path: '/path/to/usb/disk'
    mount: 'media-username-backup.mount' # name of mount
backup_user: 'username'
backup_group: 'usergroup'
```

To determine correct mount name of your USB disk, plugin the disk and wait until it has been mounted and is displayed in file manager. After that run ```systemctl list-units -t mount```and search for mount name of USB device. Use this name for ```backup_device.mount```.

