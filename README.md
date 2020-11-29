# HTTPS-LAN
HTTPS gateway in LAN

## Reason

Many hight version software repository using HTTPS, like Docker Kubernate Gradle, and this is a good feature. We want an easy way to use HTTPS in the LAN repository server. so it is born.

English is not my first language, if this document has a language grammar error, please help us rewrite it.

## Before the start
- Install docker docker-compose

- The LAN must be connected to the WAN, The Certbot will auto-renew the certificate

- Change your domain nameservers to Luadns or Cloudflare

- The Luadns allowed changing A record to LAN IP, but many routes have RFC1918 problem, you can set the route whitelist

- We recommend using Luadns, The Cloudflare doesn't allow config LAN IP, you can use a custom DNS server, or config the route DNS

## Guide

### 1. modify .env
``` sh
# both support Luadns and Cloudflare-DNS, if you are used Freenom free domain, please use the Luadns.

# if you are using Cloudflare
#      set up MY_CLOUDFLARE_TOKEN
# if you are using Luadns
#      set up MY_LUADNS_EMAIL, MY_LUADNS_TOKEN
# and then 
#      set up MY_DOMAIN and MY_EMAIL

vi .env

```
### 2. init
``` sh
# init nginx config
docker-compose -f ./docker-compose.init.yaml run --rm common_nginx_init 

# init certbot with luadns
docker-compose -f ./docker-compose.init.yaml run --rm common_certbot_luadns_init 

# init certbot with cloudflare
docker-compose -f ./docker-compose.init.yaml run --rm common_certbot_cloudflare_init

```

### 3. start
``` sh
# run with luadns
docker-compose up common_certbot_luadns gateway_nginx

# run with Cloudflare
docker-compose up common_certbot_cloudflare gateway_nginx
```