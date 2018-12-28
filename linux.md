# Linux

## Table of contents

* [Commands](#commands)
  * [Get last lines of file](#get-last-lines-of-file)
* [Directory structure](#directory-structure)

## Commands

* `history` Shell history
* `history | less` Same, browsable with keyboard
* `watch ‘<command>’` Run command each X seconds (3 default) and print result
* `htop` Command-line task manager
* `<command> | grep <filter>` Filter a result

### Get last lines of file

https://www.computerhope.com/unix/utail.htm

```bash
tail <file>
```

* `<file>` show last lines from this file.
* `-f` update lines in real-time.
* `-n <lines>` show last X lines (10 by default).

## Directory structure

* `/bin` system's base commands.
* `/boot` necessary files for booting.
* `/dev` store devices informations (hard disk for example).
* `/etc` configuration files.
* `/home` personal folders of users.
* `/lib` shared libs (.so). Like .dll in Windows.
* `/lost+found` store lost/found files in case of disk crash.
* `/media` for removable devices (USB key, SD card...).
* `/mnt` for temporary mounted devices (optical disk...).
* `/opt` programs add-ons.
* `/proc` fake directory with system informations (CPU, RAM...)
* `/root` personal directory of root user.
* `/sbin` important system programs.
* `/tmp` temporary files. They will be deleted.
* `/usr` user's programs.
* `/var` variables files, like logs.
