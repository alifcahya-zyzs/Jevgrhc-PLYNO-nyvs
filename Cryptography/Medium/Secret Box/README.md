# How to Solve Secret Box
 <br>
1. Pertama luncurkan instans dan buka website soal, download juga file source code yang ada. Disini juga ada petunjuk untuk menggunakan SQLi untuk menyelesaikan ctf ini.
  2 foto
  <br>
2. Sebelum melakukan login atau sign in di website soal, kita lihat dulu isi source code hasil download nya dengan cara:
  a. Buka power shell windows lalu masuk ke direktori dimana file hasil unduhan itu disimpan.
  b. Ekstrak file source.tar.gz dengan cara mengetik perintah: 
  
   ```PowerShell
    tar -xvf source.tar.gz
   ```
    
  c. Setelah itu masuk ke folder hasil ekstrak source tadi dengan `cd source` lalu `ls` maka akan terlihat ada 3 isi yaitu
    foto
  d. Masuk ke `cd db` lalu `ls` dan akan terlihat 2 file, coba lihat isi file `initdb.sql` dengan:
  
   ```PowerShell
   cat initdb.sql
   ```
    
  e. Maka akan terlihat banyak table disini, fokus ke bagian paling bawah dan tabel secret dari hasil cat ini, ada petunjuk owner id dan flag yang terletak di tabel secrets. Lebih tepatnya flag berada pada kolom content dari id owner.
    foto hasil cat lengkap
    <br>
3. Setelah mengetahui dimana letak kita akan menjalankan SQLi yaitu di tabel insert secrets, kita sign in dan login di website soal tadi.
