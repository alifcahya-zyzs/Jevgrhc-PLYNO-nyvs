# ﻿How to solve n0s4n1ty

&nbsp;
1. Pertama, luncurkan instans dan buka web soal.
  <img width="1673" height="947" alt="Screenshot (377)" src="https://github.com/user-attachments/assets/b70742c8-1934-4d9f-82c4-292e3421ec4c" />
  &nbsp;
  
  &nbsp;
2. Coba upload file gambar random.
  &nbsp;
  <img width="1666" height="945" alt="Screenshot (286)" src="https://github.com/user-attachments/assets/f29b7ea7-d7e2-4f7d-8d07-e0cabe8d5500" />
  &nbsp;
  <img width="1670" height="949" alt="Screenshot (287)" src="https://github.com/user-attachments/assets/6e8643ec-a1f6-467a-b10f-e640ab4a7a1c" />
  &nbsp;
  
3. Semua bentuk file dapat di upload disini karena tidak di sanitasi. Disini file gambar tetap bisa ter-upload tapi yang dibutuhkan oleh web nya adalah file php karena di URL nya tertulis gitu.
4. Karena file php bisa di upload, coba buat file php di notepad atau menggunakan nano dengan isi:

  ```
  <?php echo exec("sudo -l");?>
  ```
   untuk melihat apakah kita diizinkan untuk menkalankan perintah root dan apakah memerlukan password saat ingin melakukannya.
   &nbsp;
5. Lalu ubah bagian akhir URL menjadi ```/uploads/"nama-file".php``` untuk melihat hasil eksekusi dari file php tadi.
  &nbsp;
  <img width="1679" height="944" alt="Screenshot (292)" src="https://github.com/user-attachments/assets/82028caa-f12a-48fa-bbc8-546c1887f9c2" />
  &nbsp;
  <img width="1667" height="934" alt="Screenshot (297)" src="https://github.com/user-attachments/assets/f3c72548-bff3-4101-9a91-baa47c05b98b" />
  &nbsp;
6. Maka akan terlihat disini apakah kita diizinkan untuk melakukan perintah apa saja dan apakah ada password nya, disini terlihat bahwa ALL menunjukkan kita bisa melakukan perintah apa saja dan NO PASSWD menunjukkan kalo saat menjalankan perintah itu kita tidak memerlukan password.
7. Sekarang kita coba ganti isi file php tadi dengan ```sudo ls /root``` untuk melihat isi direktori root. Lalu upload ulang file .php nya lalu ubah URL nya seperti di cara tadi. Disini terlihat isinya ada flag.txt
  &nbsp;
  <img width="1674" height="943" alt="Screenshot (293)" src="https://github.com/user-attachments/assets/95b8431e-e06c-45d7-9515-9d4aba0f2255" />

  &nbsp;
  <img width="1668" height="941" alt="Screenshot (296)" src="https://github.com/user-attachments/assets/2dc5c039-50ed-45de-a235-44903e8a5c6a" />

  &nbsp;
8. Nah flag soal ctf itu ada di dalam file flag.txt ini. Gunakan file .php tadi lalu ubah lagi command nya dengan ```sudo cat /root/flag.txt``` dan upload ulang file nya. Ini gunanya untuk memanggil isi dari flag.txt ini.
  &nbsp;
  <img width="1669" height="949" alt="Screenshot (298)" src="https://github.com/user-attachments/assets/3b286ae7-3a8b-4406-8788-b8dea2a2409c" />

  &nbsp;
  <img width="1668" height="947" alt="Screenshot (299)" src="https://github.com/user-attachments/assets/a0e036c1-c473-4de9-8db8-fd76041c95a4" />

  &nbsp;
9. Nah flag nya sudah ketemu, tinggal salin dan di paste saja di kolom jawaban soal ctf.
&nbsp;
<img width="1920" height="871" alt="Screenshot (306)" src="https://github.com/user-attachments/assets/d4fe9dae-74a3-44a9-a942-ffa2e1325f22" />
