
Useful links:
[https://gtfobins.github.io/](https://gtfobins.github.io/)

Upgrading to full TTY

```
which python

python -c 'import pty; pty.spawn("/bin/bash")'
python3 -c 'import pty; pty.spawn("/bin/bash")'

python -c 'import pty; pty.spawn("/bin/sh")'
python3 -c 'import pty; pty.spawn("/bin/sh")'

CTRL+Z

stty raw -echo ; fg

exit
```

Basics

```
id

whoami

sudo -l

su root

sudo -i
```

Check users

```
cat /etc/passwd

cat /etc/sudoers
```

