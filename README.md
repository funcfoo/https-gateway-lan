# https-lan
HTTPS gateway in LAN

## Guide

### 1. modify .env
``` sh
# both support lua-dns and cloudflare-dns, if you are used freenom free domain, please use the lua-dns.

# if you are used cloudfalre
#      set up MY_CLOUDFLARE_TOKEN
# if you are used luadns
#      set up MY_LUADNS_EMAIL, MY_LUADNS_TOKEN
# and then 
#      set up MY_DOMAIN and MY_EMAIL

vi .env

```
### 2. init
``` sh
# first init nginx config
docker-compose -f ./docker-compose.init.yaml run --rm common_nginx_init 

# first init certbot with luadns
docker-compose -f ./docker-compose.init.yaml run --rm common_certbot_luadns_init 

# first init certbot with cloudflare
docker-compose -f ./docker-compose.init.yaml run --rm common_certbot_cloudflare_init

```

### 3. start
``` sh
# run with luadns
docker-compose up common_certbot_luadns gateway_nginx

# run with cloudflare
docker-compose up common_certbot_cloudflare gateway_nginx
```