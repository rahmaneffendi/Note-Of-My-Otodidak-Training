Disini saya akan mecoba load balancing dari krakend on top docker 

# Step

pertama buat lalu masuk ke folder

```
mkdir simple-app-v8 ; cd simple-app-v8
```

setelah itu buat 2 buah file 

```
touch Dockerfile ; touch simple16.json
```

masukan Scriptnya

```
nano Dockerfile
```

```
FROM devopsfaith/krakend
COPY simple16.json /etc/krakend/simple16.json
```

```
nano simple16.json
```

```
{
  "$schema": "https://www.krakend.io/schema/v3.json",
  "version": 3,
  "name": "Nyoba Krakend Methode Post",
  "timeout": "20000ms",
  "cache_ttl": "300s",
  "output_encoding": "json",
  "port": 8080,
  "sequential_start": false,
  "extra_config": {
    "telemetry/logging": {
      "level": "INFO",
      "prefix": "[NYOBA]",
      "syslog": true,
      "stdout": true,
      "format": "logstash"
    },
    "telemetry/logstash": {
      "enabled": true
    },
    "security/cors": {
      "allow_origins": [
        "*"
      ],
      "expose_headers": [
        "Content-Length"
      ],
      "max_age": "12h",
      "allow_methods": [
        "GET",
        "HEAD",
        "POST",
        "PUT",
        "DELETE"
      ],
      "allow_headers": [
        "x-api-key",
        "Authorization"
      ]
    }
  },
  "endpoints": [
    {
      "endpoint": "/abc",
      "method": "POST",
      "output_encoding": "no-op",
      "backend": [
        {
          "url_pattern": "/post",
          "encoding": "no-op",
          "sd": "static",
          "method": "POST",
          "extra_config": {
            "qos/circuit-breaker": {
              "interval": 60,
              "name": "circuit-breaker-1",
              "timeout": 10,
              "max_errors": 50,
              "log_status_change": true
            }
          },
          "host": [
            "http://192.168.182.143:8003",
            "http://192.168.182.147:8002"
          ],
          "disable_host_sanitize": false
        }
      ],
      "input_headers": [
        "*"
      ]
    }
  ]
}
```

setelah itu build 

```
docker build -t simple16-api .
```

dan jalankan Docker nya

```
docker run -d -p 7070:8080 simple16-api run --config "/etc/krakend/simple16.json"
```

kemudian kita cek di postman

<img width="311" alt="image" src="https://user-images.githubusercontent.com/99697182/191409347-5ec56394-dbc7-4b7b-9b95-db1623bd9fb3.png">

<img width="326" alt="image" src="https://user-images.githubusercontent.com/99697182/191409327-719d8bde-682b-4e52-b22a-fd099dce7022.png">

