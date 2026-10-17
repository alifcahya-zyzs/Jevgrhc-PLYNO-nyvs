# How to Solve Shift Registers
## Kategori: Cryptography

&nbsp;

| | |
| :--- | :--- |
| **Link Soal** | [Disini](https://learn.cylabacademy.org/library/716?page=1&category=2&search=shi&workspace=true) |
| **Kerentanan/Kelemahan** | Rawan terkena brute force karena hanya mengambil 8 bit paling belakang dari 1008 kemungkinan. |
| **Flag** | - |

&nbsp;

### # Analisis Masalah dan Kelemahannya


1. Kita lihat dulu apa isi file chall.py dari soal ini
   
   ```Python
   from Crypto.Util.number import bytes_to_long, long_to_bytes   #1
   from Crypto.Random import get_random_bytes                    #2
                                                                 #3
   key = bytes_to_long(get_random_bytes(126))                    #4
                                                                 #5
   def steplfsr(lfsr):                                           #6
    b7 = (lfsr >> 7) & 1                                         #7
    b5 = (lfsr >> 5) & 1                                         #8
    b4 = (lfsr >> 4) & 1                                         #9
    b3 = (lfsr >> 3) & 1                                         #10
                                                                 #11
    feedback = b7 ^ b5 ^ b4 ^ b3                                 #12
    lfsr = (feedback << 7) | (lfsr >> 1)                         #13  
    return lfsr                                                  #14
                                                                 #15
   def encrypt_lfsr(pt_bytes):                                   #16
    output = bytearray()                                         #17
    lfsr = key & 0xFF                                            #18
    for p in pt_bytes:                                           #19
        lfsr = steplfsr(lfsr)                                    #20
        ks = lfsr                                                #21
        output.append(p ^ ks)                                    #22
    return bytes_to_long(bytes(output))                          #23
                                                                 #24
   pt = b"[redacted]"                                            #25
   ct = encrypt_lfsr(pt)                                         #26
                                                                 #27
   print(long_to_bytes(ct).hex())                                #28
   ```

2. Kita pahami dulu satu persatu maksud dari setiap bagian pada file chall ini.
3. Di baris 1 dan 2, ada kode untuk mengambil tools yang ada di python.
   `from Crypto.Util.number import bytes_to_long, long_to_bytes` Kode ini mengambil 2 fungsi dari `Crypto.Util.number` yaitu fungsi `bytes_to_long` yang fungsinya merubah byte huruf atau angka menjadi angka kode ASCII. Dan satunya lagi yaitu fungsi `long_to_bytes` yang fungsinya kebalikan dari `bytes_to_long` yaitu merubah angka kode ASCII menjadi byte huruf atau angka biasa.
   `from Crypto.Random import get_random_bytes` Kode ini mengambil 1 fungsi dari `Crypto.Random` yaitu fungsi `get_random_bytes` yang fungsinya
