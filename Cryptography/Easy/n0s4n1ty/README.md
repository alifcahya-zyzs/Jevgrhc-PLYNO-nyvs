# ﻿How to solve n0s4n1ty
1. Pertama, luncurkan instans dan buka web soal.
<img width="1920" height="1080" alt="Screenshot (377)" src="https://github.com/user-attachments/assets/f3309ae4-5055-4d67-95b4-c8e6aed720a6" />

2. Coba upload file gambar random.
<img width="1920" height="1080" alt="Screenshot (286)" src="https://github.com/user-attachments/assets/93afc3d5-00db-429c-98e0-b87de70b937b" />
<img width="1920" height="1080" alt="Screenshot (287)" src="https://github.com/user-attachments/assets/8ee29dd1-513c-4a49-9af3-420e651d4d7e" />
3. Semua bentuk file dapat di upload disini karena tidak di sanitasi. Disini file gambar tetap bisa ter-upload tapi yang dibutuhkan oleh web nya adalah file php karena di URL nya tertulis gitu.
4. Karena file php bisa di upload, coba buat file php di notepad atau menggunakan nano dengan isi:

```
php <php? echo exec("sudo -l")?>
```

  untuk melihat apakah kita diizinkan untuk menkalankan perintah root dan apakah memerlukan password saat ingin melakukannya. 
5. Lalu ubah bagian akhir URL menjadi ```/uploads/"nama-file".php``` untuk melihat hasil eksekusi dari file php tadi.

<img width="1920" height="1080" alt="Screenshot (292)" src="https://github.com/user-attachments/assets/3cca2e13-4981-4952-9986-ac43346034d3" />
<img width="1920" height="1080" alt="Screenshot (297)" src="https://github.com/user-attachments/assets/e0f212ee-196a-4922-a94e-4f080410b68b" />

6. Maka akan terlihat disini apakah kita diizinkan untuk melakukan perintah apa saja dan apakah ada password nya, disini terlihat bahwa ALL menunjukkan kita bisa melakukan perintah apa saja dan NO PASSWD menunjukkan kalo saat menjalankan perintah itu kita tidak memerlukan password.
7. Sekarang kita coba ganti isi file php tadi dengan ```bash sudo ls /root``` untuk melihat isi direktori root. Lalu upload ulang file .php nya lalu ubah URL nya seperti di cara tadi. Disini terlihat isinya ada flag.txt
<img width="1920" height="1080" alt="Screenshot (293)" src="https://github.com/user-attachments/assets/13cff263-9191-467c-b407-31ea8d7d90b7" />

<img width="1920" height="1080" alt="Screenshot (296)" src="https://github.com/user-attachments/assets/90dd0d89-0f4a-4e8a-b47d-bb58c3728647" />

8. Nah flag soal ctf itu ada di dalam file flag.txt ini. Gunakan file .php tadi lalu ubah lagi command nya dengan ```bash sudo cat /root/flag.txt``` dan upload ulang file nya. Ini gunanya untuk memanggil isi dari flag.txt ini.
<img width="1920" height="1080" alt="Screenshot (298)" src="https://github.com/user-attachments/assets/31564286-333c-497f-8e0e-328a14639eb9" />

<img width="1920" height="1080" alt="Screenshot (299)" src="https://github.com/user-attachments/assets/f337db34-db2d-442f-89d4-d22cc016269d" />

9. Nah flag nya sudah ketemu, tinggal salin dan di paste saja di kolom jawaban soal ctf.
