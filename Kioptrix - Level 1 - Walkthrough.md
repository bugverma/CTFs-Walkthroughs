## Machine Information

- **Attacker Machine**

**HOSTNAME:** kali
**IP ADDRESS:** 192.168.137.133
**SUBNET MASK:** 255.255.255.0

![[Pasted image 20221115162701.png]]

- **Target Machine**

**IP ADDRESS:** 192.168.137.134
**SUBNET MASK:** 255.255.255.0

![[Pasted image 20221115162810.png]]

## NMAP

- **All Ports**

![[Pasted image 20221115163834.png]]
![[Pasted image 20221115163908.png]]

## Enumerating SMB ie. Port 139

- **NMAP Scan**

![[Pasted image 20221115164535.png]]
![[Pasted image 20221115164731.png]]

**Findings**
Version: Samba smbd (workgroup: NMYGROUP) - SMB2
NetBIOS name: KIOPTRIX

- **Trying to Connect & Access SMB File Shares** 

![[Pasted image 20221115165251.png]]
![[Pasted image 20221115165515.png]]

**Findings**
We weren't able to Connect to either of the SMB File Shares.

- **Enumerating SMB Version**

![[Pasted image 20221115170137.png]]
![[Pasted image 20221115170210.png]]
![[Pasted image 20221115170251.png]]
![[Pasted image 20221115170332.png]]

**Findings**
Version: Samba 2.2.1a

- **Checking if SMB Version is Vulnerable to EternalBlue**
 
![[Pasted image 20221115170432.png]]
![[Pasted image 20221115170542.png]]
![[Pasted image 20221115170624.png]]
![[Pasted image 20221115170734.png]]
![[Pasted image 20221115170810.png]]

**Findings**
Not Vulnerable to Eternal Blue

- **Checking for more Vulnerablities**

We came across 2 Vulnerabilties:
1. Trans2Open - https://www.rapid7.com/db/modules/exploit/linux/samba/trans2open/ - But this wouldn't work because we weren't able to gain Anonymous Access to File Shares.
2. Samba < 2.2.8 (Linux/BSD) - Remote Code Execution - https://www.exploit-db.com/exploits/10

Trying out the Second One.

![[Pasted image 20221115173903.png]]
![[Pasted image 20221115173945.png]]
![[Pasted image 20221115174029.png]]

We Rooted the Machine. We can also see that there are 2 users:
- John
- Harold

Their Password Hashes are:
- John - $1$zL4.MR4t$26N4YpTGceBO0gTX6TAky1
- Harold - $1$Xx6dZdOd$IMOGACl3r757dv17LZ9010

These Passwords can be Cracked by using:
- unshadow
- John the Ripper

See this Video:
https://www.youtube.com/watch?v=X1Yl_StL1ac

