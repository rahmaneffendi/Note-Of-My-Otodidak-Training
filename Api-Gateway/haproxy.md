```
global
   log /dev/log local0
   log /dev/log local1 notice
   chroot /var/lib/haproxy
   stats timeout 30s
   user haproxy
   group haproxy
   daemon

defaults
   log global
   mode http
   option httplog
   option dontlognull
   timeout connect 10000
   timeout client 30000
   timeout server 30000
   maxconn 50000
   retries 10

listen stats
   bind *:9000
   stats enable
   stats uri /monitoring
   stats realm Haproxy\ Statistics
   stats auth admin:admin
   stats admin if TRUE
   default_backend http_back

frontend http_front
   bind *:1000
   mode http
   default_backend http_back

backend http_back
   balance roundrobin
   server unotoken-web-poc-1 10.10.10.237:22222 check
   server unotoken-web-poc-2 10.10.10.237:22223 check
```
