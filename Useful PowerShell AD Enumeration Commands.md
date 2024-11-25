# Useful PowerShell AD Enumeration Commands

sometimes a man just dont wanna learn all the syntax and need those commands fireable pew pew haha

# 🎃Users 🎃

## 🐈‍⬛.scf file🐈‍⬛

Get-WindowsCapability -Name RSAT* -Online | Select-Object -Property Name, State 	Check if RSAT tools are installed
Get-WindowsCapability -Name RSAT* -Online | Add-WindowsCapability –Online


## ⭐ Attacker


##🌙 Victim



```
[Shell]

```


Here's a cheatsheet for enumerating Active Directory (AD) using the RSAT (Remote Server Administration Tools) with PowerShell. This guide includes common commands for querying AD objects like users, groups, computers, and organizational units.
Setup Prerequisites

    Install RSAT:

Install-WindowsFeature -Name RSAT-AD-PowerShell

##🌙  Import the AD module:

    Import-Module ActiveDirectory

#🌙 1. General Domain Information
##🌙 Get Current Domain:

(Get-ADDomain).Name

##🌙 Get Domain Controller Details:

Get-ADDomainController -Filter *

##🌙 List All Trusted Domains:

Get-ADTrust -Filter *

#🌙 2. Enumerating Users
##🌙 Get All Users:

Get-ADUser -Filter * -Properties DisplayName | Select-Object Name, SamAccountName

##🌙 Find Disabled Accounts:

Get-ADUser -Filter {Enabled -eq $false} -Properties DisplayName | Select-Object Name, SamAccountName

##🌙 Find Locked-Out Accounts:

Search-ADAccount -LockedOut

##🌙 Find Accounts with Password Never Expiring:

Get-ADUser -Filter * -Properties PasswordNeverExpires | Where-Object { $_.PasswordNeverExpires -eq $true } | Select-Object Name, SamAccountName

#🌙 3. Enumerating Groups
##🌙 List All Groups:

Get-ADGroup -Filter * | Select-Object Name, SamAccountName

##🌙 Find Group Membership for a User:

Get-ADUser -Identity "username" -Properties MemberOf | Select-Object -ExpandProperty MemberOf

##🌙 List Members of a Group:

Get-ADGroupMember -Identity "GroupName" | Select-Object Name, SamAccountName

#🌙 4. Enumerating Computers
##🌙 Get All Computers:

Get-ADComputer -Filter * | Select-Object Name, OperatingSystem

##🌙 Find Disabled Computers:

Get-ADComputer -Filter {Enabled -eq $false} | Select-Object Name

##🌙 Find Stale Computers (Inactive for 90+ Days):

Get-ADComputer -Filter * -Properties LastLogonDate | Where-Object { $_.LastLogonDate -lt (Get-Date).AddDays(-90) } | Select-Object Name, LastLogonDate

#🌙 5. Organizational Units (OUs)
##🌙 List All OUs:

Get-ADOrganizationalUnit -Filter * | Select-Object Name, DistinguishedName

##🌙 Find Objects in a Specific OU:

Get-ADObject -Filter * -SearchBase "OU=IT,DC=domain,DC=com" | Select-Object Name, ObjectClass

#🌙 6. Advanced Enumeration
##🌙 Find Service Accounts (Accounts with SPNs):

Get-ADUser -Filter {ServicePrincipalName -like "*"} -Properties ServicePrincipalName | Select-Object Name, SamAccountName, ServicePrincipalName

##🌙 Search for High-Privilege Users:

Get-ADUser -Filter * -Properties MemberOf | Where-Object { $_.MemberOf -like "*Admins*" } | Select-Object Name, SamAccountName

##🌙 List GPOs Applied to a User or Computer:

Get-GPResultantSetOfPolicy -ReportType HTML -Path "C:\GPOReport.html"

#🌙 7. Auditing and Monitoring
##🌙 Check for Recently Created Accounts:

Get-ADUser -Filter * -Properties WhenCreated | Where-Object { $_.WhenCreated -gt (Get-Date).AddDays(-30) } | Select-Object Name, WhenCreated

##🌙 List Locked-Out Accounts:

Search-ADAccount -LockedOut | Select-Object Name, SamAccountName

##🌙 Find Accounts with Expired Passwords:

Search-ADAccount -PasswordExpired | Select-Object Name, SamAccountName


