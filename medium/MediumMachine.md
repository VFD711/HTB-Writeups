```shell 
Not shown: 994 closed tcp ports (reset)
PORT     STATE SERVICE       VERSION
111/tcp  open  rpcbind?
|_rpcinfo: ERROR: Script execution failed (use -d to debug)
135/tcp  open  msrpc         Microsoft Windows RPC
139/tcp  open  netbios-ssn   Microsoft Windows netbios-ssn
445/tcp  open  microsoft-ds?
2049/tcp open  mountd        1-3 (RPC #100005)
3389/tcp open  ms-wbt-server Microsoft Terminal Services
| rdp-ntlm-info:
|   Target_Name: WINMEDIUM
|   NetBIOS_Domain_Name: WINMEDIUM
|   NetBIOS_Computer_Name: WINMEDIUM
|   DNS_Domain_Name: WINMEDIUM
|   DNS_Computer_Name: WINMEDIUM
|   Product_Version: 10.0.17763
|_  System_Time: 2026-09-17T07:49:30+00:00
| ssl-cert: Subject: commonName=WINMEDIUM
| Not valid before: 2026-09-16T07:40:48
|_Not valid after:  2027-03-18T07:40:48
|_ssl-date: 2026-09-17T07:49:39+00:00; -34s from scanner time.
Service Info: OS: Windows; CPE: cpe:/o:microsoft:windows

Host script results:
| smb2-security-mode:
|   3:1:1:
|_    Message signing enabled but not required
| smb2-time:
|   date: 2026-09-17T07:49:33
|_  start_date: N/A
|_clock-skew: mean: -34s, deviation: 0s, median: -34s

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
```
then i didnt know much about windows machine since this is my first Certificate test , so i use write up to follow up the idea and found this , by using `showmount` command to display mount and export the information for a network file system (`NFS`) server, and by adding `-e` / `--exports` to show NFS server's export list (shared directory available mounting) , we found this directory 
```shell
showmount -e 10.129.176.221
Export list for 10.129.176.221:
/TechSupport (everyone)
```
and by that i create file directory with `targetNFS` name i can check the directory with command `sudo ls -lah` which mean list all with human readable and i found this 
```shell
sudo ls -lah targetNFS/
total 68K
drwx------ 2 4294967294 4294967294  64K Nov 11  2021 .
drwxrwxrwx 1 nxz        nxz         512 Sep 18 13:22 ..
-rwx------ 1 4294967294 4294967294    0 Nov 10  2021 ticket4238791283649.txt
-rwx------ 1 4294967294 4294967294    0 Nov 10  2021 ticket4238791283650.txt
-rwx------ 1 4294967294 4294967294    0 Nov 10  2021 ticket4238791283651.txt
-rwx------ 1 4294967294 4294967294    0 Nov 10  2021 ticket4238791283652.txt
-rwx------ 1 4294967294 4294967294    0 Nov 10  2021 ticket4238791283653.txt
-rwx------ 1 4294967294 4294967294    0 Nov 10  2021 ticket4238791283654.txt
-rwx------ 1 4294967294 4294967294    0 Nov 10  2021 ticket4238791283655.txt
-rwx------ 1 4294967294 4294967294    0 Nov 10  2021 ticket4238791283656.txt
-rwx------ 1 4294967294 4294967294    0 Nov 10  2021 ticket4238791283657.txt
-rwx------ 1 4294967294 4294967294    0 Nov 10  2021 ticket4238791283658.txt
-rwx------ 1 4294967294 4294967294    0 Nov 10  2021 ticket4238791283659.txt
-rwx------ 1 4294967294 4294967294    0 Nov 10  2021 ticket4238791283660.txt
-rwx------ 1 4294967294 4294967294    0 Nov 10  2021 ticket4238791283661.txt
-rwx------ 1 4294967294 4294967294    0 Nov 10  2021 ticket4238791283662.txt
-rwx------ 1 4294967294 4294967294    0 Nov 10  2021 ticket4238791283663.txt
-rwx------ 1 4294967294 4294967294    0 Nov 10  2021 ticket4238791283664.txt
-rwx------ 1 4294967294 4294967294    0 Nov 10  2021 ticket4238791283665.txt
-rwx------ 1 4294967294 4294967294    0 Nov 10  2021 ticket4238791283666.txt
-rwx------ 1 4294967294 4294967294    0 Nov 10  2021 ticket4238791283667.txt
-rwx------ 1 4294967294 4294967294    0 Nov 10  2021 ticket4238791283668.txt
-rwx------ 1 4294967294 4294967294    0 Nov 10  2021 ticket4238791283669.txt
-rwx------ 1 4294967294 4294967294    0 Nov 10  2021 ticket4238791283670.txt
-rwx------ 1 4294967294 4294967294    0 Nov 10  2021 ticket4238791283671.txt
-rwx------ 1 4294967294 4294967294    0 Nov 10  2021 ticket4238791283672.txt
-rwx------ 1 4294967294 4294967294    0 Nov 10  2021 ticket4238791283673.txt
-rwx------ 1 4294967294 4294967294    0 Nov 10  2021 ticket4238791283674.txt
-rwx------ 1 4294967294 4294967294    0 Nov 10  2021 ticket4238791283675.txt
-rwx------ 1 4294967294 4294967294    0 Nov 10  2021 ticket4238791283676.txt
-rwx------ 1 4294967294 4294967294    0 Nov 10  2021 ticket4238791283677.txt
-rwx------ 1 4294967294 4294967294    0 Nov 10  2021 ticket4238791283678.txt
-rwx------ 1 4294967294 4294967294    0 Nov 10  2021 ticket4238791283679.txt
-rwx------ 1 4294967294 4294967294    0 Nov 10  2021 ticket4238791283680.txt
-rwx------ 1 4294967294 4294967294    0 Nov 10  2021 ticket4238791283681.txt
-rwx------ 1 4294967294 4294967294    0 Nov 10  2021 ticket4238791283682.txt
-rwx------ 1 4294967294 4294967294    0 Nov 10  2021 ticket4238791283683.txt
-rwx------ 1 4294967294 4294967294    0 Nov 10  2021 ticket4238791283684.txt
-rwx------ 1 4294967294 4294967294    0 Nov 10  2021 ticket4238791283685.txt
-rwx------ 1 4294967294 4294967294    0 Nov 10  2021 ticket4238791283686.txt
-rwx------ 1 4294967294 4294967294    0 Nov 10  2021 ticket4238791283687.txt
-rwx------ 1 4294967294 4294967294    0 Nov 10  2021 ticket4238791283688.txt
-rwx------ 1 4294967294 4294967294    0 Nov 10  2021 ticket4238791283689.txt
-rwx------ 1 4294967294 4294967294    0 Nov 10  2021 ticket4238791283690.txt
-rwx------ 1 4294967294 4294967294    0 Nov 10  2021 ticket4238791283691.txt
-rwx------ 1 4294967294 4294967294    0 Nov 10  2021 ticket4238791283692.txt
-rwx------ 1 4294967294 4294967294    0 Nov 10  2021 ticket4238791283693.txt
-rwx------ 1 4294967294 4294967294    0 Nov 10  2021 ticket4238791283694.txt
-rwx------ 1 4294967294 4294967294    0 Nov 10  2021 ticket4238791283695.txt
-rwx------ 1 4294967294 4294967294    0 Nov 10  2021 ticket4238791283696.txt
-rwx------ 1 4294967294 4294967294    0 Nov 10  2021 ticket4238791283697.txt
-rwx------ 1 4294967294 4294967294    0 Nov 10  2021 ticket4238791283698.txt
-rwx------ 1 4294967294 4294967294    0 Nov 10  2021 ticket4238791283699.txt
-rwx------ 1 4294967294 4294967294    0 Nov 10  2021 ticket4238791283700.txt
-rwx------ 1 4294967294 4294967294    0 Nov 10  2021 ticket4238791283701.txt
-rwx------ 1 4294967294 4294967294    0 Nov 10  2021 ticket4238791283702.txt
-rwx------ 1 4294967294 4294967294    0 Nov 10  2021 ticket4238791283703.txt
-rwx------ 1 4294967294 4294967294    0 Nov 10  2021 ticket4238791283704.txt
-rwx------ 1 4294967294 4294967294    0 Nov 10  2021 ticket4238791283705.txt
-rwx------ 1 4294967294 4294967294    0 Nov 10  2021 ticket4238791283706.txt
-rwx------ 1 4294967294 4294967294    0 Nov 10  2021 ticket4238791283707.txt
-rwx------ 1 4294967294 4294967294    0 Nov 10  2021 ticket4238791283708.txt
-rwx------ 1 4294967294 4294967294    0 Nov 10  2021 ticket4238791283709.txt
-rwx------ 1 4294967294 4294967294    0 Nov 10  2021 ticket4238791283710.txt
-rwx------ 1 4294967294 4294967294    0 Nov 10  2021 ticket4238791283711.txt
-rwx------ 1 4294967294 4294967294    0 Nov 10  2021 ticket4238791283712.txt
-rwx------ 1 4294967294 4294967294    0 Nov 10  2021 ticket4238791283713.txt
-rwx------ 1 4294967294 4294967294    0 Nov 10  2021 ticket4238791283714.txt
-rwx------ 1 4294967294 4294967294    0 Nov 10  2021 ticket4238791283715.txt
-rwx------ 1 4294967294 4294967294    0 Nov 10  2021 ticket4238791283716.txt
-rwx------ 1 4294967294 4294967294    0 Nov 10  2021 ticket4238791283717.txt
-rwx------ 1 4294967294 4294967294    0 Nov 10  2021 ticket4238791283718.txt
-rwx------ 1 4294967294 4294967294    0 Nov 10  2021 ticket4238791283719.txt
-rwx------ 1 4294967294 4294967294    0 Nov 10  2021 ticket4238791283720.txt
-rwx------ 1 4294967294 4294967294    0 Nov 10  2021 ticket4238791283721.txt
-rwx------ 1 4294967294 4294967294    0 Nov 10  2021 ticket4238791283722.txt
-rwx------ 1 4294967294 4294967294    0 Nov 10  2021 ticket4238791283723.txt
-rwx------ 1 4294967294 4294967294    0 Nov 10  2021 ticket4238791283724.txt
-rwx------ 1 4294967294 4294967294    0 Nov 10  2021 ticket4238791283725.txt
-rwx------ 1 4294967294 4294967294    0 Nov 10  2021 ticket4238791283726.txt
-rwx------ 1 4294967294 4294967294    0 Nov 10  2021 ticket4238791283727.txt
-rwx------ 1 4294967294 4294967294    0 Nov 10  2021 ticket4238791283728.txt
-rwx------ 1 4294967294 4294967294    0 Nov 10  2021 ticket4238791283729.txt
-rwx------ 1 4294967294 4294967294    0 Nov 10  2021 ticket4238791283730.txt
-rwx------ 1 4294967294 4294967294    0 Nov 10  2021 ticket4238791283731.txt
-rwx------ 1 4294967294 4294967294    0 Nov 10  2021 ticket4238791283732.txt
-rwx------ 1 4294967294 4294967294    0 Nov 10  2021 ticket4238791283733.txt
-rwx------ 1 4294967294 4294967294    0 Nov 10  2021 ticket4238791283734.txt
-rwx------ 1 4294967294 4294967294    0 Nov 10  2021 ticket4238791283735.txt
-rwx------ 1 4294967294 4294967294    0 Nov 10  2021 ticket4238791283736.txt
-rwx------ 1 4294967294 4294967294    0 Nov 10  2021 ticket4238791283737.txt
-rwx------ 1 4294967294 4294967294    0 Nov 10  2021 ticket4238791283738.txt
-rwx------ 1 4294967294 4294967294    0 Nov 10  2021 ticket4238791283739.txt
-rwx------ 1 4294967294 4294967294    0 Nov 10  2021 ticket4238791283740.txt
-rwx------ 1 4294967294 4294967294    0 Nov 10  2021 ticket4238791283741.txt
-rwx------ 1 4294967294 4294967294    0 Nov 10  2021 ticket4238791283742.txt
-rwx------ 1 4294967294 4294967294    0 Nov 10  2021 ticket4238791283743.txt
-rwx------ 1 4294967294 4294967294    0 Nov 10  2021 ticket4238791283744.txt
-rwx------ 1 4294967294 4294967294    0 Nov 10  2021 ticket4238791283745.txt
-rwx------ 1 4294967294 4294967294    0 Nov 10  2021 ticket4238791283746.txt
-rwx------ 1 4294967294 4294967294    0 Nov 10  2021 ticket4238791283747.txt
-rwx------ 1 4294967294 4294967294    0 Nov 10  2021 ticket4238791283748.txt
-rwx------ 1 4294967294 4294967294    0 Nov 10  2021 ticket4238791283749.txt
-rwx------ 1 4294967294 4294967294    0 Nov 10  2021 ticket4238791283750.txt
-rwx------ 1 4294967294 4294967294    0 Nov 10  2021 ticket4238791283751.txt
-rwx------ 1 4294967294 4294967294    0 Nov 10  2021 ticket4238791283752.txt
-rwx------ 1 4294967294 4294967294    0 Nov 10  2021 ticket4238791283753.txt
-rwx------ 1 4294967294 4294967294    0 Nov 10  2021 ticket4238791283754.txt
-rwx------ 1 4294967294 4294967294    0 Nov 10  2021 ticket4238791283755.txt
-rwx------ 1 4294967294 4294967294    0 Nov 10  2021 ticket4238791283756.txt
-rwx------ 1 4294967294 4294967294    0 Nov 10  2021 ticket4238791283757.txt
-rwx------ 1 4294967294 4294967294    0 Nov 10  2021 ticket4238791283758.txt
-rwx------ 1 4294967294 4294967294    0 Nov 10  2021 ticket4238791283759.txt
-rwx------ 1 4294967294 4294967294    0 Nov 10  2021 ticket4238791283760.txt
-rwx------ 1 4294967294 4294967294    0 Nov 10  2021 ticket4238791283761.txt
-rwx------ 1 4294967294 4294967294    0 Nov 10  2021 ticket4238791283762.txt
-rwx------ 1 4294967294 4294967294    0 Nov 10  2021 ticket4238791283763.txt
-rwx------ 1 4294967294 4294967294    0 Nov 10  2021 ticket4238791283764.txt
-rwx------ 1 4294967294 4294967294    0 Nov 10  2021 ticket4238791283765.txt
-rwx------ 1 4294967294 4294967294    0 Nov 10  2021 ticket4238791283766.txt
-rwx------ 1 4294967294 4294967294    0 Nov 10  2021 ticket4238791283767.txt
-rwx------ 1 4294967294 4294967294    0 Nov 10  2021 ticket4238791283768.txt
-rwx------ 1 4294967294 4294967294    0 Nov 10  2021 ticket4238791283769.txt
-rwx------ 1 4294967294 4294967294    0 Nov 10  2021 ticket4238791283770.txt
-rwx------ 1 4294967294 4294967294    0 Nov 10  2021 ticket4238791283771.txt
-rwx------ 1 4294967294 4294967294    0 Nov 10  2021 ticket4238791283772.txt
-rwx------ 1 4294967294 4294967294    0 Nov 10  2021 ticket4238791283773.txt
-rwx------ 1 4294967294 4294967294    0 Nov 10  2021 ticket4238791283774.txt
-rwx------ 1 4294967294 4294967294    0 Nov 10  2021 ticket4238791283775.txt
-rwx------ 1 4294967294 4294967294    0 Nov 10  2021 ticket4238791283776.txt
-rwx------ 1 4294967294 4294967294    0 Nov 10  2021 ticket4238791283777.txt
-rwx------ 1 4294967294 4294967294    0 Nov 10  2021 ticket4238791283778.txt
-rwx------ 1 4294967294 4294967294    0 Nov 10  2021 ticket4238791283779.txt
-rwx------ 1 4294967294 4294967294    0 Nov 10  2021 ticket4238791283780.txt
-rwx------ 1 4294967294 4294967294    0 Nov 10  2021 ticket4238791283781.txt
-rwx------ 1 4294967294 4294967294 1.3K Nov 10  2021 ticket4238791283782.txt
-rwx------ 1 4294967294 4294967294    0 Nov 10  2021 ticket4238791283783.txt
-rwx------ 1 4294967294 4294967294    0 Nov 10  2021 ticket4238791283784.txt
-rwx------ 1 4294967294 4294967294    0 Nov 10  2021 ticket4238791283785.txt
-rwx------ 1 4294967294 4294967294    0 Nov 10  2021 ticket4238791283786.txt
-rwx------ 1 4294967294 4294967294    0 Nov 10  2021 ticket4238791283787.txt
-rwx------ 1 4294967294 4294967294    0 Nov 10  2021 ticket4238791283788.txt
-rwx------ 1 4294967294 4294967294    0 Nov 10  2021 ticket4238791283789.txt
-rwx------ 1 4294967294 4294967294    0 Nov 10  2021 ticket4238791283790.txt
-rwx------ 1 4294967294 4294967294    0 Nov 10  2021 ticket4238791283791.txt
-rwx------ 1 4294967294 4294967294    0 Nov 10  2021 ticket4238791283792.txt
-rwx------ 1 4294967294 4294967294    0 Nov 10  2021 ticket4238791283793.txt
-rwx------ 1 4294967294 4294967294    0 Nov 10  2021 ticket4238791283794.txt
-rwx------ 1 4294967294 4294967294    0 Nov 10  2021 ticket4238791283795.txt
-rwx------ 1 4294967294 4294967294    0 Nov 10  2021 ticket4238791283796.txt
-rwx------ 1 4294967294 4294967294    0 Nov 10  2021 ticket4238791283797.txt
-rwx------ 1 4294967294 4294967294    0 Nov 10  2021 ticket4238791283798.txt
-rwx------ 1 4294967294 4294967294    0 Nov 10  2021 ticket4238791283799.txt
-rwx------ 1 4294967294 4294967294    0 Nov 10  2021 ticket4238791283800.txt
-rwx------ 1 4294967294 4294967294    0 Nov 10  2021 ticket4238791283801.txt
```
only one ticker that has the value with `1.3k` , i think it could lead somewhere let's check it 
```shell
sudo cat /mnt/e/file\ sampingan/htb/CPTS/footprinting/mediummachine/targetNFS/ticket4238791283782.txt
Conversation with InlaneFreight Ltd

Started on November 10, 2021 at 01:27 PM London time GMT (GMT+0200)
---
01:27 PM | Operator: Hello,.

So what brings you here today?
01:27 PM | alex: hello
01:27 PM | Operator: Hey alex!
01:27 PM | Operator: What do you need help with?
01:36 PM | alex: I run into an issue with the web config file on the system for the smtp server. do you mind to take a look at the config?
01:38 PM | Operator: Of course
01:42 PM | alex: here it is:

 1smtp {
 2    host=smtp.web.dev.inlanefreight.htb
 3    #port=25
 4    ssl=true
 5    user="alex"
 6    password="lol123!mD"
 7    from="alex.g@web.dev.inlanefreight.htb"
 8}
 9
10securesocial {
11
12    onLoginGoTo=/
13    onLogoutGoTo=/login
14    ssl=false
15
16    userpass {
17      withUserNameSupport=false
18      sendWelcomeEmail=true
19      enableGravatarSupport=true
20      signupSkipLogin=true
21      tokenDuration=60
22      tokenDeleteInterval=5
23      minimumPasswordLength=8
24      enableTokenJob=true
25      hasher=bcrypt
26      }
27
28     cookie {
29     #       name=id
30     #       path=/login
31     #       domain="10.129.2.59:9500"
32            httpOnly=true
33            makeTransient=false
34            absoluteTimeoutInMinutes=1440
35            idleTimeoutInMinutes=1440
36    }



---
```
okay in here we can see that's a credentials `alex@lol123!mD` from `alex.g@web.dev.inlanefreight.htb`, and since i already get the credentials , i think it's worth to check with smbclient 
```shell
smbclient -U alex -L //10.129.176.221/
Password for [WORKGROUP\alex]:

        Sharename       Type      Comment
        ---------       ----      -------
        ADMIN$          Disk      Remote Admin
        C$              Disk      Default share
        devshare        Disk
        IPC$            IPC       Remote IPC
        Users           Disk
SMB1 disabled -- no workgroup available
```
found some directory here , `devshare`, we try log in with the credentials that we just get 
```shell
mbclient -U alex //10.129.176.221/devshare
Password for [WORKGROUP\alex]:
Try "help" to get a list of possible commands.
smb: \>
```
in the smb i found ` important.txt                       A       16  Wed Nov 10 23:12:55 2021`, which have some value inside , worth to check 
```shell
smb: \> get important.txt
getting file \important.txt of size 16 as important.txt (0.0 KiloBytes/sec) (average 0.0 KiloBytes/sec)
```
```shell
cat important.txt
sa:87N1ns@slls83
```
hmm another credentials , hmm , i didnt know what this for , and since i stuck here , i try to retrace everything what have i done , first we check all the nmap result that i got before 
```shell
| smb2-time:
|   date: 2026-09-17T07:49:33
|_  start_date: N/A
|_clock-skew: mean: -34s, deviation: 0s, median: -34s
```
hmm smb i think it's worth to try to login with mssql 
```shell
python3 /home/nxz/.local/bin/mssqlclient.py sa:87N1ns@slls83@10.129.176.221 -windows-auth
Impacket v0.13.1 - Copyright Fortra, LLC and its affiliated companies

Traceback (most recent call last):
  File "/home/nxz/.local/bin/mssqlclient.py", line 94, in <module>
    ms_sql.connect()
  File "/home/nxz/.local/lib/python3.12/site-packages/impacket/tds.py", line 1271, in connect
    sock.connect(sa)
ConnectionRefusedError: [Errno 111] Connection refused

```

connection refuse , seems it another dead end ? , well ... no , looking back at nmap result i remember that the there's an open port in `3389 `
```shell
389/tcp open  ms-wbt-server Microsoft Terminal Services
| rdp-ntlm-info:
|   Target_Name: WINMEDIUM
|   NetBIOS_Domain_Name: WINMEDIUM
|   NetBIOS_Computer_Name: WINMEDIUM
|   DNS_Domain_Name: WINMEDIUM
|   DNS_Computer_Name: WINMEDIUM
|   Product_Version: 10.0.17763
|_  System_Time: 2026-09-17T07:49:30+00:00
| ssl-cert: Subject: commonName=WINMEDIUM
| Not valid before: 2026-09-16T07:40:48
|_Not valid after:  2027-03-18T07:40:48
|_ssl-date: 2026-09-17T07:49:39+00:00; -34s from scanner time.
Service Info: OS: Windows; CPE: cpe:/o:microsoft:windows
```
since im curios about this port let's just check it in google how to access to this port 
![[document_medium_htb_footprinting_1.png]]
and with ai power let's try to using xfreerdp 
```shell
 xfreerdp /u:alex /p:'lol123!mD' /v:10.129.176.221 /cert:ignore
[13:45:32:735] [2694:2695] [INFO][com.freerdp.gdi] - Local framebuffer format  PIXEL_FORMAT_BGRX32
[13:45:32:735] [2694:2695] [INFO][com.freerdp.gdi] - Remote framebuffer format PIXEL_FORMAT_BGRA32
[13:45:32:768] [2694:2695] [INFO][com.freerdp.channels.rdpsnd.client] - [static] Loaded fake backend for rdpsnd
[13:45:32:769] [2694:2695] [INFO][com.freerdp.channels.drdynvc.client] - Loading Dynamic Virtual Channel rdpgfx
[13:45:33:900] [2694:2695] [INFO][com.freerdp.client.x11] - Logon Error Info LOGON_FAILED_OTHER [LOGON_MSG_SESSION_CONTINUE]
```
![[document_medium_htb_footprinting_2.png]]
with the success to access the `Visual Desktop Windows` / another machine, i try to roaming around in the `visual desktop window` and found the `micosoft SQL server` app that we can run , by opening the page already give us the login credentials , i try with the credentials that i got didnt work it pop out this message 
![[document_medium_htb_footprinting_3.png]]
another dead end i guess, since i cannot run with normal user , maybe i can try it with `run as administrator`, just like linux
![[linuxmeme.png]]
after i run as administrator it goes the same popping the login with credentials , after entering the same password again it does give me an access .... , as an `admin`
![[documentation_medium_htb_footprinting_4.png]]
and by roaming around in this app that i didnt know how does even work in my terminal , i found `dbp.devsacc`
![[documentation_medium_htb_foorprinting_5.png]]
seems interesting enough then i open the table and found the flag in row 157 with user `HTB` 
![[documentation_medium_htb_footprinting_6.png]]