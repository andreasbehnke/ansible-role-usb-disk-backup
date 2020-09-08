# ansible-role-backup-master

See [ansible-backup](https://github.com/andreasbehnke/ansible-backup) for details.
Supports two types of automatic backups:

* Provide rsync backup support for clients which perform the backup using inexpensive USB disks. Backup of backup_slaves will start when USB device is plugged in.

* Perform scheduled rsync backup
