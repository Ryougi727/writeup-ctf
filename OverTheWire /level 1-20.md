# OVER THE WIRE

### Level 0 -> 1
```bash
bandit0@bandit:~$ ls
readme
bandit0@bandit:~$ cat readme
Congratulations on your first steps into the bandit game!!
Please make sure you have read the rules at https://overthewire.org/rules/
If you are following a course, workshop, walkthrough or other educational activity,
please inform the instructor about the rules as well and encourage them to
contribute to the OverTheWire community so we can keep these games free!

The password you are looking for is: {PASSWORD}
```

### Level 1-> 2
```bash
bandit1@bandit:~$ 
bandit1@bandit:~$ ls
-
bandit1@bandit:~$ cat ./-
{PASSWORD}
```

### Level 2-> 3
```bash
bandit2@bandit:~$ ls
--spaces in this filename--
bandit2@bandit:~$ cat "./--spaces in this filename--"
{PASSWORD}
bandit2@bandit:~$ exit
```

### Level 3-> 4
```bash
bandit3@bandit:~$ ls
inhere
bandit3@bandit:~$ cd inhere/
bandit3@bandit:~/inhere$ ls
bandit3@bandit:~/inhere$ ls -al
total 12
drwxr-xr-x 2 root    root    4096 Oct 14 09:26 .
drwxr-xr-x 3 root    root    4096 Oct 14 09:26 ..
-rw-r----- 1 bandit4 bandit3   33 Oct 14 09:26 ...Hiding-From-You
bandit3@bandit:~/inhere$ cat ...Hiding-From-You 
{PASSWORD}
```

### Level 4-> 5
```bash
bandit4@bandit:~$ ls
inhere
bandit4@bandit:~$ cd inhere/
bandit4@bandit:~/inhere$ ls
-file00  -file01  -file02  -file03  -file04  -file05  -file06  -file07  -file08  -file09
bandit4@bandit:~/inhere$ file ./*
./-file00: data
./-file01: OpenPGP Public Key
./-file02: OpenPGP Public Key
./-file03: data
./-file04: data
./-file05: data
./-file06: data
./-file07: ASCII text
./-file08: data
./-file09: data
bandit4@bandit:~/inhere$ cat ./-file07
4oQYVPkxZOOEOO5pTW81FB8j8lxXGUQw
```

### Level 5-> 6
```bash
bandit5@bandit:~$ ls
inhere
bandit5@bandit:~$ cd inhere/
bandit5@bandit:~/inhere$ ls
maybehere00  maybehere03  maybehere06  maybehere09  maybehere12  maybehere15  maybehere18
maybehere01  maybehere04  maybehere07  maybehere10  maybehere13  maybehere16  maybehere19
maybehere02  maybehere05  maybehere08  maybehere11  maybehere14  maybehere17
bandit5@bandit:~/inhere$ find . -type f -size 1033c ! -executable
./maybehere07/.file2
bandit5@bandit:~/inhere$ cat ./maybehere07/.file2
HWasnPhtq9AVKe0dmk45nxy20cvUa6EG
```

### Level 6-> 7
```bash
bandit6@bandit:~$ ls
bandit6@bandit:~$ ls -al
total 20
drwxr-xr-x   2 root root 4096 Oct 14 09:25 .
drwxr-xr-x 150 root root 4096 Oct 14 09:29 ..
-rw-r--r--   1 root root  220 Mar 31  2024 .bash_logout
-rw-r--r--   1 root root 3851 Oct 14 09:19 .bashrc
-rw-r--r--   1 root root  807 Mar 31  2024 .profile
bandit6@bandit:~$ find / -type f -user bandit7 -group bandit6 -size 33c 2>/dev/null
/var/lib/dpkg/info/bandit7.password
bandit6@bandit:~$ cat /var/lib/dpkg/info/bandit7.password
morbNTDkSW6jIlUc0ymOdMaLnOlFVAaj
```

### Level 7-> 8
```bash
bandit7@bandit:~$ ls
data.txt
bandit7@bandit:~$ file data.txt 
data.txt: Unicode text, UTF-8 text
bandit7@bandit:~$ grep millionth data.txt
millionth       dfwvzFQi4mU0wfNbFOe9RoWskMLg7eEc
bandit7@bandit:~$ exit
```

### Level 8-> 9
```bash
bandit8@bandit:~$ ls
data.txt
bandit8@bandit:~$ file data.txt 
data.txt: ASCII text
bandit8@bandit:~$ grep data.txt | wc -l
^C
bandit8@bandit:~$ sort data.txt | uniq -u
4CKMh1JI91bUIZZPXDqGanal4xvAg0JM
bandit8@bandit:~$ exit
```

### Level 9-> 10
```bash
bandit9@bandit:~$ ls
data.txt
bandit9@bandit:~$ file data.txt 
data.txt: data
bandit9@bandit:~$ strings data.txt | grep "===="
========== the
========== password
f\Z'========== is
========== FGUW5ilLVJrxX9kMYMmlN4MgbpfMiqey
bandit9@bandit:~$ exit
```

### Level 10-> 11
```bash
bandit10@bandit:~$ ls
data.txt
bandit10@bandit:~$ file data.txt 
data.txt: ASCII text
bandit10@bandit:~$ cat data.txt 
VGhlIHBhc3N3b3JkIGlzIGR0UjE3M2ZaS2IwUlJzREZTR3NnMlJXbnBOVmozcVJyCg==
bandit10@bandit:~$ echo "VGhlIHBhc3N3b3JkIGlzIGR0UjE3M2ZaS2IwUlJzREZTR3NnMlJXbnBOVmozcVJyCg==
" | base64 -d
The password is dtR173fZKb0RRsDFSGsg2RWnpNVj3qRr
bandit10@bandit:~$ exit
```

### Level 11-> 12
```bash
bandit11@bandit:~$ ls
data.txt
bandit11@bandit:~$ nano data.txt 
Unable to create directory /home/bandit11/.local/share/nano/: No such file or directory
It is required for saving/loading search history or cursor positions.

bandit11@bandit:~$ cat data.txt 
Gur cnffjbeq vf 7k16JArUVv5LxVuJfsSVdbbtaHGlw9D4
bandit11@bandit:~$ echo "Gur cnffjbeq vf 7k16JArUVv5LxVuJfsSVdbbtaHGlw9D4" | tr 'A-Za-z' 'N-ZA-Mn-za-m'
The password is 7x16WNeHIi5YkIhWsfFIqoognUTyj9Q4
bandit11@bandit:~$ exit
```

### Level 12-> 13
```bash
bandit12@bandit:~$ ls
data.txt
bandit12@bandit:~$ cat data.txt 
00000000: 1f8b 0808 2e17 ee68 0203 6461 7461 322e  .......h..data2.
00000010: 6269 6e00 0134 02cb fd42 5a68 3931 4159  bin..4...BZh91AY
00000020: 2653 59b6 7680 8b00 001a ffff fadd cfd6  &SY.v...........
00000030: f2e7 f6bb b87f 57ee fff3 b7d7 8bfd fafe  ......W.........
00000040: bffe fdfd d9ef 3dff bfff bdff b001 3aa1  ......=.......:.
00000050: a40d 007a 9901 a000 1a01 a000 1934 7a80  ...z.........4z.
00000060: 6993 469a 6800 0068 1a00 0340 680d 0d00  i.F.h..h...@h...
00000070: 01a6 8794 188d 0c27 a8d3 4608 8006 4d01  .......'..F...M.
00000080: 8800 3268 c8d0 3434 0006 9a19 0f50 3400  ..2h..44.....P4.
00000090: 1840 6403 2064 0034 1934 c468 c862 6868  .@d. d.4.4.h.bhh
000000a0: c801 a000 68f5 0e9e a346 8343 4346 8698  ....h....F.CCF..
000000b0: 40d0 0686 864c 9b48 0000 0003 40d3 4d34  @....L.H....@.M4
000000c0: 3231 3261 0003 46d4 01ea 0000 1a00 d000  212a..F.........
000000d0: 0d00 0020 c002 3067 df82 0e7a a6f5 b39a  ... ..0g...z....
000000e0: 6472 0263 7c59 8eaf c404 a738 aece fe35  dr.c|Y.....8...5
000000f0: 1921 a104 6114 268f 7f45 0411 a3de efc3  .!..a.&..E......
00000100: 7905 de6d 2229 95e1 a0e0 0d61 13bd 457e  y..m").....a..E~
00000110: 5ea0 e955 1a0c c20c dbf5 853e 0177 370e  ^..U.......>.w7.
00000120: 073a 1fb3 2b32 57b7 0c16 1ae4 c817 ac62  .:..+2W........b
00000130: 94ca ed32 1d62 6acb 0e94 e932 2b6f 9702  ...2.bj....2+o..
00000140: 4480 2c49 9192 eab8 fc13 dd5d 4ebb 4495  D.,I.......]N.D.
00000150: a8c5 81d9 e2b8 e68d 291e e9e2 11ee cc35  ........)......5
00000160: 6460 63e7 fc6c 1575 7984 da54 8626 21d6  d`c..l.uy..T.&!.
00000170: 8888 2469 cb2e 4229 6f7a 9658 174a 2edd  ..$i..B)oz.X.J..
00000180: 2381 252f 2b81 5693 5f96 432d 4f17 25e8  #.%/+.V._.C-O.%.
00000190: 9129 100e 4ef1 83ca 11de 610d 7bb0 33f0  .)..N.....a.{.3.
000001a0: a3d7 a77c dab0 cfdb 4793 5bda b7a1 2573  ...|....G.[...%s
000001b0: 0ce4 d2f2 a221 1c83 5053 dd24 bacd f161  .....!..PS.$...a
000001c0: 22d9 f42b 903d 68c4 479e c021 f658 7a32  "..+.=h.G..!.Xz2
000001d0: 67c6 975e 8b25 7c28 2ad6 119e d5e6 dbcf  g..^.%|(*.......
000001e0: 2469 7a74 fa67 3ea2 235e 1500 6deb f009  $izt.g>.#^..m...
000001f0: 3ad0 ef6e 444d 15e9 fdc2 67bc 01f3 1764  :..nDM....g....d
00000200: 980e b3c6 045f ef4b ffd1 e529 4130 2141  ....._.K...)A0!A
00000210: ca03 5c28 dce0 5f73 ecec b637 d1fe 852f  ..\(.._s...7.../
00000220: f9eb 416b b5fd df54 8aa6 0b08 022d 7160  ..Ak...T.....-q`
00000230: 215d f790 ccb0 f047 9240 083c d2a6 c098  !].....G.@.<....
00000240: 04bf f8bb 9229 c284 85b3 b404 5856 1e5b  .....)......XV.[
00000250: 9034 0200 00                             .4...
bandit12@bandit:~$ mktemp -d
/tmp/tmp.iaSBp88lGJ
bandit12@bandit:~$ cd /tmp/tmp.iaSBp88lGJ
bandit12@bandit:/tmp/tmp.iaSBp88lGJ$ cp ~/data.txt .
bandit12@bandit:/tmp/tmp.iaSBp88lGJ$ ls
data.txt
bandit12@bandit:/tmp/tmp.iaSBp88lGJ$ xxd -r data.txt > data.bin
bandit12@bandit:/tmp/tmp.iaSBp88lGJ$ ls
data.bin  data.txt
bandit12@bandit:/tmp/tmp.iaSBp88lGJ$ file data.bin
data.bin: gzip compressed data, was "data2.bin", last modified: Tue Oct 14 09:26:06 2025, max compression, from Unix, original size modulo 2^32 564
bandit12@bandit:/tmp/tmp.iaSBp88lGJ$ mv data.bin data.gz
bandit12@bandit:/tmp/tmp.iaSBp88lGJ$ gunzip data.gz
bandit12@bandit:/tmp/tmp.iaSBp88lGJ$ ls
data  data.txt
bandit12@bandit:/tmp/tmp.iaSBp88lGJ$ file data
data: bzip2 compressed data, block size = 900k
bandit12@bandit:/tmp/tmp.iaSBp88lGJ$ mv data data.bzip2
bandit12@bandit:/tmp/tmp.iaSBp88lGJ$ mv data.bzip2 data.bz2
bandit12@bandit:/tmp/tmp.iaSBp88lGJ$ bunzip2 data.bz2
bandit12@bandit:/tmp/tmp.iaSBp88lGJ$ ls
data  data.txt
bandit12@bandit:/tmp/tmp.iaSBp88lGJ$ file data
data: gzip compressed data, was "data4.bin", last modified: Tue Oct 14 09:26:06 2025, max compression, from Unix, original size modulo 2^32 20480
bandit12@bandit:/tmp/tmp.iaSBp88lGJ$ mv data data.gz
bandit12@bandit:/tmp/tmp.iaSBp88lGJ$ gunzip data.gz
bandit12@bandit:/tmp/tmp.iaSBp88lGJ$ file data
data: POSIX tar archive (GNU)
bandit12@bandit:/tmp/tmp.iaSBp88lGJ$ mv data data.tar
bandit12@bandit:/tmp/tmp.iaSBp88lGJ$ tar -xf data.tar
bandit12@bandit:/tmp/tmp.iaSBp88lGJ$ ls
data5.bin  data.tar  data.txt
bandit12@bandit:/tmp/tmp.iaSBp88lGJ$ ls
data5.bin  data.tar  data.txt
bandit12@bandit:/tmp/tmp.iaSBp88lGJ$ file data5.bin
data5.bin: POSIX tar archive (GNU)
bandit12@bandit:/tmp/tmp.iaSBp88lGJ$ mv data5.bin data2.tar
bandit12@bandit:/tmp/tmp.iaSBp88lGJ$ tar -xf data2.tar
bandit12@bandit:/tmp/tmp.iaSBp88lGJ$ ls
data2.tar  data6.bin  data.tar  data.txt
bandit12@bandit:/tmp/tmp.iaSBp88lGJ$ file data6.bin 
data6.bin: bzip2 compressed data, block size = 900k
bandit12@bandit:/tmp/tmp.iaSBp88lGJ$ mv data6.bin data.bz2
bandit12@bandit:/tmp/tmp.iaSBp88lGJ$ bunzip2 data.bz2 
bandit12@bandit:/tmp/tmp.iaSBp88lGJ$ ls
data  data2.tar  data.tar  data.txt
bandit12@bandit:/tmp/tmp.iaSBp88lGJ$ file data
data: POSIX tar archive (GNU)
bandit12@bandit:/tmp/tmp.iaSBp88lGJ$ mv data data.tar
bandit12@bandit:/tmp/tmp.iaSBp88lGJ$ tar -xf data.tar
bandit12@bandit:/tmp/tmp.iaSBp88lGJ$ ls
data2.tar  data8.bin  data.tar  data.txt
bandit12@bandit:/tmp/tmp.iaSBp88lGJ$ file data8.bin 
data8.bin: gzip compressed data, was "data9.bin", last modified: Tue Oct 14 09:26:06 2025, max compression, from Unix, original size modulo 2^32 49
bandit12@bandit:/tmp/tmp.iaSBp88lGJ$ mv data8.bin data.gz
bandit12@bandit:/tmp/tmp.iaSBp88lGJ$ gunzip data.gz
bandit12@bandit:/tmp/tmp.iaSBp88lGJ$ ls
data  data2.tar  data.tar  data.txt
bandit12@bandit:/tmp/tmp.iaSBp88lGJ$ file data
data: ASCII text
bandit12@bandit:/tmp/tmp.iaSBp88lGJ$ cat data
The password is FO5dwFsc0cbaIiH0h8J2eUks2vdTDwAn
```

### Level 13-> 14 
```bash
bandit13@bandit:~$ ls
sshkey.private
bandit13@bandit:~$ exit
logout
Connection to bandit.labs.overthewire.org closed.
                                                                                                                                            
┌──(kali㉿kali)-[~]
└─$ scp -P 2220 bandit13@bandit.labs.overthewire.org:sshkey.private .
                         _                     _ _ _   
                        | |__   __ _ _ __   __| (_) |_ 
                        | '_ \ / _` | '_ \ / _` | | __|
                        | |_) | (_| | | | | (_| | | |_ 
                        |_.__/ \__,_|_| |_|\__,_|_|\__|
                                                       

                      This is an OverTheWire game server. 
            More information on http://www.overthewire.org/wargames

backend: gibson-1
bandit13@bandit.labs.overthewire.org's password: 
sshkey.private                                                                                            100% 1679     3.0KB/s   00:00    
                                                                                                                                            
┌──(kali㉿kali)-[~]
└─$ ls -l sshkey.private      
-rw-r----- 1 kali kali 1679 Feb 19 12:21 sshkey.private
                                                                                                                                            
┌──(kali㉿kali)-[~]
└─$ chmod 700 sshkey.private 
                                                                                                                                            
┌──(kali㉿kali)-[~]
└─$ ls -l sshkey.private    
-rwx------ 1 kali kali 1679 Feb 19 12:21 sshkey.private
                                                                                                                                            
┌──(kali㉿kali)-[~]
└─$ ssh -i sshkey.private bandit14@bandit.labs.overthewire.org -p 2220

bandit14@bandit:~$ cat  /etc/bandit_pass/bandit14
MU4VWeTyJk8ROof1qqmcBPaLh7lDCPvS
```

### Level 14-> 15
```bash
bandit14@bandit:~$ nc localhost 30000
MU4VWeTyJk8ROof1qqmcBPaLh7lDCPvS 
Correct!
8xCjnmgoKbGLhHFAZlGE5Tmu4M2tKJQo
```

### Level 15-> 16
```bash
bandit15@bandit:~$ ls
bandit15@bandit:~$ openssl s_client -connect localhost:30001
CONNECTED(00000003)
Can't use SSL_get_servername
depth=0 CN = SnakeOil
verify error:num=18:self-signed certificate
verify return:1
depth=0 CN = SnakeOil
verify return:1
---
Certificate chain
 0 s:CN = SnakeOil
   i:CN = SnakeOil
   a:PKEY: rsaEncryption, 4096 (bit); sigalg: RSA-SHA256
   v:NotBefore: Jun 10 03:59:50 2024 GMT; NotAfter: Jun  8 03:59:50 2034 GMT
---
Server certificate
-----BEGIN CERTIFICATE-----
MIIFBzCCAu+gAwIBAgIUBLz7DBxA0IfojaL/WaJzE6Sbz7cwDQYJKoZIhvcNAQEL
BQAwEzERMA8GA1UEAwwIU25ha2VPaWwwHhcNMjQwNjEwMDM1OTUwWhcNMzQwNjA4
MDM1OTUwWjATMREwDwYDVQQDDAhTbmFrZU9pbDCCAiIwDQYJKoZIhvcNAQEBBQAD
ggIPADCCAgoCggIBANI+P5QXm9Bj21FIPsQqbqZRb5XmSZZJYaam7EIJ16Fxedf+
jXAv4d/FVqiEM4BuSNsNMeBMx2Gq0lAfN33h+RMTjRoMb8yBsZsC063MLfXCk4p+
09gtGP7BS6Iy5XdmfY/fPHvA3JDEScdlDDmd6Lsbdwhv93Q8M6POVO9sv4HuS4t/
jEjr+NhE+Bjr/wDbyg7GL71BP1WPZpQnRE4OzoSrt5+bZVLvODWUFwinB0fLaGRk
GmI0r5EUOUd7HpYyoIQbiNlePGfPpHRKnmdXTTEZEoxeWWAaM1VhPGqfrB/Pnca+
vAJX7iBOb3kHinmfVOScsG/YAUR94wSELeY+UlEWJaELVUntrJ5HeRDiTChiVQ++
wnnjNbepaW6shopybUF3XXfhIb4NvwLWpvoKFXVtcVjlOujF0snVvpE+MRT0wacy
tHtjZs7Ao7GYxDz6H8AdBLKJW67uQon37a4MI260ADFMS+2vEAbNSFP+f6ii5mrB
18cY64ZaF6oU8bjGK7BArDx56bRc3WFyuBIGWAFHEuB948BcshXY7baf5jjzPmgz
mq1zdRthQB31MOM2ii6vuTkheAvKfFf+llH4M9SnES4NSF2hj9NnHga9V08wfhYc
x0W6qu+S8HUdVF+V23yTvUNgz4Q+UoGs4sHSDEsIBFqNvInnpUmtNgcR2L5PAgMB
AAGjUzBRMB0GA1UdDgQWBBTPo8kfze4P9EgxNuyk7+xDGFtAYzAfBgNVHSMEGDAW
gBTPo8kfze4P9EgxNuyk7+xDGFtAYzAPBgNVHRMBAf8EBTADAQH/MA0GCSqGSIb3
DQEBCwUAA4ICAQAKHomtmcGqyiLnhziLe97Mq2+Sul5QgYVwfx/KYOXxv2T8ZmcR
Ae9XFhZT4jsAOUDK1OXx9aZgDGJHJLNEVTe9zWv1ONFfNxEBxQgP7hhmDBWdtj6d
taqEW/Jp06X+08BtnYK9NZsvDg2YRcvOHConeMjwvEL7tQK0m+GVyQfLYg6jnrhx
egH+abucTKxabFcWSE+Vk0uJYMqcbXvB4WNKz9vj4V5Hn7/DN4xIjFko+nREw6Oa
/AUFjNnO/FPjap+d68H1LdzMH3PSs+yjGid+6Zx9FCnt9qZydW13Miqg3nDnODXw
+Z682mQFjVlGPCA5ZOQbyMKY4tNazG2n8qy2famQT3+jF8Lb6a4NGbnpeWnLMkIu
jWLWIkA9MlbdNXuajiPNVyYIK9gdoBzbfaKwoOfSsLxEqlf8rio1GGcEV5Hlz5S2
txwI0xdW9MWeGWoiLbZSbRJH4TIBFFtoBG0LoEJi0C+UPwS8CDngJB4TyrZqEld3
rH87W+Et1t/Nepoc/Eoaux9PFp5VPXP+qwQGmhir/hv7OsgBhrkYuhkjxZ8+1uk7
tUWC/XM0mpLoxsq6vVl3AJaJe1ivdA9xLytsuG4iv02Juc593HXYR8yOpow0Eq2T
U5EyeuFg5RXYwAPi7ykw1PW7zAPL4MlonEVz+QXOSx6eyhimp1VZC11SCg==
-----END CERTIFICATE-----
subject=CN = SnakeOil
issuer=CN = SnakeOil
---
No client certificate CA names sent
Peer signing digest: SHA256
Peer signature type: RSA-PSS
Server Temp Key: X25519, 253 bits
---
SSL handshake has read 2103 bytes and written 373 bytes
Verification error: self-signed certificate
---
New, TLSv1.3, Cipher is TLS_AES_256_GCM_SHA384
Server public key is 4096 bit
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
    Session-ID: 0897F83586C4DF21ACB1818DA103657CFD38993E0F7606E2A3E24F50C51A8573
    Session-ID-ctx: 
    Resumption PSK: A279E0112D047742C8FCE5B89ADFA339A07B91A6BD961C0005620F4702647787EB928BB0ACC5CB5E34F2B88829191DA3
    PSK identity: None
    PSK identity hint: None
    SRP username: None
    TLS session ticket lifetime hint: 300 (seconds)
    TLS session ticket:
    0000 - ca 05 30 7c 7c 2e 15 ba-cf 68 d6 86 43 76 ac 94   ..0||....h..Cv..
    0010 - 21 95 37 35 b8 cd 8c 12-89 f0 12 11 e3 54 1c 70   !.75.........T.p
    0020 - 00 4f 44 ac d4 4d 05 57-07 67 65 66 87 9b c6 22   .OD..M.W.gef..."
    0030 - 9e 11 02 50 74 51 b1 9c-30 bd bb 73 02 6b 24 65   ...PtQ..0..s.k$e
    0040 - 88 1a d5 74 92 fd ad e0-08 cc 22 0d c4 b2 13 63   ...t......"....c
    0050 - 77 e1 9a 9a 6c c1 43 ee-2a 12 3f 5d f7 fa b1 c6   w...l.C.*.?]....
    0060 - d9 9e 87 b2 4d f3 b8 2f-68 b9 80 0d b5 c3 98 98   ....M../h.......
    0070 - dd 93 e6 de 58 23 43 e3-3b 41 7d f6 b5 34 7b f0   ....X#C.;A}..4{.
    0080 - 52 3a 6e 5d b1 32 2d bf-d2 64 b4 14 42 de 03 e6   R:n].2-..d..B...
    0090 - 38 ce c6 72 5a c8 26 c5-dd 9d 39 4d 7d 13 fe 8a   8..rZ.&...9M}...
    00a0 - cf 88 f8 10 80 73 19 7e-eb 9f 65 58 82 40 26 81   .....s.~..eX.@&.
    00b0 - 13 12 7e 37 a4 e9 7d ce-56 82 cb 44 0b 63 41 45   ..~7..}.V..D.cAE
    00c0 - df 08 01 cb 51 0d c2 6f-29 9d ba 66 c1 37 6d 39   ....Q..o)..f.7m9
    00d0 - 75 f0 ee d9 09 b7 e9 11-ce a5 10 e3 2e 33 97 eb   u............3..

    Start Time: 1771522202
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
    Session-ID: BEFED5D221AD603C1B32377E840E43364009EFAD79439615B7D07E9078E130D7
    Session-ID-ctx: 
    Resumption PSK: EDA35619963A107A45E37111F69D345E20864F5526D6CCBD5F4A6DB9E06F228A112E30261987B37EC7ABC23A6BD5453A
    PSK identity: None
    PSK identity hint: None
    SRP username: None
    TLS session ticket lifetime hint: 300 (seconds)
    TLS session ticket:
    0000 - ca 05 30 7c 7c 2e 15 ba-cf 68 d6 86 43 76 ac 94   ..0||....h..Cv..
    0010 - 96 dd b3 24 f4 9f d5 30-8e 11 38 52 ee 2a 21 cd   ...$...0..8R.*!.
    0020 - c5 ee 33 42 e8 a3 4b a1-b8 e3 4f 2c b9 66 97 ac   ..3B..K...O,.f..
    0030 - e6 7a a3 26 75 52 c8 4d-9c 67 72 73 1a 4c ce 1f   .z.&uR.M.grs.L..
    0040 - 52 8b ff 18 df 56 e4 4e-92 db d9 c0 b5 a1 b9 bc   R....V.N........
    0050 - 2a 31 8a 7e 89 b9 50 63-9c 33 ec 0b da 26 b1 ec   *1.~..Pc.3...&..
    0060 - 91 4a 0b a0 a2 81 61 fc-28 74 ee 54 da ee 41 78   .J....a.(t.T..Ax
    0070 - a7 b5 d0 92 11 f4 55 f3-7c 87 c6 7e e5 90 e0 31   ......U.|..~...1
    0080 - a6 a7 33 a5 c8 67 13 31-d1 d0 21 74 04 36 8c 6a   ..3..g.1..!t.6.j
    0090 - f1 be 61 6d a8 1c 25 c2-b2 6c 33 4f 9f 58 ec 8c   ..am..%..l3O.X..
    00a0 - 8c 0f 24 6d f4 bd 31 0a-41 a0 ba f9 f0 7a d7 4f   ..$m..1.A....z.O
    00b0 - 81 04 01 df 01 05 5d ad-fa 65 65 76 85 6c 98 58   ......]..eev.l.X
    00c0 - 1b d1 47 a8 c2 ce dc e1-25 ef c8 31 3a 76 9f ad   ..G.....%..1:v..
    00d0 - 20 08 bb c7 4b c2 e2 4f-b3 b5 a7 09 8a 70 c7 d0    ...K..O.....p..

    Start Time: 1771522202
    Timeout   : 7200 (sec)
    Verify return code: 18 (self-signed certificate)
    Extended master secret: no
    Max Early Data: 0
---
read R BLOCK
8xCjnmgoKbGLhHFAZlGE5Tmu4M2tKJQo
Correct!
kSkvUpMQ7lBYyCM4GBPvCvT1BfWRy0Dx

closed
```

### Level 16-> 17
```bash
bandit16@bandit:~$ nmap -sV 10.0.1.164 -p31000-32000
Starting Nmap 7.94SVN ( https://nmap.org ) at 2026-02-19 17:39 UTC
Nmap scan report for 10.0.1.164
Host is up (0.00062s latency).
Not shown: 996 closed tcp ports (conn-refused)
PORT      STATE SERVICE     VERSION
31046/tcp open  echo
31518/tcp open  ssl/echo
31691/tcp open  echo
31790/tcp open  ssl/unknown
31960/tcp open  echo
1 service unrecognized despite returning data. If you know the service/version, please submit the following fingerprint at https://nmap.org/cgi-bin/submit.cgi?new-service :
---

bandit16@bandit:~$ openssl s_client -connect localhost:31790 -quiet
Can't use SSL_get_servername
depth=0 CN = SnakeOil
verify error:num=18:self-signed certificate
verify return:1
depth=0 CN = SnakeOil
verify return:1
kSkvUpMQ7lBYyCM4GBPvCvT1BfWRy0Dx
Correct!
-----BEGIN RSA PRIVATE KEY-----
MIIEogIBAAKCAQEAvmOkuifmMg6HL2YPIOjon6iWfbp7c3jx34YkYWqUH57SUdyJ
imZzeyGC0gtZPGujUSxiJSWI/oTqexh+cAMTSMlOJf7+BrJObArnxd9Y7YT2bRPQ
Ja6Lzb558YW3FZl87ORiO+rW4LCDCNd2lUvLE/GL2GWyuKN0K5iCd5TbtJzEkQTu
DSt2mcNn4rhAL+JFr56o4T6z8WWAW18BR6yGrMq7Q/kALHYW3OekePQAzL0VUYbW
JGTi65CxbCnzc/w4+mqQyvmzpWtMAzJTzAzQxNbkR2MBGySxDLrjg0LWN6sK7wNX
x0YVztz/zbIkPjfkU1jHS+9EbVNj+D1XFOJuaQIDAQABAoIBABagpxpM1aoLWfvD
KHcj10nqcoBc4oE11aFYQwik7xfW+24pRNuDE6SFthOar69jp5RlLwD1NhPx3iBl
J9nOM8OJ0VToum43UOS8YxF8WwhXriYGnc1sskbwpXOUDc9uX4+UESzH22P29ovd
d8WErY0gPxun8pbJLmxkAtWNhpMvfe0050vk9TL5wqbu9AlbssgTcCXkMQnPw9nC
YNN6DDP2lbcBrvgT9YCNL6C+ZKufD52yOQ9qOkwFTEQpjtF4uNtJom+asvlpmS8A
vLY9r60wYSvmZhNqBUrj7lyCtXMIu1kkd4w7F77k+DjHoAXyxcUp1DGL51sOmama
+TOWWgECgYEA8JtPxP0GRJ+IQkX262jM3dEIkza8ky5moIwUqYdsx0NxHgRRhORT
8c8hAuRBb2G82so8vUHk/fur85OEfc9TncnCY2crpoqsghifKLxrLgtT+qDpfZnx
SatLdt8GfQ85yA7hnWWJ2MxF3NaeSDm75Lsm+tBbAiyc9P2jGRNtMSkCgYEAypHd
HCctNi/FwjulhttFx/rHYKhLidZDFYeiE/v45bN4yFm8x7R/b0iE7KaszX+Exdvt
SghaTdcG0Knyw1bpJVyusavPzpaJMjdJ6tcFhVAbAjm7enCIvGCSx+X3l5SiWg0A
R57hJglezIiVjv3aGwHwvlZvtszK6zV6oXFAu0ECgYAbjo46T4hyP5tJi93V5HDi
Ttiek7xRVxUl+iU7rWkGAXFpMLFteQEsRr7PJ/lemmEY5eTDAFMLy9FL2m9oQWCg
R8VdwSk8r9FGLS+9aKcV5PI/WEKlwgXinB3OhYimtiG2Cg5JCqIZFHxD6MjEGOiu
L8ktHMPvodBwNsSBULpG0QKBgBAplTfC1HOnWiMGOU3KPwYWt0O6CdTkmJOmL8Ni
blh9elyZ9FsGxsgtRBXRsqXuz7wtsQAgLHxbdLq/ZJQ7YfzOKU4ZxEnabvXnvWkU
YOdjHdSOoKvDQNWu6ucyLRAWFuISeXw9a/9p7ftpxm0TSgyvmfLF2MIAEwyzRqaM
77pBAoGAMmjmIJdjp+Ez8duyn3ieo36yrttF5NSsJLAbxFpdlc1gvtGCWW+9Cq0b
dxviW8+TFVEBl1O4f7HVm6EpTscdDxU+bCXWkfjuRb7Dy9GOtt9JPsX8MBTakzh3
vBgsyi/sN3RqRBcGU40fOoZyfAMT8s1m/uYv52O6IgeuZ/ujbjY=
-----END RSA PRIVATE KEY-----
┌──(kali㉿kali)-[~]
└─$ nano bandit17.private --> buat file baru dan paste key nya
                                                                                                                                            
┌──(kali㉿kali)-[~]
└─$ chmod 700 bandit17.private                                         
                                                                                                                                            
┌──(kali㉿kali)-[~]
└─$ ls -l bandit17.private 
-rwx------ 1 kali kali 1675 Feb 19 12:52 bandit17.private
                                                                                                                                            
┌──(kali㉿kali)-[~]
└─$ ssh -i bandit17.private bandit17@bandit.labs.overthewire.org -p 2220 
```

### Level 17-> 18
```bash
  bandit17@bandit:~$ ls
passwords.new  passwords.old
bandit17@bandit:~$ diff passwords.old passwords.new
42c42
< pGozC8kOHLkBMOaL0ICPvLV1IjQ5F1VA
---
> x2gLTTjFwMOhQ8oWNbMN362QKxfRqGlO    (ini yang baru)
bandit17@bandit:~$ exit
logout
```

### Level 18-> 19
```bash
┌──(kali㉿kali)-[~]
└─$ ssh bandit18@bandit.labs.overthewire.org -p 2220 -t /bin/sh
                         _                     _ _ _   
                        | |__   __ _ _ __   __| (_) |_ 
                        | '_ \ / _` | '_ \ / _` | | __|
                        | |_) | (_| | | | | (_| | | |_ 
                        |_.__/ \__,_|_| |_|\__,_|_|\__|
                                                       

                      This is an OverTheWire game server. 
            More information on http://www.overthewire.org/wargames

backend: gibson-1
bandit18@bandit.labs.overthewire.org's password: 
$ ls
readme
$ cat read
cat: read: No such file or directory
$ cat readme
cGWpMaKXVwDUNgPAVJbWYuGHVn9zl3j8
$ ^C
$ exit
```
Alternatifnya, Anda dapat menggunakan metode yang sama untuk menjalankan perintah dengan SSH tetapi menggunakan /bin/bash sebagai perintah untuk menjalankan shell bash atau menggunakan flag t, yang memungkinkan 'pseudo-terminal' berjalan di mesin target, dengan cara ini kita dapat menjalankan \bin\sh  

### Level 19-> 20
```bash
bandit19@bandit:~$ ls
bandit20-do
bandit19@bandit:~$ ls -l
total 16
-rwsr-x--- 1 bandit20 bandit19 14884 Oct 14 09:26 bandit20-do
bandit19@bandit:~$ id
uid=11019(bandit19) gid=11019(bandit19) groups=11019(bandit19)
bandit19@bandit:~$ ./bandit20-do 
Run a command as another user.
  Example: ./bandit20-do whoami
bandit19@bandit:~$ ./bandit20-do id
uid=11019(bandit19) gid=11019(bandit19) euid=11020(bandit20) groups=11019(bandit19)
bandit19@bandit:~$ ./bandit20-do cat /etc/bandit_pass/bandit20
0qXahG8ZjOVMN9Ghs7iOWsCfZyXOUbYO
```

### level 20 -> 21
```bash
bandit20@bandit:~$ ls
suconnect
bandit20@bandit:~$ ls -l
total 16
-rwsr-x--- 1 bandit21 bandit20 15608 Oct 14 09:26 suconnect
bandit20@bandit:~$ echo -n '0qXahG8ZjOVMN9Ghs7iOWsCfZyXOUbYO'| nc -l -p 1234 &
[1] 20
bandit20@bandit:~$ ./suconnect 1234
Read: 0qXahG8ZjOVMN9Ghs7iOWsCfZyXOUbYO
Password matches, sending next password
EeoULMCra2q0dSkYj561DX7s1CpBuOBt
```



















