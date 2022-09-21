# Step

1. Install pyhton 

```
yum install gcc openssl-devel bzip2-devel libffi-devel -y
```

```
curl -O https://www.python.org/ftp/python/3.8.1/Python-3.8.1.tgz
```

```
tar -xzf Python-3.8.1.tgz
```

```
cd Python-3.8.1
```

```
./configure --enable-optimizations
```

```
make altinstall
```

```
python3.8
```

2. Buat Konfigurasi Python

```
cd /opt
```

```
mkdir python
```

```
cd python/
```

```
python3.8 -m venv venv
```

```
pip install fastapi
```

```
pip install uvicorn
```

```
nano main.py
```

masukan skrip berikut

```
from typing import Union
import uvicorn
from fastapi import FastAPI


app = FastAPI()

@app.post("/post")
def create_item():
    return "hello"

uvicorn.run(app, host="0.0.0.0", port=8003)
```

kemudian atur firewall nya

```
firewall-cmd --add-port=8003/tcp --permanent
```

```
firewall-cmd --reload
```

```
firewall-cmd --list-all
```

kemudian jalankan 

```
python3.8 main.py
```

setelah itu keluar

`
ctrl + c
`

kemudian kita akan menjalankannya secara daemon

```
nano daemon.sh
```

masukan script nya

```
#!/bin/bash
cd /opt/python
source /opt/python/venv/bin/activate
python3.8 /opt/python/main.py
```

atur izin nya

```
chmod +x /opt/python/daemon.sh
```


kemudian kita masuk ke sistem linux

```
 cd /etc/systemd/system
```

dan buat service nya

```
nano post-testing.service
```

masukan script nya

```
[Unit]
Description=ejbca REST api , talk to web service(SOAP)

[Service]
Type=simple
User=root
Group=root
ExecStart=/opt/python/daemon.sh

[Install]
WantedBy=multi-user.target
```

kemudian atur service nya

```
systemctl enable post-testing.service
```

```
systemctl start post-testing.service
```

```
systemctl status post-testing.service
```

terakhir kita bisa cek service nya

```
ss -tulnp
```


