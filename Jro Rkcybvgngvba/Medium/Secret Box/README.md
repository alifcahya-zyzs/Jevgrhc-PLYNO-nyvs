# How to Solve Secret Box

<br>

1. Pertama luncurkan instans dan buka website soal, download juga file source code yang ada. Disini juga ada petunjuk untuk menggunakan SQLi untuk menyelesaikan ctf ini. 
   
   &nbsp;
   
   <img width="1920" height="945" alt="Screenshot (401)" src="https://github.com/user-attachments/assets/9e8b922e-8329-41ff-8a6c-2c3ae632604a" />
   
   &nbsp;
   
   <img width="1920" height="947" alt="Screenshot (402)" src="https://github.com/user-attachments/assets/3108f05a-c418-42ac-b710-9d695b79bc00" />

   <br>

2. Sebelum melakukan login atau sign in di website soal, kita lihat dulu isi source code hasil download nya dengan cara: 


   a. Buka power shell windows lalu masuk ke direktori dimana file hasil unduhan itu disimpan. 

   
   b. Ekstrak file source.tar.gz dengan cara mengetik perintah: 
  
   ```PowerShell
    tar -xvf source.tar.gz
   ```

    
   c. Setelah itu masuk ke folder hasil ekstrak source tadi dengan `cd source` lalu `ls` maka akan terlihat ada 3 isi yaitu `app`, `db`, dan `docker-compose.yml`.

  
     
   <img width="1013" height="812" alt="Screenshot (387)cut" src="https://github.com/user-attachments/assets/7507c0c2-e06d-4666-a514-f0be7a6fdb66" />

   
   d. Masuk ke `cd db` lalu `ls` dan akan terlihat 2 file yaitu `DockerFile`, dan `initdb.sql`, coba lihat isi file `initdb.sql` dengan:
  
   ```PowerShell
   cat initdb.sql
   ```

    
   e. Maka akan terlihat banyak table disini, fokus ke bagian paling bawah dan tabel secrets dari hasil cat ini, ada petunjuk owner id dan flag yang terletak di tabel secrets. Lebih tepatnya flag berada pada kolom content dari id owner. 
     
     
   &nbsp; 
   
   <img width="1920" height="820" alt="Screenshot (388)" src="https://github.com/user-attachments/assets/ef007f07-1c8c-4de7-8127-b8c2016d8de4" />

   <br>

3. Setelah mengetahui dimana letak kita akan menjalankan SQLi yaitu di tabel insert secrets, kita sign in dan login di website soal tadi menggunakan username dan pasword bebas.

   &nbsp;
   
   <img width="1920" height="941" alt="Screenshot (396)" src="https://github.com/user-attachments/assets/a3cfc440-df4d-4b3f-8e4d-d19cd876888a" />

   <br>
   
4. Coba buat secret bebas dengan sisipan karakter SQL ini `'` dibelakang kalimat/kata terakihir untuk menghentikan string bawaan di depannya. lalu submit, jika website memiliki kerentanan SQLi maka karakter `'` ini akan menyebabkan eror. 
   &nbsp;
   <img width="1920" height="942" alt="Screenshot (403)" src="https://github.com/user-attachments/assets/780a4521-8506-4f37-8d46-79677c8fc358" />

   <br>
   
5. Disini terbukti website rentan terhadap SOLi di tabel insert secrets ini. 
   <img width="1920" height="945" alt="Screenshot (404)" src="https://github.com/user-attachments/assets/9679ba52-a4a4-4218-89eb-6defc83bdb07" />
   
   <br>
   
6. Coba buat new secrets lagi dengan perintah SOLi untuk mencari flag menggunakan owner id di source code tadi

   &nbsp;
   
   <img width="1920" height="945" alt="Screenshot (397)" src="https://github.com/user-attachments/assets/b15b51a9-b61b-4eb9-a0e0-f52bd60bc924" />

   &nbsp;

   ```sql
    '||(select content from secrets where owner_id='e2a66f7d-2ce6-4861-b4aa-be8e069601cb')||'
   ```

   
   `'` gunanya untuk menghentikan atau memulai string pada SOL tergantung pada dimana peletakannya, di depan sendiri itu ada tanda `'` untuk menghentikan string bawaan yang ada didepannya agar kita bisa menyisipkan string baru.

   `||` gunanya untuk menyambungkan string pertama dengan string kedua agar tidak terjadi eror karena ada dua string dalam satu query. Intinya seperti lem penghubung antar string.


   `()` gunanya untuk membungkus perintah/request SQL agar diproses secara terpisah dan didahulukan agar tidak eror.


   `select content from secrets where owner_id='e2a66f7d-2ce6-4861-b4aa-be8e069601cb'` Nah yang ini adalah perintah request ke database SQL nya.


   `select content from secrets` meminta SQL untuk mengambil konten dari tabel secret.


   `where owner_id='e2a66f7d-2ce6-4861-b4aa-be8e069601cb'` yang ini memfilter SQL agar mengambil konten yang spesifik dari akun target dengan owner_id yang spesifik itu.
   
   <br>

7. Submit perintah SQLi itu lalu lihat hasil nya, jika langsung menghasilkan flag maka berhasil.

   &nbsp;

   <img width="1920" height="944" alt="Screenshot (398)" src="https://github.com/user-attachments/assets/ec8af95b-c48d-4e3c-b510-62403d78f75e" />

   <br>
   
8. Salin flag lalu paste di kolom jawaban soal ctf. 
   
   &nbsp;
   
   <img width="1920" height="944" alt="Screenshot (400)" src="https://github.com/user-attachments/assets/76d0bc9a-3720-4f09-be0a-7d4f7d114837" />

