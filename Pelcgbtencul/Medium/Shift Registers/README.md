# How to Solve Shift Registers
## Kategori: Cryptography

&nbsp;

| | |
| :--- | :--- |
| **Link Soal** | [Disini](https://learn.cylabacademy.org/library/716?page=1&category=2&search=shi&workspace=true) |
| **Kerentanan/Kelemahan** | Rawan terkena brute force karena hanya mengambil 8 bit paling belakang dari 1008 kemungkinan. |
| **Flag** | - |

&nbsp;

### /# Analisis Masalah dan Kelemahannya

&nbsp;

1. Kita lihat dulu apa isi file chall.py dari soal ini
   
   ```Python
   from Crypto.Util.number import bytes_to_long, long_to_bytes
   from Crypto.Random import get_random_bytes
   
   key = bytes_to_long(get_random_bytes(126))
   
   def steplfsr(lfsr):
    b7 = (lfsr >> 7) & 1
    b5 = (lfsr >> 5) & 1
    b4 = (lfsr >> 4) & 1
    b3 = (lfsr >> 3) & 1
   
    feedback = b7 ^ b5 ^ b4 ^ b3
    lfsr = (feedback << 7) | (lfsr >> 1)
    return lfsr
   
   def encrypt_lfsr(pt_bytes):
    output = bytearray()
    lfsr = key & 0xFF
    for p in pt_bytes:
        lfsr = steplfsr(lfsr)
        ks = lfsr
        output.append(p ^ ks)
    return bytes_to_long(bytes(output))
   
   pt = b"[redacted]"
   ct = encrypt_lfsr(pt)
   
   print(long_to_bytes(ct).hex())
   ```

2. Kita pahami dulu satu persatu maksud dari setiap bagian pada file chall ini.
3. 
