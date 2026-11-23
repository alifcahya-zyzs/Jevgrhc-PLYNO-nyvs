# Shift Registers

&nbsp;


1. Buka soal lalu baca deskripsi dan petunjuk, disini cuma ada deskripsi kalo pembuat soal baru saja belajar tentang LFSR jadi dia menerapkannya pada program ini.
   
   <img width="1401" height="262" alt="Screenshot_2026-11-23_08_39_49" src="https://github.com/user-attachments/assets/2140451a-b0ea-47b5-85aa-ca9303bec7b7" />
   
   
   &nbsp;
   
2. Karena sudah ada petunjuk yaitu lfsr, maka langsung saja unduh kedua file yang dilampirkan yaitu kode program dalam bahasa python dan ciphertext dalam file .txt.
   
   
   &nbsp;
   
3. Karena saya belum paham dengan bahasa python, maka saya menggunakan `AI` untuk membuatkan saya kode program bruteforce lfsr berdasarkan file python yang terlampir. Kalo ada beberapa program yang eror atau kesulitan saat mengedit programnya, tanyakan saja pada AI.
   
   <img width="799" height="863" alt="Screenshot_2026-11-23_08_40_00" src="https://github.com/user-attachments/assets/e37a65c9-9bc0-4971-9c04-15b58c8874a0" />
   
   <img width="810" height="901" alt="Screenshot_2026-11-23_08_40_36" src="https://github.com/user-attachments/assets/75552400-de27-4c39-9a73-13a0310bc4af" />
   
   
   &nbsp;
   
4. Setelah mendapatkan kode brute force nya, buka terminal dan cari direktori dimana file ciphertext/output.txt tadi disimpan. Jalankan command ini untuk mendapat isi/ciphertext nya.
   
   ```bash
   cat output.txt
   ```
   
   &nbsp;
   
5. Buka terminal lain lalu buat file python dengan command:
   
   ```bash
   nano namafile.py
   ```
   
   Karena input ciphertext pada kode ini berada di luar kode(pada kolom input tersendiri saat kode dijalankan), paste semua isi kode yang dibuat AI tadi kesini dan simpan.
   ***Kecuali untuk kode yang input ciphertext nya berada di dalam kode bruteforce ini, maka tempel ciphertext di variabel ciphertext yang disediakan***
   
   <img width="797" height="1080" alt="Screenshot_2026-11-23_08_41_43" src="https://github.com/user-attachments/assets/27af8894-d759-4609-9e13-e29b0fc1f7f8" />
   
   
   &nbsp;
   
6. ***Jika memakai linux, wajib menggunakan `virtual environment(VENV)` untuk menjalankan kode python, selain itu kita juga harus sudah menginstal python cryptodome agar kode tadi dapat berjalan.***
   
   &nbsp;
   
7. Jika semua hal itu sudah terpenuhi, lanjutkan dengan menjalankan kode python yang sudah dibuat tadi dengan:
   
   ```bash
   python3 namafile.py
   ```
   
   &nbsp;
   
   Jika kode bruteforce berhasil berjalan maka akan menampilkan flag seperti ini
   
   
   <img width="1171" height="605" alt="Screenshot_2026-11-23_08_42_49" src="https://github.com/user-attachments/assets/d730e601-86a3-44a2-928b-1f3509a9dc3b" />
   
   
