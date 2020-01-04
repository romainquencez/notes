# NFS sharing

## Table of contents

* [Enable server-side share](#enable-server-side-share)
* [Enable client-side share](#enable-client-side-share)
* [Check server share](#check-server-share)

## Enable server-side share

Complete instructions : https://www.synology.com/en-us/knowledgebase/DSM/tutorial/File_Sharing/How_to_access_files_on_Synology_NAS_within_the_local_network_NFS

Be sure to set squash to "Map root to admin". This allow you to connect as root from the client and have admin user privileges.

## Enable client-side access

First, `nfs-common` package is required.

```
sudo apt update
sudo apt install nfs-common
```

Next, create the directory that will link to the share. You can create it in `/mnt`.

```
cd /mnt
sudo mkdir share
```

Add this line to `/etc/fstab` file to add mounting point :
```
YOUR_SERVER:/yourshare /mnt/share nfs rw,async,hard,intr,noexec 0 0
```

Finally, mount it :
```
sudo mount /mnt/share
```

## Check server share

You can check if your NFS share is enabled in your server with this command:
```
showmount -e <YOUR_SERVER>
```
