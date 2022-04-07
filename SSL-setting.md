# How to set SSL

## Install Certbot on Ubuntu

```bash
sudo apt-get update
sudo apt-get install certbot
```

## DNS Verification

```bash
sudo certbot certonly --manual --preferred-challenges dns --server https://acme-v02.api.letsencrypt.org/directory -d 'woj.wookingwoo.com'
```

- Do follow the instruction to complete DNS verification: TXT entry at _acme-challenge.woj.wookingwoo.com

- Before proceeding with cerbot DNS verification, run a check to verify if the DNS TXT entry has propagated within reach of your machine.

```bash
dig -t txt _acme-challenge.www.mydomain.com
```

## Change pem to key and crt file

```bash
cd /etc/letsencrypt/live/woj.wookingwoo.com
```

- You can see 'privkey.pem' and 'fullchain.pem'

- Make 'server.crt' and 'server.key' file

```bash
openssl rsa -in privkey.pem -text > server.key

openssl x509 -inform PEM -in fullchain.pem -out server.crt
```

- put them in OnlineJudgeDeploy/data/backend/ssl/

```bash
sudo mv server.key /home/ubuntu/OnlineJudgeDeploy/data/backend/ssl
sudo mv server.crt /home/ubuntu/OnlineJudgeDeploy/data/backend/ssl
```

