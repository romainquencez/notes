# Linux

## Table of contents

* [Commands](#commands)
  * [Get last lines of file](#get-last-lines-of-file)

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
