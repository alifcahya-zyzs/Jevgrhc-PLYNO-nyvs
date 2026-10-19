# How to Solve Shift Registers
## Kategori: Cryptography

&nbsp;

| | |
| :--- | :--- |
| **Link Soal** | [Disini](https://learn.cylabacademy.org/library/716?page=1&category=2&search=shi&workspace=true) |
| **Kerentanan/Kelemahan** | Rawan terkena brute force karena hanya mengambil 8 bit paling belakang dari 1008 kemungkinan. |
| **Flag** | - |

&nbsp;

### # Analisis Masalah, Kode Python dan Kelemahannya


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
   
   
   `from Crypto.Random import get_random_bytes` Kode ini mengambil 1 fungsi dari `Crypto.Random` yaitu fungsi `get_random_bytes` yang fungsinya menghasilkan byte kriptografi acak.
   
   &nbsp;

4. Di baris ke 4 `key = bytes_to_long(get_random_bytes(126))` adalah fungsi untuk mengambil 126 byte acak sebagai key. Fungsi `(get_random_bytes(126))` ini adalah yang berfungsi mengambil 126 byte acak itu. Sedangkan kode `bytes_to_long` adalah fungsi yang merubah byte acak itu menjadi angka ASCII. 126 byte acak itu berarti ada 1008 bit yang berarti juga ada 2<sup>1008</sup> kemungkinan.
   
   &nbsp;

5. Di baris 6-10 adalah blok kode yang yang berfungsi mengambil bit dari urutan yang dipilih yang disini adalah bit ke 7,5,4,3 dari setiap byte.
   
   
   `def steplfsr(lfsr):` berfungsi membuat blok fungsi steplfsr dengan parameter (lfsr).
   
   
   ```Python
   b7 = (lfsr >> 7) & 1
   b5 = (lfsr >> 5) & 1
   b4 = (lfsr >> 4) & 1
   b3 = (lfsr >> 3) & 1
   ```
   
   Blok fungsi ini berfungsi untuk mengambil bit dari urutan bit ke 7,5,4,9 lalu di operasi bitwise &(AND) dengan angka 1(dalam byte), meskipun dalam bit biner angka 1 tetaplah hanya 1))

   &nbsp;

6. Pada baris 12-14 ini masih sambungan dari blok fungsi steplfsr diatas, namun di bagian kode ini adalah yang berfungsi melakukan operasi bitwise XOR dalam lfsr dan mengirim hasilnya keluar dari blok fungsi steplfsr.


   ```Python
    feedback = b7 ^ b5 ^ b4 ^ b3
   ```

   Yang di atas ini adalah fungsi yang melakukan bitwise XOR nya menggunakan urutan bit yang sudah dipilih dan di operasi AND dengan 1 tadi.
   
   ```Python
    lfsr = (feedback << 7) | (lfsr >> 1)
   ```
   
   `(feedback << 7)` Yang ini berfungsi meletakkan bit hasil operasi XOR tadi ke urutan ke 7(ke bagian paling kiri barisan bit) lalu di operasikan OR oleh karakter `|`(pipe) ini dengan fungsi `(lfsr >> 1)`, nah fungsi ini mengambil parameter lfsr tadi lalu digeser ke kenan 1 langkah.

   ```Python
    return lfsr
   ```

   Fungsi ini berguna mengirimkan hasil lfsr ke luar blok fungsi ini agar bisa diolah lagi oleh fungsi lain.

   &nbsp;

7. Sekarang kita bahas blok fungsi baris ke 16-23 ini:
   
   ```Python
   def encrypt_lfsr(pt_bytes):
    output = bytearray()
    lfsr = key & 0xFF
    for p in pt_bytes:
        lfsr = steplfsr(lfsr)
        ks = lfsr
        output.append(p ^ ks)
    return bytes_to_long(bytes(output))
   ```
   
   
   ```Python
   def encrypt_lfsr(pt_bytes):
   ```
   Baris ini mendefinisikan encrypt_lfsr sebagai blok fungsi baru dengan parameter kosong pt_bytes.
   
   
   ```Python
    output = bytearray()
   ```
   Baris ini membuat variabel output untuk menyimpan hasil lfsr secara urut  agar tidak hilang saat lfsr sedang bekerja.
   
   
   ```Python
    lfsr = key & 0xFF
   ```
   `**Nah di bagian ini adalah petunjuk yang sangat penting untuk menemukan key dari lfsr ini**`
   Petunjuknya adalah `& 0xFF` ini yang maksudnya adalah 0xFF ini hanya mengambil 8 bit paling belakang dari key karena 0xFF dalam biner hanya bernilai 8 bit angka 1. 0xFF ini juga dapat berfungsi karena adanya operasi bitwise AND dari karakter ini `&` . Jika tidak ada 0xFF maka pencarian key lfsr ini akan memerlukan banyak waktu karena harus mencoba 2<sup>1008</sup> kemungkinan sedangkan dengan adanya `& 0xFF` ini sangat mempermudah karena hanya mencoba 2<sup>8</sup> kemungkinan.
   
   
   ```Python
    for p in pt_bytes:
   ```
   Fungsi ini mendefinisikan variabel p dalam pt_bytes.
   
   
   ```Python
    lfsr = steplfsr(lfsr)
   ```
   Fungi ini mengambil output dari `steplfsr(lfsr)` tadi kemudian menyimpannya dalam variabel `lfsr` yang baru.
   
   
   ```Python
    ks = lfsr
   ```
   Yang ini tidak ada fungsinya sih, cuma merubah nama variabel lfsr menjadi ks(keystream)
   
   
   ```Python
    output.append(p ^ ks)
   ```
   Nah fungsi ini lah yang bertugas meng enkripsi plaintext menggunakan key yang sudah dibuat tadi dengan cara byte dari plaintext di XOR dengan byte dari keystream. lalu hasil XOR tadi dimasukkan kedalam variabel output tadi.
   
   
   
   
   
# I'm Confused :{
