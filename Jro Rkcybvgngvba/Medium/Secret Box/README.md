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
3. Setelah mengetahui dimana letak kita akan menjalankan SQLi yaitu di tabel insert secrets, kita sign in dan login di website soal tadi menggunakan username dan pasword bebas.
   foto login
   <br>
4. Coba buat secret bebas dengan sisipan karakter SQL ini `'` dibelakang kalimat/kata terakihir untuk menghentikan string bawaan di depannya. lalu submit, jika website memiliki kerentanan SQLi maka tanda `'` ini akan menyebabkan eror.
   foto
   <br>
5. Disini terbukti website rentan terhadap SOLi di tabel insert secrets ini.
   foto
   <br>
6. Coba buat new secrets lagi dengan perintah SOLi ini untuk mencari flag menggunakan owner id di source code tadi

   ```sql
    '||(select content from secrets where owner_id='e2a66f7d-2ce6-4861-b4aa-be8e069601cb')||'
   ```

   
  `'` gunanya untuk menghentikan atau memulai string pada SOL tergantung pada dimana peletakannya, di depan sendiri itu ada tanda `'` untuk menghentikan string bawaan yang ada didepannya agar kita bisa menyisipkan string baru.
  <br>
  `||` gunanya untuk menyambungkan string pertama dengan string kedua agar tidak terjadi eror karena ada dua string dalam satu query. Intinya seperti lem penghubung antar string.
  <br>
  `()` gunanya untuk membungkus perintah/request SQL agar diproses secara terpisah dan didahulukan agar tidak eror.
  <br>
  `select content from secrets where owner_id='e2a66f7d-2ce6-4861-b4aa-be8e069601cb'` Nah yang ini adalah perintah request ke database SQL nya.
  <br>
  `select content from secrets` meminta SQL untuk mengambil konten dari tabel secret.
  <br> 
  `where owner_id='e2a66f7d-2ce6-4861-b4aa-be8e069601cb'` yang ini memfilter SQL agar mengambil konten yang spesifik dari akun target dengan owner_id yang spesifik itu.
   
   <br>
7. Submit perintah SQLi itu lalu lihat hasil nya, jika langsung menghasilkan flag maka berhasil.
   foto
   <br>
8. Salin flag lalu paste di kolom jawaban soal ctf.
