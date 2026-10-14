# Nmap Enumeration
```shell 
sudo nmap -sV -sC -T5 10.129.202.20
[sudo] password for nxz:
Starting Nmap 7.94SVN ( https://nmap.org ) at 2026-09-18 14:53 WIB
Nmap scan report for 10.129.202.20
Host is up (0.25s latency).
Not shown: 995 closed tcp ports (reset)
PORT    STATE SERVICE  VERSION
22/tcp  open  ssh      OpenSSH 8.2p1 Ubuntu 4ubuntu0.3 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey:
|   3072 3f:4c:8f:10:f1:ae:be:cd:31:24:7c:a1:4e:ab:84:6d (RSA)
|   256 7b:30:37:67:50:b9:ad:91:c0:8f:f7:02:78:3b:7c:02 (ECDSA)
|_  256 88:9e:0e:07:fe:ca:d0:5c:60:ab:cf:10:99:cd:6c:a7 (ED25519)
110/tcp open  pop3     Dovecot pop3d
| ssl-cert: Subject: commonName=NIXHARD
| Subject Alternative Name: DNS:NIXHARD
| Not valid before: 2021-11-10T01:30:25
|_Not valid after:  2031-11-08T01:30:25
|_pop3-capabilities: AUTH-RESP-CODE PIPELINING USER SASL(PLAIN) RESP-CODES CAPA STLS TOP UIDL
143/tcp open  imap     Dovecot imapd (Ubuntu)
| ssl-cert: Subject: commonName=NIXHARD
| Subject Alternative Name: DNS:NIXHARD
| Not valid before: 2021-11-10T01:30:25
|_Not valid after:  2031-11-08T01:30:25
|_ssl-date: TLS randomness does not represent time
|_imap-capabilities: OK capabilities have IMAP4rev1 IDLE ID ENABLE more post-login SASL-IR LOGIN-REFERRALS listed Pre-login STARTTLS AUTH=PLAINA0001 LITERAL+
993/tcp open  ssl/imap Dovecot imapd (Ubuntu)
|_ssl-date: TLS randomness does not represent time
|_imap-capabilities: OK capabilities have AUTH=PLAINA0001 IDLE ID ENABLE more SASL-IR LOGIN-REFERRALS post-login listed Pre-login LITERAL+ IMAP4rev1
| ssl-cert: Subject: commonName=NIXHARD
| Subject Alternative Name: DNS:NIXHARD
| Not valid before: 2021-11-10T01:30:25
|_Not valid after:  2031-11-08T01:30:25
995/tcp open  ssl/pop3 Dovecot pop3d
|_ssl-date: TLS randomness does not represent time
| ssl-cert: Subject: commonName=NIXHARD
| Subject Alternative Name: DNS:NIXHARD
| Not valid before: 2021-11-10T01:30:25
|_Not valid after:  2031-11-08T01:30:25
|_pop3-capabilities: SASL(PLAIN) USER AUTH-RESP-CODE PIPELINING CAPA RESP-CODES TOP UIDL
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 28.70 seconds
```
Honestly this machine is kinda hard since i keep forgotin what should i do , but i always want to learn again and again so that i could remember it , let's larp i guess , since in here i didnt know how to start with , i try to understand the `nmap` result first , i see that that port `993` and `995` is open i think i can try to enumerate it using `OpenSSL`
## OpenSSL enumeration
```shell
openssl s_client -connect 10.129.202.20:pop3s
CONNECTED(00000003)
Can't use SSL_get_servername
depth=0 CN = NIXHARD
verify error:num=18:self-signed certificate
verify return:1
depth=0 CN = NIXHARD
verify return:1
---
Certificate chain
 0 s:CN = NIXHARD
   i:CN = NIXHARD
   a:PKEY: rsaEncryption, 2048 (bit); sigalg: RSA-SHA256
   v:NotBefore: Nov 10 01:30:25 2021 GMT; NotAfter: Nov  8 01:30:25 2031 GMT
---
Server certificate
-----BEGIN CERTIFICATE-----
MIIC0zCCAbugAwIBAgIUC6tYfrtqQqCrhjYv11bUtaKet3EwDQYJKoZIhvcNAQEL
BQAwEjEQMA4GA1UEAwwHTklYSEFSRDAeFw0yMTExMTAwMTMwMjVaFw0zMTExMDgw
MTMwMjVaMBIxEDAOBgNVBAMMB05JWEhBUkQwggEiMA0GCSqGSIb3DQEBAQUAA4IB
DwAwggEKAoIBAQDEBpDfkH4Ro5ZXW44NvnF3N9lKz27V1hgRppyUk5y/SEPKt2zj
EU+r2tEHUeHoJHQZBbW0ybxh+X2H3ZPNEG9nV1GtFQfTBVcrUEpN5VV15aIbdh+q
j53pp/wcL/d8+Zg2ZAaVYWvQHVqtsAudQmynrV1MHA39A44fG3/SutKlurY8AKR0
MW5zMPtflMc/N3+lH8UUMBf2Q+zNSyZLiBEihxK3kfMW92HqWeh016egSIFuxUsH
kk4xpGmyG9NDYna47dQzoHCg+42KgqFvWrGw2nIccaEIX5XA8rU9u53C7EQzDzmQ
vAtHpKWBwNmiivxAz/QC7MPExWIWtZtOqxmfAgMBAAGjITAfMAkGA1UdEwQCMAAw
EgYDVR0RBAswCYIHTklYSEFSRDANBgkqhkiG9w0BAQsFAAOCAQEAG+Dm9pLJgNGC
X1YmznmtBUekhXMrU67tQl745fFasJQzIrDgVtK27fjAtQRwvIbDruSwTj47E7+O
XdS7qyjFNBerklWNq4fEAVI7BmkxnTS9542okA/+UmeG70LdKjzFS+LjjOnyWzTh
YwU8uUjLfnRca74kY0DkVHOIkwZQha0J+BrKSADq/zDjkG0g4v0vzHINOmHx9eiE
67NoJKJPY5S3RYWxl/4x8Kphx7PNJBPC75gYjlxxDhxdYu9a3daqJUa58/qOm6P8
w1P9nA6lkg7NopyqepulLAzIcqnTjb/nMD2Pd9b6vgWc3IqSfFreqjzshZ+FjNZo
zR+tR6z4TQ==
-----END CERTIFICATE-----
subject=CN = NIXHARD
issuer=CN = NIXHARD
---
No client certificate CA names sent
Peer signing digest: SHA256
Peer signature type: RSA-PSS
Server Temp Key: X25519, 253 bits
---
SSL handshake has read 1283 bytes and written 373 bytes
Verification error: self-signed certificate
---
New, TLSv1.3, Cipher is TLS_AES_256_GCM_SHA384
Server public key is 2048 bit
Secure Renegotiation IS NOT supported
Compression: NONE
Expansion: NONE
No ALPN negotiated
Early data was not sent
Verify return code: 18 (self-signed certificate)
---
---
Post-Handshake New Session Ticket arrived:
SSL-Session:
    Protocol  : TLSv1.3
    Cipher    : TLS_AES_256_GCM_SHA384
    Session-ID: D9DAB6A057EF783B035722CC1F78767D694FF7B46110AD9B57620902291779E9
    Session-ID-ctx:
    Resumption PSK: 13437D8F9C33FC1FAAAD9D4067E69FB568F45F7657506999B1D898BA0FAFD52D2AD0E29FEAF01E85E1C9ECEC379FFFE4
    PSK identity: None
    PSK identity hint: None
    SRP username: None
    TLS session ticket lifetime hint: 7200 (seconds)
    TLS session ticket:
    0000 - a0 2e 9e 7b a4 da b6 46-55 77 3c ba cb bf 89 6e   ...{...FUw<....n
    0010 - ed 7d 2f f3 cd bb 77 e0-08 9c 4c 9f db d1 44 f1   .}/...w...L...D.
    0020 - 6b c5 ca 85 1e 6e 63 07-3f 4a 27 6b 86 83 03 da   k....nc.?J'k....
    0030 - 0b 73 70 46 10 5e fa c9-bb d0 ea 76 ba c4 a0 d2   .spF.^.....v....
    0040 - 90 13 6b 6f 90 1d 49 6e-0a 0b cb 50 6f ca 11 b6   ..ko..In...Po...
    0050 - 34 6c d3 b7 ab 61 7a a9-94 99 3c 9e 45 11 ab f9   4l...az...<.E...
    0060 - f3 b1 23 7d f7 73 92 8e-c1 84 e3 ad da 4c 5e 30   ..#}.s.......L^0
    0070 - 2b eb c7 f4 ce d4 50 8e-25 32 51 b9 fd 6a ed 21   +.....P.%2Q..j.!
    0080 - af 8f 85 62 ab b6 e9 8b-5a 89 e7 7c 35 67 00 cd   ...b....Z..|5g..
    0090 - 6a 3c 5c 0f d6 37 50 5e-a2 d1 1c aa 82 68 27 43   j<\..7P^.....h'C
    00a0 - f2 48 85 7f e8 9e 32 0b-fe 2a e0 a5 8d ea 5f 41   .H....2..*...._A
    00b0 - af d1 e7 74 45 36 c8 96-bd 30 2a 33 87 41 ee 82   ...tE6...0*3.A..

    Start Time: 1789719061
    Timeout   : 7200 (sec)
    Verify return code: 18 (self-signed certificate)
    Extended master secret: no
    Max Early Data: 0
---
read R BLOCK
---
Post-Handshake New Session Ticket arrived:
SSL-Session:
    Protocol  : TLSv1.3
    Cipher    : TLS_AES_256_GCM_SHA384
    Session-ID: 49F36DFF0D4A299D218DE7A12E9EFB0F10A0D54885EEF3A3BD14F87B47A6BD92
    Session-ID-ctx:
    Resumption PSK: F14FF3144F367F63D2C13DEE7373561FB6B14C9DC3C973492B960FD891A0DB847D20172962CDD42D80DFE98C971FCEE6
    PSK identity: None
    PSK identity hint: None
    SRP username: None
    TLS session ticket lifetime hint: 7200 (seconds)
    TLS session ticket:
    0000 - a0 2e 9e 7b a4 da b6 46-55 77 3c ba cb bf 89 6e   ...{...FUw<....n
    0010 - 4e 46 a5 df 28 1d 5d 2b-4d 38 79 f5 7c 0f 4a 06   NF..(.]+M8y.|.J.
    0020 - a4 99 d6 66 ad 94 03 95-a5 43 f8 3b 5a 18 fa 70   ...f.....C.;Z..p
    0030 - f5 a0 f3 68 24 76 9c 41-04 3a 8b 2c 4b 6d 86 8a   ...h$v.A.:.,Km..
    0040 - 59 a4 19 bd 54 00 d0 a6-22 c2 65 f9 4d 6f 1d ab   Y...T...".e.Mo..
    0050 - 43 0a 67 5d 1d 03 7c f2-b5 f6 e6 00 d4 60 64 4d   C.g]..|......`dM
    0060 - 87 c8 2a 40 1e de dd 32-af 87 8a 38 ea 4c 83 dd   ..*@...2...8.L..
    0070 - cd 89 7c f9 ab c4 61 69-23 b5 bc 82 88 51 48 29   ..|...ai#....QH)
    0080 - a6 60 8d 8c a7 93 55 ab-f0 7e ef 02 52 02 ea 32   .`....U..~..R..2
    0090 - ec 06 3c 7f c1 a4 b8 b6-8e 5f c7 8d 43 7a d0 76   ..<......_..Cz.v
    00a0 - 70 1b a3 4b 34 d3 0e 57-87 7c 9c 0f 3f 5e e4 db   p..K4..W.|..?^..
    00b0 - 84 1a ec c2 e5 42 e0 dd-48 82 33 63 25 9d 73 2a   .....B..H.3c%.s*

    Start Time: 1789719061
    Timeout   : 7200 (sec)
    Verify return code: 18 (self-signed certificate)
    Extended master secret: no
    Max Early Data: 0
---
read R BLOCK
+OK Dovecot (Ubuntu) ready.
^Z
[1]+  Stopped                 openssl s_client -connect 10.129.202.20:pop3s
```
i try with `pop3s` didn't found anything interesting here so i try with `imaps`
```shell
openssl s_client -connect 10.129.202.20:imaps
CONNECTED(00000003)
Can't use SSL_get_servername
depth=0 CN = NIXHARD
verify error:num=18:self-signed certificate
verify return:1
depth=0 CN = NIXHARD
verify return:1
---
Certificate chain
 0 s:CN = NIXHARD
   i:CN = NIXHARD
   a:PKEY: rsaEncryption, 2048 (bit); sigalg: RSA-SHA256
   v:NotBefore: Nov 10 01:30:25 2021 GMT; NotAfter: Nov  8 01:30:25 2031 GMT
---
Server certificate
-----BEGIN CERTIFICATE-----
MIIC0zCCAbugAwIBAgIUC6tYfrtqQqCrhjYv11bUtaKet3EwDQYJKoZIhvcNAQEL
BQAwEjEQMA4GA1UEAwwHTklYSEFSRDAeFw0yMTExMTAwMTMwMjVaFw0zMTExMDgw
MTMwMjVaMBIxEDAOBgNVBAMMB05JWEhBUkQwggEiMA0GCSqGSIb3DQEBAQUAA4IB
DwAwggEKAoIBAQDEBpDfkH4Ro5ZXW44NvnF3N9lKz27V1hgRppyUk5y/SEPKt2zj
EU+r2tEHUeHoJHQZBbW0ybxh+X2H3ZPNEG9nV1GtFQfTBVcrUEpN5VV15aIbdh+q
j53pp/wcL/d8+Zg2ZAaVYWvQHVqtsAudQmynrV1MHA39A44fG3/SutKlurY8AKR0
MW5zMPtflMc/N3+lH8UUMBf2Q+zNSyZLiBEihxK3kfMW92HqWeh016egSIFuxUsH
kk4xpGmyG9NDYna47dQzoHCg+42KgqFvWrGw2nIccaEIX5XA8rU9u53C7EQzDzmQ
vAtHpKWBwNmiivxAz/QC7MPExWIWtZtOqxmfAgMBAAGjITAfMAkGA1UdEwQCMAAw
EgYDVR0RBAswCYIHTklYSEFSRDANBgkqhkiG9w0BAQsFAAOCAQEAG+Dm9pLJgNGC
X1YmznmtBUekhXMrU67tQl745fFasJQzIrDgVtK27fjAtQRwvIbDruSwTj47E7+O
XdS7qyjFNBerklWNq4fEAVI7BmkxnTS9542okA/+UmeG70LdKjzFS+LjjOnyWzTh
YwU8uUjLfnRca74kY0DkVHOIkwZQha0J+BrKSADq/zDjkG0g4v0vzHINOmHx9eiE
67NoJKJPY5S3RYWxl/4x8Kphx7PNJBPC75gYjlxxDhxdYu9a3daqJUa58/qOm6P8
w1P9nA6lkg7NopyqepulLAzIcqnTjb/nMD2Pd9b6vgWc3IqSfFreqjzshZ+FjNZo
zR+tR6z4TQ==
-----END CERTIFICATE-----
subject=CN = NIXHARD
issuer=CN = NIXHARD
---
No client certificate CA names sent
Peer signing digest: SHA256
Peer signature type: RSA-PSS
Server Temp Key: X25519, 253 bits
---
SSL handshake has read 1283 bytes and written 373 bytes
Verification error: self-signed certificate
---
New, TLSv1.3, Cipher is TLS_AES_256_GCM_SHA384
Server public key is 2048 bit
Secure Renegotiation IS NOT supported
Compression: NONE
Expansion: NONE
No ALPN negotiated
Early data was not sent
Verify return code: 18 (self-signed certificate)
---
---
Post-Handshake New Session Ticket arrived:
SSL-Session:
    Protocol  : TLSv1.3
    Cipher    : TLS_AES_256_GCM_SHA384
    Session-ID: 1CBDFA8741F31FB357AF60CF61DB3692E8E49112BBD0A46EA64B433EEC452588
    Session-ID-ctx:
    Resumption PSK: 882769126C6BC4D3649781021F89496A7DA072FA857AE7C55DDE86E3FCDEF6B8FCF33E6CA0B1890975B40356F7C879FB
    PSK identity: None
    PSK identity hint: None
    SRP username: None
    TLS session ticket lifetime hint: 7200 (seconds)
    TLS session ticket:
    0000 - de 1a 2d 34 62 57 60 52-90 4c bb bc 01 5d 2f 59   ..-4bW`R.L...]/Y
    0010 - 1c 8d 53 ae 9d a8 fa 2d-d5 bc 52 72 ea f1 e5 be   ..S....-..Rr....
    0020 - d2 68 1e c5 7d dc 4e 1d-b9 b4 41 bc ff f0 e7 6a   .h..}.N...A....j
    0030 - 02 44 52 15 d6 08 e1 46-89 ae db f8 74 23 9d aa   .DR....F....t#..
    0040 - a5 01 e1 f1 de ad f3 5f-5b 83 cc d2 42 55 17 e6   ......._[...BU..
    0050 - bf 3a c0 73 83 a0 41 d0-84 f4 55 db a8 e2 54 49   .:.s..A...U...TI
    0060 - 02 30 2c ce 09 c5 19 0d-6d dd ae ea 60 43 b1 c7   .0,.....m...`C..
    0070 - c4 d9 f9 ca f7 07 3c 40-bc 7a 8b ea 7a e4 4c 42   ......<@.z..z.LB
    0080 - a6 d1 41 b5 52 42 23 f4-33 e9 63 8f 51 2f 31 85   ..A.RB#.3.c.Q/1.
    0090 - 1c b5 5c a7 78 c8 f3 7d-04 ae 51 a3 bf 14 90 a8   ..\.x..}..Q.....
    00a0 - 3e 79 34 10 bc 13 50 cc-af e0 ab 9f dd a0 9c 2e   >y4...P.........
    00b0 - 40 c1 e8 13 00 3a 25 0d-af 2c 8a 95 ea 7f 37 01   @....:%..,....7.

    Start Time: 1789719133
    Timeout   : 7200 (sec)
    Verify return code: 18 (self-signed certificate)
    Extended master secret: no
    Max Early Data: 0
---
read R BLOCK
---
Post-Handshake New Session Ticket arrived:
SSL-Session:
    Protocol  : TLSv1.3
    Cipher    : TLS_AES_256_GCM_SHA384
    Session-ID: D9F5E40D2896D2B01F81B5F594B7EB2E38AB061859F6948231A43E6206E7483A
    Session-ID-ctx:
    Resumption PSK: 02911FF088CA6B643210FCC5635A112690460A11F5CA4636970BB8D3CC5A0A1ED8ED5CC6441459B7469F67E6B7537257
    PSK identity: None
    PSK identity hint: None
    SRP username: None
    TLS session ticket lifetime hint: 7200 (seconds)
    TLS session ticket:
    0000 - de 1a 2d 34 62 57 60 52-90 4c bb bc 01 5d 2f 59   ..-4bW`R.L...]/Y
    0010 - 0f f7 45 df db 18 f2 92-1b c9 c7 ae cd b4 7f 37   ..E............7
    0020 - 85 e0 6a 5b 7b 78 15 33-6f 25 e9 f0 df 80 ed 8b   ..j[{x.3o%......
    0030 - 17 45 1a b9 63 5b 3e 01-23 42 b1 2b 53 69 2a 16   .E..c[>.#B.+Si*.
    0040 - aa be ea c2 15 9e af d0-e3 32 64 4e 99 28 27 c3   .........2dN.('.
    0050 - 14 d2 09 c2 02 f9 9b cd-50 6b 86 c9 29 35 ad 9e   ........Pk..)5..
    0060 - be 9e 81 27 6e c9 67 8d-ac 50 05 a2 de 3d a1 58   ...'n.g..P...=.X
    0070 - 3c 48 4c 35 6b 35 12 e0-67 a2 e0 10 f1 94 c0 44   <HL5k5..g......D
    0080 - 99 a7 83 ee 8b fa 5c 3b-08 89 f5 ae cd 67 0d 2a   ......\;.....g.*
    0090 - dd a8 9d c9 97 a3 0b 96-a6 79 48 0c 29 09 b2 88   .........yH.)...
    00a0 - 0c 44 94 19 95 47 9d c5-97 3c ac ec 18 cb 81 26   .D...G...<.....&
    00b0 - 01 f4 97 66 dc ed b3 21-89 52 05 45 c0 16 3b b2   ...f...!.R.E..;.

    Start Time: 1789719133
    Timeout   : 7200 (sec)
    Verify return code: 18 (self-signed certificate)
    Extended master secret: no
    Max Early Data: 0
---
read R BLOCK
* OK [CAPABILITY IMAP4rev1 SASL-IR LOGIN-REFERRALS ID ENABLE IDLE LITERAL+ AUTH=PLAIN] Dovecot (Ubuntu) ready.
```

i found nothing interesting here, but since i check the `nmap` result i felt something was not right , like it didn't show anything much in my opinion . So i decided to try another nmap with different command 
## Second try Nmap
```shell
sudo nmap -sU --top-ports 100 10.129.202.20
Starting Nmap 7.94SVN ( https://nmap.org ) at 2026-09-18 15:30 WIB
Stats: 0:00:02 elapsed; 0 hosts completed (1 up), 1 undergoing UDP Scan
UDP Scan Timing: About 8.00% done; ETC: 15:30 (0:00:23 remaining)
Nmap scan report for 10.129.202.20
Host is up (0.23s latency).
Not shown: 97 closed udp ports (port-unreach)
PORT    STATE         SERVICE
68/udp  open|filtered dhcpc
161/udp open          snmp
631/udp open|filtered ipp

Nmap done: 1 IP address (1 host up) scanned in 107.71 seconds
```
well3 i found something that i didnt expect that there's 3 port that didn't show at the first result in here we can see that port `68`,`161`,`631` . SNMP one of the most hardest thing i ever try to understand , anyway , after i see that `161` is up i think is worth to enumerate with snmpwalk, 
### SNMPWALK enumeration 
```shell 
 snmpwalk -v2c -c public 10.129.202.20
Timeout: No Response from 10.129.202.20
```
well didn't work , dead end i guess, i think i remember something since in [SNMP HOST BASED ENUMERATION](https://academy.hackthebox.com/app/module/112/section/1075) i learn that to find if it's `public` or not we can use `onesixtyone` tool to find it out 
#### ONESIXTYONE
```shell 
 onesixtyone -c /home/nxz/seclists/Discovery/SNMP/snmp.txt 10.129.202.20
Scanning 1 hosts, 3219 communities
10.129.202.20 [backup] Linux NIXHARD 5.4.0-90-generic #101-Ubuntu SMP Fri Oct 15 20:00:55 UTC 2021 x86_64
```
okay in here i realize that the community strings is `backup` not `public`, then i give another try to enumerate with `Snmpwalk`
#### SNMPWALK again && thinking again
```shell 
 snmpwalk -v2c -c backup 10.129.202.20
iso.3.6.1.2.1.1.1.0 = STRING: "Linux NIXHARD 5.4.0-90-generic #101-Ubuntu SMP Fri Oct 15 20:00:55 UTC 2021 x86_64"
iso.3.6.1.2.1.1.2.0 = OID: iso.3.6.1.4.1.8072.3.2.10
iso.3.6.1.2.1.1.3.0 = Timeticks: (270527) 0:45:05.27
iso.3.6.1.2.1.1.4.0 = STRING: "Admin <tech@inlanefreight.htb>"
iso.3.6.1.2.1.1.5.0 = STRING: "NIXHARD"
iso.3.6.1.2.1.1.6.0 = STRING: "Inlanefreight"
iso.3.6.1.2.1.1.7.0 = INTEGER: 72
iso.3.6.1.2.1.1.8.0 = Timeticks: (36) 0:00:00.36
iso.3.6.1.2.1.1.9.1.2.1 = OID: iso.3.6.1.6.3.10.3.1.1
iso.3.6.1.2.1.1.9.1.2.2 = OID: iso.3.6.1.6.3.11.3.1.1
iso.3.6.1.2.1.1.9.1.2.3 = OID: iso.3.6.1.6.3.15.2.1.1
iso.3.6.1.2.1.1.9.1.2.4 = OID: iso.3.6.1.6.3.1
iso.3.6.1.2.1.1.9.1.2.5 = OID: iso.3.6.1.6.3.16.2.2.1
iso.3.6.1.2.1.1.9.1.2.6 = OID: iso.3.6.1.2.1.49
iso.3.6.1.2.1.1.9.1.2.7 = OID: iso.3.6.1.2.1.4
iso.3.6.1.2.1.1.9.1.2.8 = OID: iso.3.6.1.2.1.50
iso.3.6.1.2.1.1.9.1.2.9 = OID: iso.3.6.1.6.3.13.3.1.3
iso.3.6.1.2.1.1.9.1.2.10 = OID: iso.3.6.1.2.1.92
iso.3.6.1.2.1.1.9.1.3.1 = STRING: "The SNMP Management Architecture MIB."
iso.3.6.1.2.1.1.9.1.3.2 = STRING: "The MIB for Message Processing and Dispatching."
iso.3.6.1.2.1.1.9.1.3.3 = STRING: "The management information definitions for the SNMP User-based Security Model."
iso.3.6.1.2.1.1.9.1.3.4 = STRING: "The MIB module for SNMPv2 entities"
iso.3.6.1.2.1.1.9.1.3.5 = STRING: "View-based Access Control Model for SNMP."
iso.3.6.1.2.1.1.9.1.3.6 = STRING: "The MIB module for managing TCP implementations"
iso.3.6.1.2.1.1.9.1.3.7 = STRING: "The MIB module for managing IP and ICMP implementations"
iso.3.6.1.2.1.1.9.1.3.8 = STRING: "The MIB module for managing UDP implementations"
iso.3.6.1.2.1.1.9.1.3.9 = STRING: "The MIB modules for managing SNMP Notification, plus filtering."
iso.3.6.1.2.1.1.9.1.3.10 = STRING: "The MIB module for logging SNMP Notifications."
iso.3.6.1.2.1.1.9.1.4.1 = Timeticks: (35) 0:00:00.35
iso.3.6.1.2.1.1.9.1.4.2 = Timeticks: (36) 0:00:00.36
iso.3.6.1.2.1.1.9.1.4.3 = Timeticks: (36) 0:00:00.36
iso.3.6.1.2.1.1.9.1.4.4 = Timeticks: (36) 0:00:00.36
iso.3.6.1.2.1.1.9.1.4.5 = Timeticks: (36) 0:00:00.36
iso.3.6.1.2.1.1.9.1.4.6 = Timeticks: (36) 0:00:00.36
iso.3.6.1.2.1.1.9.1.4.7 = Timeticks: (36) 0:00:00.36
iso.3.6.1.2.1.1.9.1.4.8 = Timeticks: (36) 0:00:00.36
iso.3.6.1.2.1.1.9.1.4.9 = Timeticks: (36) 0:00:00.36
iso.3.6.1.2.1.1.9.1.4.10 = Timeticks: (36) 0:00:00.36
iso.3.6.1.2.1.25.1.1.0 = Timeticks: (272104) 0:45:21.04
iso.3.6.1.2.1.25.1.2.0 = Hex-STRING: 07 EA 09 12 08 22 12 00 2B 00 00
iso.3.6.1.2.1.25.1.3.0 = INTEGER: 393216
iso.3.6.1.2.1.25.1.4.0 = STRING: "BOOT_IMAGE=/vmlinuz-5.4.0-90-generic root=/dev/mapper/ubuntu--vg-ubuntu--lv ro ipv6.disable=1 maybe-ubiquity
"
iso.3.6.1.2.1.25.1.5.0 = Gauge32: 0
iso.3.6.1.2.1.25.1.6.0 = Gauge32: 159
iso.3.6.1.2.1.25.1.7.0 = INTEGER: 0
iso.3.6.1.2.1.25.1.7.1.1.0 = INTEGER: 1
iso.3.6.1.2.1.25.1.7.1.2.1.2.6.66.65.67.75.85.80 = STRING: "/opt/tom-recovery.sh"
iso.3.6.1.2.1.25.1.7.1.2.1.3.6.66.65.67.75.85.80 = STRING: "tom NMds732Js2761"
iso.3.6.1.2.1.25.1.7.1.2.1.4.6.66.65.67.75.85.80 = ""
iso.3.6.1.2.1.25.1.7.1.2.1.5.6.66.65.67.75.85.80 = INTEGER: 5
iso.3.6.1.2.1.25.1.7.1.2.1.6.6.66.65.67.75.85.80 = INTEGER: 1
iso.3.6.1.2.1.25.1.7.1.2.1.7.6.66.65.67.75.85.80 = INTEGER: 1
iso.3.6.1.2.1.25.1.7.1.2.1.20.6.66.65.67.75.85.80 = INTEGER: 4
iso.3.6.1.2.1.25.1.7.1.2.1.21.6.66.65.67.75.85.80 = INTEGER: 1
iso.3.6.1.2.1.25.1.7.1.3.1.1.6.66.65.67.75.85.80 = STRING: "chpasswd: (user tom) pam_chauthtok() failed, error:"
iso.3.6.1.2.1.25.1.7.1.3.1.2.6.66.65.67.75.85.80 = STRING: "chpasswd: (user tom) pam_chauthtok() failed, error:
Authentication token manipulation error
chpasswd: (line 1, user tom) password not changed
Changing password for tom."
iso.3.6.1.2.1.25.1.7.1.3.1.3.6.66.65.67.75.85.80 = INTEGER: 4
iso.3.6.1.2.1.25.1.7.1.3.1.4.6.66.65.67.75.85.80 = INTEGER: 1
iso.3.6.1.2.1.25.1.7.1.4.1.2.6.66.65.67.75.85.80.1 = STRING: "chpasswd: (user tom) pam_chauthtok() failed, error:"
iso.3.6.1.2.1.25.1.7.1.4.1.2.6.66.65.67.75.85.80.2 = STRING: "Authentication token manipulation error"
iso.3.6.1.2.1.25.1.7.1.4.1.2.6.66.65.67.75.85.80.3 = STRING: "chpasswd: (line 1, user tom) password not changed"
iso.3.6.1.2.1.25.1.7.1.4.1.2.6.66.65.67.75.85.80.4 = STRING: "Changing password for tom."
iso.3.6.1.2.1.25.1.7.1.4.1.2.6.66.65.67.75.85.80.4 = No more variables left in this MIB View (It is past the end of the MIB tree)
```

well3 , in here i can see that there's a string that shows credentials , i think it must be login to something , i try to login using SSH but didn't work . Another dead end  .......

Well im not giving up in here , i must say that openssl must do something in here , cause i feel that just by why they put `110`, `143` , `993` , `995` with no purpose , or maybe i just dumb , cause in here i already assuming , but why not give it a try 

Since i already have some credentials to use and i didn't know how to use the command inside the openssl i try to google it to find out how to use the tool 
![screenshot](documentation/documentation_hard_htb_footprinting_1.png)
Owh we can login inside `openssl` , well then let's give it a try 
```shell 
openssl s_client -connect 10.129.202.20:imaps
CONNECTED(00000003)
Can't use SSL_get_servername
depth=0 CN = NIXHARD
verify error:num=18:self-signed certificate
verify return:1
depth=0 CN = NIXHARD
verify return:1
---
Certificate chain
 0 s:CN = NIXHARD
   i:CN = NIXHARD
   a:PKEY: rsaEncryption, 2048 (bit); sigalg: RSA-SHA256
   v:NotBefore: Nov 10 01:30:25 2021 GMT; NotAfter: Nov  8 01:30:25 2031 GMT
---
Server certificate
-----BEGIN CERTIFICATE-----
MIIC0zCCAbugAwIBAgIUC6tYfrtqQqCrhjYv11bUtaKet3EwDQYJKoZIhvcNAQEL
BQAwEjEQMA4GA1UEAwwHTklYSEFSRDAeFw0yMTExMTAwMTMwMjVaFw0zMTExMDgw
MTMwMjVaMBIxEDAOBgNVBAMMB05JWEhBUkQwggEiMA0GCSqGSIb3DQEBAQUAA4IB
DwAwggEKAoIBAQDEBpDfkH4Ro5ZXW44NvnF3N9lKz27V1hgRppyUk5y/SEPKt2zj
EU+r2tEHUeHoJHQZBbW0ybxh+X2H3ZPNEG9nV1GtFQfTBVcrUEpN5VV15aIbdh+q
j53pp/wcL/d8+Zg2ZAaVYWvQHVqtsAudQmynrV1MHA39A44fG3/SutKlurY8AKR0
MW5zMPtflMc/N3+lH8UUMBf2Q+zNSyZLiBEihxK3kfMW92HqWeh016egSIFuxUsH
kk4xpGmyG9NDYna47dQzoHCg+42KgqFvWrGw2nIccaEIX5XA8rU9u53C7EQzDzmQ
vAtHpKWBwNmiivxAz/QC7MPExWIWtZtOqxmfAgMBAAGjITAfMAkGA1UdEwQCMAAw
EgYDVR0RBAswCYIHTklYSEFSRDANBgkqhkiG9w0BAQsFAAOCAQEAG+Dm9pLJgNGC
X1YmznmtBUekhXMrU67tQl745fFasJQzIrDgVtK27fjAtQRwvIbDruSwTj47E7+O
XdS7qyjFNBerklWNq4fEAVI7BmkxnTS9542okA/+UmeG70LdKjzFS+LjjOnyWzTh
YwU8uUjLfnRca74kY0DkVHOIkwZQha0J+BrKSADq/zDjkG0g4v0vzHINOmHx9eiE
67NoJKJPY5S3RYWxl/4x8Kphx7PNJBPC75gYjlxxDhxdYu9a3daqJUa58/qOm6P8
w1P9nA6lkg7NopyqepulLAzIcqnTjb/nMD2Pd9b6vgWc3IqSfFreqjzshZ+FjNZo
zR+tR6z4TQ==
-----END CERTIFICATE-----
subject=CN = NIXHARD
issuer=CN = NIXHARD
---
No client certificate CA names sent
Peer signing digest: SHA256
Peer signature type: RSA-PSS
Server Temp Key: X25519, 253 bits
---
SSL handshake has read 1283 bytes and written 373 bytes
Verification error: self-signed certificate
---
New, TLSv1.3, Cipher is TLS_AES_256_GCM_SHA384
Server public key is 2048 bit
Secure Renegotiation IS NOT supported
Compression: NONE
Expansion: NONE
No ALPN negotiated
Early data was not sent
Verify return code: 18 (self-signed certificate)
---
---
Post-Handshake New Session Ticket arrived:
SSL-Session:
    Protocol  : TLSv1.3
    Cipher    : TLS_AES_256_GCM_SHA384
    Session-ID: 1BF13668D2990C9185DF480322C3352A9B4A07AD77904F72D169A3C4D17CCB66
    Session-ID-ctx:
    Resumption PSK: AC907EA71F52BA7524751CF2638853E6E30B11727F4D725A0C7603D321E7D0D45C52610075890C5538BF495DE0EC05B9
    PSK identity: None
    PSK identity hint: None
    SRP username: None
    TLS session ticket lifetime hint: 7200 (seconds)
    TLS session ticket:
    0000 - df a7 09 fb ab 67 85 ef-93 78 67 d2 5c 9a c5 92   .....g...xg.\...
    0010 - 50 45 a4 22 5a 29 91 7e-25 f2 e7 e1 2a ba dc 17   PE."Z).~%...*...
    0020 - df 20 66 44 26 bd a6 62-d5 10 ed d8 62 14 45 53   . fD&..b....b.ES
    0030 - a3 5e b4 3b 2d 8b ab bc-15 a3 e6 47 81 1e df cf   .^.;-......G....
    0040 - 0a 1e 62 b8 bb ee 40 13-47 f4 ad 20 b4 8a 9b 2b   ..b...@.G.. ...+
    0050 - 66 ad 6e 48 e3 01 22 e2-0d da fb e2 be 7f cf 0e   f.nH..".........
    0060 - b5 c1 b3 b0 86 f2 42 a1-ed 7a a3 a0 b0 3c d3 83   ......B..z...<..
    0070 - 73 9b 49 77 b5 6a 40 da-2e 9a a4 f0 70 cf af 41   s.Iw.j@.....p..A
    0080 - 5c 8f 77 68 db 16 cf d8-b1 3d d3 ef d8 6f af 87   \.wh.....=...o..
    0090 - 3b 6a bf e1 20 44 b1 a0-68 37 7f f3 74 94 05 5b   ;j.. D..h7..t..[
    00a0 - a9 5c 24 5c 55 b1 16 62-26 45 72 05 b4 e5 b0 9f   .\$\U..b&Er.....
    00b0 - ed 92 68 3c 79 b3 b2 0e-b1 91 e3 89 e7 ba ed 92   ..h<y...........

    Start Time: 1789721226
    Timeout   : 7200 (sec)
    Verify return code: 18 (self-signed certificate)
    Extended master secret: no
    Max Early Data: 0
---
read R BLOCK
---
Post-Handshake New Session Ticket arrived:
SSL-Session:
    Protocol  : TLSv1.3
    Cipher    : TLS_AES_256_GCM_SHA384
    Session-ID: 90DC6F87678065DC54041857B22AA61EC84B2B16C80DDDC88F6BD976B3C2C2B6
    Session-ID-ctx:
    Resumption PSK: 5D87995CCEB465CEB1D13FCE9997AF95B3C8CA65D03A05E4DEBA05F924BE6BEE627ADB457FB8CE652ECAAB8B4F5751C9
    PSK identity: None
    PSK identity hint: None
    SRP username: None
    TLS session ticket lifetime hint: 7200 (seconds)
    TLS session ticket:
    0000 - df a7 09 fb ab 67 85 ef-93 78 67 d2 5c 9a c5 92   .....g...xg.\...
    0010 - 24 f2 ea d7 ec e0 f3 d8-f8 20 e8 77 be 7c 5c 5b   $........ .w.|\[
    0020 - a6 fd 17 8f 4e 2d e6 01-d9 a7 d7 7d 91 cf ca 8f   ....N-.....}....
    0030 - d3 5c 6e 53 21 40 91 2d-67 1e ae 31 f0 d0 0d 60   .\nS!@.-g..1...`
    0040 - 1c 75 5c 71 5f 94 44 ac-1f 2d e7 ad 8e 46 a2 0c   .u\q_.D..-...F..
    0050 - 1b e5 54 39 89 2a 78 06-dc af ee 67 35 80 ba eb   ..T9.*x....g5...
    0060 - ce 87 7b 40 d0 87 0f a5-96 88 be b9 18 30 9a 30   ..{@.........0.0
    0070 - ac 8c ad 28 1c 35 6c 95-fb 03 e1 6a 27 81 ac a2   ...(.5l....j'...
    0080 - b0 00 3f a3 7d 66 a8 dc-bc 0a 5a b9 20 41 ea 43   ..?.}f....Z. A.C
    0090 - be 08 eb 82 dd c5 43 02-af f7 14 66 01 f8 7c 90   ......C....f..|.
    00a0 - 86 34 d0 13 4e 54 51 73-a9 cc dc 2c d4 a3 d9 49   .4..NTQs...,...I
    00b0 - 25 3a 5f 11 16 c5 77 2c-71 50 16 26 f5 8a 40 d8   %:_...w,qP.&..@.

    Start Time: 1789721226
    Timeout   : 7200 (sec)
    Verify return code: 18 (self-signed certificate)
    Extended master secret: no
    Max Early Data: 0
---
read R BLOCK
* OK [CAPABILITY IMAP4rev1 SASL-IR LOGIN-REFERRALS ID ENABLE IDLE LITERAL+ AUTH=PLAIN] Dovecot (Ubuntu) ready.
a LOGIN tom NMds732Js2761
a OK [CAPABILITY IMAP4rev1 SASL-IR LOGIN-REFERRALS ID ENABLE IDLE SORT SORT=DISPLAY THREAD=REFERENCES THREAD=REFS THREAD=ORDEREDSUBJECT MULTIAPPEND URL-PARTIAL CATENATE UNSELECT CHILDREN NAMESPACE UIDPLUS LIST-EXTENDED I18NLEVEL=1 CONDSTORE QRESYNC ESEARCH ESORT SEARCHRES WITHIN CONTEXT=SEARCH LIST-STATUS BINARY MOVE SNIPPET=FUZZY PREVIEW=FUZZY LITERAL+ NOTIFY SPECIAL-USE] Logged in
```
ofc i keep forgeting that this is not bash / shell i want to list all path so that i could see what's inside 
```shell 
a LIST "" "*"
* LIST (\HasNoChildren) "." Notes
* LIST (\HasNoChildren) "." Meetings
* LIST (\HasNoChildren \UnMarked) "." Important
* LIST (\HasNoChildren) "." INBOX
a OK List completed (0.001 + 0.000 secs).
```
well there's a `notes`, `Meetings` ,`Important` ,`INBOX` , let's check it one by one 
```shell 
a SELECT Notes
* FLAGS (\Answered \Flagged \Deleted \Seen \Draft)
* OK [PERMANENTFLAGS (\Answered \Flagged \Deleted \Seen \Draft \*)] Flags permitted.
* 0 EXISTS
* 0 RECENT
* OK [UIDVALIDITY 1636509065] UIDs valid
* OK [UIDNEXT 1] Predicted next UID
a OK [READ-WRITE] Select completed (0.004 + 0.000 + 0.003 secs).
a SELECT Meetings
* OK [CLOSED] Previous mailbox closed.
* FLAGS (\Answered \Flagged \Deleted \Seen \Draft)
* OK [PERMANENTFLAGS (\Answered \Flagged \Deleted \Seen \Draft \*)] Flags permitted.
* 0 EXISTS
* 0 RECENT
* OK [UIDVALIDITY 1636509063] UIDs valid
* OK [UIDNEXT 1] Predicted next UID
a OK [READ-WRITE] Select completed (0.004 + 0.000 + 0.003 secs).
a SELECT Important
* OK [CLOSED] Previous mailbox closed.
* FLAGS (\Answered \Flagged \Deleted \Seen \Draft)
* OK [PERMANENTFLAGS (\Answered \Flagged \Deleted \Seen \Draft \*)] Flags permitted.
* 0 EXISTS
* 0 RECENT
* OK [UIDVALIDITY 1636509062] UIDs valid
* OK [UIDNEXT 1] Predicted next UID
a OK [READ-WRITE] Select completed (0.010 + 0.000 + 0.009 secs).
a SELECT Inbox
* OK [CLOSED] Previous mailbox closed.
* FLAGS (\Answered \Flagged \Deleted \Seen \Draft)
* OK [PERMANENTFLAGS (\Answered \Flagged \Deleted \Seen \Draft \*)] Flags permitted.
* 1 EXISTS
* 0 RECENT
* OK [UIDVALIDITY 1636509064] UIDs valid
* OK [UIDNEXT 2] Predicted next UID
a OK [READ-WRITE] Select completed (0.001 + 0.000 secs).
```
as we can see in here with Google help , i found that all of them `0 exists` but only INBOX have `1 Exists` , let's check it out 
```shell 
a fetch 1 (body[text])
* 1 FETCH (BODY[TEXT] {3430}
-----BEGIN OPENSSH PRIVATE KEY-----
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
-----END OPENSSH PRIVATE KEY-----
)
a OK Fetch completed (0.001 + 0.000 secs).
```
well well well we have a `OPENSSH` private key , now i can copy paste the private key to my `home` directory to activate the key with `chmod 600 tom_id_rsa`
## SSH - Get shell 
```shell
ssh -i tom_id_rsa tom@10.129.202.20
The authenticity of host '10.129.202.20 (10.129.202.20)' can't be established.
ED25519 key fingerprint is SHA256:AtNYHXCA7dVpi58LB+uuPe9xvc2lJwA6y7q82kZoBNM.
This host key is known by the following other names/addresses:
    ~/.ssh/known_hosts:17: [hashed name]
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Warning: Permanently added '10.129.202.20' (ED25519) to the list of known hosts.
Welcome to Ubuntu 20.04.3 LTS (GNU/Linux 5.4.0-90-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

  System information as of Fri 18 Sep 2026 08:49:21 AM UTC

  System load:  0.0               Processes:               184
  Usage of /:   66.4% of 5.70GB   Users logged in:         0
  Memory usage: 32%               IPv4 address for ens192: 10.129.202.20
  Swap usage:   0%

 * Super-optimized for small spaces - read how we shrank the memory
   footprint of MicroK8s to make it the smallest full K8s around.

   https://ubuntu.com/blog/microk8s-memory-optimisation

0 updates can be applied immediately.


The list of available updates is more than a week old.
To check for new updates run: sudo apt update
Ubuntu comes with ABSOLUTELY NO WARRANTY, to the extent permitted by
applicable law.


Last login: Wed Nov 10 02:51:52 2021 from 10.10.14.20
tom@NIXHARD:~$
```
since we already in SSH i try to find what can we found interesting here 
```shell 
tom@NIXHARD:~$ ls -la
total 48
drwxr-xr-x 6 tom  tom  4096 Nov 10  2021 .
drwxr-xr-x 5 root root 4096 Nov 10  2021 ..
-rw------- 1 tom  tom   532 Nov 10  2021 .bash_history
-rw-r--r-- 1 tom  tom   220 Nov 10  2021 .bash_logout
-rw-r--r-- 1 tom  tom  3771 Nov 10  2021 .bashrc
drwx------ 2 tom  tom  4096 Nov 10  2021 .cache
drwx------ 3 tom  tom  4096 Nov 10  2021 mail
drwx------ 8 tom  tom  4096 Sep 18 08:46 Maildir
-rw------- 1 tom  tom   169 Nov 10  2021 .mysql_history
-rw-r--r-- 1 tom  tom   807 Nov 10  2021 .profile
drwx------ 2 tom  tom  4096 Nov 10  2021 .ssh
-rw------- 1 tom  tom  2018 Nov 10  2021 .viminfo
```
after a long session of roaming around i decided to check one by one in tom directory , since i didn't know what to do next , but surprisingly i found something interesting inside `.bash_history`
```shell
tom@NIXHARD:~$ cat .bash_history
mysql -u tom -p
ssh-keygen -t rsa -b 4096
ls
ls -al
cd .ssh/
ls
cd mail/
ls
ls -al
cd .imap/
ls
cd Important/
ls
set term=xterm
vim key
cat ~/.ssh/id_rsa
vim key
ls
mv key ..
cd ..
ls
mv key Important/
mv Important/key ../
cd ..
ls
ls -l
id
cat /etc/passwd
ls
cd mail/
ls
ls -al
cd mail/
ls
rm Meetings
rm TESTING Important
ls -l
cd ..
ls -al
mv mail/key Maildir/.Important/new/
mv Maildir/.Important/new/key Maildir/new/
cd Maildir/new/
ls
cd ..
tree .
cat cur/key
cd cur/
ls
ls -al
cat "key:2,"
mysql -u tom -p
mysql -u tom -p
tom@NIXHARD:~$
```
that there's mysql command ? , why there i mysql command ? , okay then let's try the mysql command , hopefully bring something  
### MYSQL
```shell
tom@NIXHARD:~$ mysql -u tom -p
Enter password:
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 8
Server version: 8.0.27-0ubuntu0.20.04.1 (Ubuntu)

Copyright (c) 2000, 2021, Oracle and/or its affiliates.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

mysql>
```
well3 were in , let's check what's inside 
```shell
mysql> show databases;
+--------------------+
| Database           |
+--------------------+
| information_schema |
| mysql              |
| performance_schema |
| sys                |
| users              |
+--------------------+
5 rows in set (0.01 sec)
```
hmm users ?? , interesting let's check what's inside users database 
```shell
Database changed
mysql> show tables;
+-----------------+
| Tables_in_users |
+-----------------+
| users           |
+-----------------+
1 row in set (0.00 sec)

mysql> SELECT * from users;
+------+-------------------+------------------------------+
|  150 | HTB               | cr3n4o7rzse7rzhnckhssncif7ds |
+------+-------------------+------------------------------+
200 rows in set (0.01 sec)

mysql>
```
WELL WELL WELL , HTB username , since the practice case ask me to find the username HTB and its password , i think this is it , THX u all 


> THE TRUTH
> Of course im here not because i already understand , im here is to understand that my capabilites for now is` just like `this , i still need the google help to find out what is it , i hope i can get better in the future , cause till this day , if i already found another dead end i have an urge to open people writeup , i feel like im still need to try again without the open other people write-up , im quite jealous that the fact all of my friends can solve easy machine without open other people write-up , but i try to keep up so that i could be like them , i feel this write up will be disappointing to read , since this is my first time taking certificate .
> -- Bryant || Arkryr -- [still learning mate pls dont bully me, i try my best to keep learning ]
