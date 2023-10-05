일부 암호화 알고리즘에 사용되는 난수 하나를 미리 생성해 보안을 높이는 방법

-------

```
mkdir /etc/nginx/ssl 
cd /etc/nginx/ssl 
openssl dhparam -out dhparams.pem 4096 # 2048비트로 하려면 4096대신 2048로 대체 한다. 
openssl rand 48 
session_ticket.key # 세션 티켓키도 생성 이는 시간이 거의 걸리지 않는다.
```