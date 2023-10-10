오픈 소스 웹서버

Ubuntu , Debian 에서 설치법

```
sudo apt update
sudo apt list --upgradable

cd /etc/nginx

sudo ln -s /etc/nginx/sites-available/해당 파일 /etc/nginx/sites-enabled
L (sites-available 파일 작성 후 sites-enabled 로 심볼릭)

nginx.conf 에 추가 (버전 정보 숨)
server_tokens on;  
proxy_pass_header Server;

sudo apt install nginx-extras  //서버 정보 삭제

nginx.conf http 추가
more_clear_headers Server;
more_clear_headers X-Powered-By;

```


인증서 ([[certbot]]) 

보안키 ([[dhparam]])
```shall
mkdir /etc/nginx/ssl   
openssl dhparam -out /etc/nginx/ssl/dhparam.pem 4096

ssl_dhparam /etc/nginx/ssl/dhparam.pem; 추가 
```

암호화 알고리즘 ([[cipher]])
```shall
/usr/bin/openssl ciphers -s -v
체크 후
https://wiki.mozilla.org/Security/Server_Side_TLS#Modern_compatibility 에서 확인

https://ssl-config.mozilla.org/ 에서 자동소스 만들어

예
ssl_protocols TLSv1.3;
ssl_prefer_server_ciphers off; 

- listen 443 ssl : SSL-TLS 서비스를 제공할 포트를 지정합니다.  
- ssl on : SSL-TLS 를 켭니다.  
- ssl_protocols : 사용할 SSL-TLS 버전을 지정합니다.  
- ssl_ciphers : 사용할 암호 알고리즘을 지정합니다.  
- ssl_prefer_server_ciphers : SSL-TLS 협상 과정에서 서버에 설정한 암호 알고리즘을 우선하며 off 일 경우 알고리즘을 약화시켜서 공격할 수가 있
```

사이트 안정성 확인 사이트
https://www.ssllabs.com/ssltest/



-----
```
#upstream app {
#       ip_hash;
#       server 172.26.11.253:8000;
#}
server {
listen 80;
listen [::]:80;
server_name kenaz-translation.srabb.net;
location / {
return 301 https://$host$request_uri;
}
#       return 404;
}
server {
listen 443 ssl http2;
listen [::]:443 ssl http2;
server_name kenaz-translation.srabb.net;

ssl_certificate /etc/letsencrypt/live/kenaz-translation.srabb.net/fullchain.pem;
ssl_certificate_key /etc/letsencrypt/live/kenaz-translation.srabb.net/privkey.pem;
ssl_dhparam /etc/nginx/ssl/dhparam.pem;
ssl_prefer_server_ciphers off;
ssl_protocols TLSv1.3;

location / {
proxy_pass_header Server;
#               proxy_pass_request_headers off; //이거 하면 세션 공유 안됨
proxy_pass http://172.26.11.253:8000;
#       proxy_pass http://app;
}
}

```

