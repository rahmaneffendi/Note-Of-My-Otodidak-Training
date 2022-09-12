# KRAKEND

  Hello Gaes, Disini gw mau buat catatan pribadi tentang krakend,

jadi krakend itu salah satu ultra high tool untuk api gateway. dimana kita bisa dengan mudah mengadopsi microservice dan komunikasii yang aman. 

disini gw mau nge run simple app, betul-betul simple ya hehe:

1. Pertama, siapkan 1 buah server, disini os yang saya pake centos 7, kemudian update dan install docker di dalamnya, karena gw akan ngejalanin krakend nya based on docker

2. kemudian buat folder, disini gw namain foldernya "simple-app-v2"

3. dalam folder tersebut, buat 2 buah file; Dockerfile & simple2.json, yang isinya bisa temen2 liat di bawah ini :

<img width="357" alt="image" src="https://user-images.githubusercontent.com/99697182/189606664-dbd36f36-30de-43f4-ab76-56eb758b16c8.png">

4. kemudian build menjadi image

```
docker build -t simple6-api .
```

5. lalu jalan kan image nya menjadi container

```
docker run -d -p 8888:8080 simple6-api run --config "/etc/krakend/simple2.json"
```

6. dan kita liat container nya berjalan

<img width="787" alt="image" src="https://user-images.githubusercontent.com/99697182/189607343-e364bd4b-b659-4fd1-9010-21fbac925482.png">

7. kita cek di browser apakah sudah betul konfigurasinya

<img width="243" alt="image" src="https://user-images.githubusercontent.com/99697182/189607472-68fd301a-3ef9-4f2f-9dd4-4703e9397c21.png">

nah sudah ada response, itu berarti api gateway nya sudah berjalan

kalau ada pertanyaan, bisa tanyakan di kolom komentar
