## download
```shell
Ubuntu or Debian
apt install certbot
apt install [[letsencrypt]]  (안에 certbot 포함)
snap 다운 후 설치

etc
??
```


```shell
웹서버 정지
sudo systemctl stop nginx

certbot certonly --standalone -d sample.com

 -nginx : 기본 명령에 웹 서버(ex. nginx, apache 등) 이름을 옵션 값으로 입력.
 -standalone : 인증서 발급 방식은 옵션을 붙여 사용할 수 있습니다.(ex. standalone, webroot, manual 등)
 -manual : 수동 발급으로 인증서를 가져와 도메인 검증을 직접 수행하며, 자동 갱신은 지원되지 않습니다.
    - —preferred-challenges dns : DNS 방식의 경우
 -d [Domain Name] : -d 옵션은 발급할 인증서의 도메인을 입력하는 부분입니다. 여로 도메인을 사용하는 경우 -d를 계속 붙이거나 콤마(,)로 구분하여 입력합니다.(ex. -d example.com, sub1.example.com, sub2.example.com…)
 certonly : 인증서 생성 및 갱신만 진행하는 옵션으로 인증서 관련 내용을 임의로 수정하지 않도록 주의.
```


## 인증서 자동 갱신([[Let's Encrypt]])
```bash
cd /bin
sudo vi letsencrypt.sh
```

```bash
#!/bin/sh
sudo systemctl stop nginx
sudo certbot renew > /var/log/letsencrypt/letsencrypt_renew.log
fuser -k 80/tcp
sudo systemctl start nginx 
```

```bash
sudo chmod +x letsencrypt.sh 
sudo crontab -e 
30 4 * * 0 letsencrypt.sh


test
sudo certbot renew --dry-run
```
