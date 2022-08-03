



# Recap

1. Berkenalan Teknologi Containerisation menggunakan Docker

2. Mempermudah mendevelop app & mendeploynya
 
3. konsepnya itu kaya plug & play , tinggal mindahin si containernya
 
4. dengan docker mempermudah implementasi kontenerisasi dari build image, bagaimana deploy app di server linux, bagaimana 2 kontener bisa berhubungan satu sama lain
 
5. jadi kalau ada konener yang berjalan di network yang sama dan ingin mengakses kontener yang lain hanya tinggal menggunakan nama kontener sebagai hostnya
 
6. docker volume, cara kita menyinpam data dalam kontener, 
 
7. mengenal persistance volume, dan menggunakan binding volume untuk mempermudah ketika develop app, karena ngga pengen ketika ada kode yang berubah kita harus ng build ulang imagenya, jadi alih-alih seperti itu kenapa kita ngga nge build ulang aplikasi kita  
 
8. publish image ke docker hub yang akan di pakai saat proses deployment
 
9. belajar tool docker compose untuk mempermudah menjalankan multi container dengan 1 comment aja, 
 
10. docker compose mempermudah saat deployment, kita hanya copy aja si docker compose.yml nya , terus kita define aja image nya, dan kita tinggal jalanin comment docker-compose up nya , ini lebih mudah dari pada deploy harus install depedency, app, library dll, dan itu di bundle dalam 1 container aja, 
 
11. belajar stage build secara best practice, dengan mengecilkan size nya
 
12. docker itu nge cache perlayer, jadi proses build image nya lebih cepat, biasanya di gunakan dalam app microservices, biasanya tiap service itu di presentasikan dengan 1 image
 
