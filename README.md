# x-ui (English Panel)

Xray panel that supports multiple protocols and multiple users. this panel is https://github.com/vaxilu/x-ui but i have changed it to english and also added support for Vless with Xray version 1.70 and above.

# Function introduction

- System status monitoring
- Supports multiple users and multiple protocols, web page visualization operation
- Supports protocols: vmess, vless, trojan, shadowsocks, dokodemo-door, socks, http
- Supports configuration of more transmission configurations
- Traffic statistics, traffic limit, expiration limit
- Customizable xray configuration templates
- Support https access panel (self-provided domain name + ssl certificate)
- Support one-click SSL certificate application and automatic renewal
- For more advanced configuration items, see the panel

# Installation & Upgrade

```
bash <(curl -Ls https://raw.githubusercontent.com/pouyasamie/x-ui/master/install.sh)
```

## Manual installation & upgrade

1. First download the latest compressed package from https://github.com/pouyasamie/x-ui/releases, generally choose the `amd64` architecture
2. Then upload this compressed package to the server's `/root/` directory and log in to the server as `root` user

> If your server's CPU architecture is not `amd64`, replace `amd64` in the command with other architectures

```
cd /root/
rm x-ui/ /usr/local/x-ui/ /usr/bin/x-ui -rf
tar zxvf x-ui-linux-amd64.tar.gz
chmod +x x-ui/x-ui x-ui/bin/xray-linux-* x-ui/x-ui.sh
cp x-ui/x-ui.sh /usr/bin/x-ui
cp -f x-ui/x-ui.service /etc/systemd/system/
mv x-ui/ /usr/local/
systemctl daemon-reload
systemctl enable x-ui
systemctl restart x-ui
```

## Install using docker

> This docker tutorial is similar to Docker image provided by [Chasing66](https://github.com/Chasing66)

1. Install docker

```shell
curl -fsSL https://get.docker.com | sh
```

2. Install x-ui

```shell
mkdir x-ui && cd x-ui
docker run -itd --network=host \
-v $PWD/db/:/etc/x-ui/ \
-v $PWD/cert/:/root/cert/ \
--name x-ui --restart=unless-stopped \
enwaiax/x-ui:latest
```

> Build your own image

```shell
docker build -t x-ui .
```

## SSL certificate application

> This function and tutorial are provided by [FranzKafkaYu](https://github.com/FranzKafkaYu)

The script has a built-in SSL certificate application function. To use this script to apply for a certificate, the following conditions must be met:

- Know the Cloudflare registration email address
- Know the Cloudflare Global API Key
- The domain name has been resolved to the current server through cloudflare

When using it, just enter `domain name`, `email`, `API KEY`.

Notes:

- This script uses the DNS API for certificate application
- Let'sEncrypt is used as the CA by default
- The certificate installation directory is /root/cert
- All certificates applied for in this script are wildcard certificates

## Use of Tg robot (under development, temporarily unavailable)

> This function and tutorial are provided by [FranzKafkaYu](https://github.com/FranzKafkaYu)

X-UI supports daily traffic notification, panel login reminder and other functions through Tg robot. To use Tg robot, you need to apply for it yourself
For specific application tutorials, please refer to [blog link](https://coderfan.net/how-to-use-telegram-bot-to-alarm-you-when-someone-login-into-your-vps.html)
Instructions: Set robot-related parameters in the panel background, including

- Tg robot Token
- Tg robot ChatId
- Tg robot cycle running time, using crontab syntax

Reference syntax:

- 30 \* \* \* \* \* //Notify at the 30th second of every minute
- @hourly //Notify every hour
- @daily //Notify every day (at midnight)
- @every 8h //Notify every 8 hours

TG notification content:

- Node traffic usage
- Panel login reminder
- Node expiration reminder
- Traffic warning reminder

More features are being planned...

## Recommended system

- CentOS 7+
- Ubuntu 16+
- Debian 8+

# FAQ

## Migrate from v2-ui

First install the latest version of x-ui on the server where v2-ui is installed, and then use the following command to migrate, which will migrate `all inbound account data` of the local v2-ui to x-ui, `panel settings and username and password will not be migrated`

> After the migration is successful, please `close v2-ui` and `restart x-ui`, otherwise the inbound of v2-ui will cause `port conflict` with the inbound of x-ui

```
x-ui v2-ui
```

## Issue closed

Various newbie questions make my blood pressure very high

## Stargazers over time

[![Stargazers over time](https://starchart.cc/vaxilu/x-ui.svg)](https://starchart.cc/vaxilu/x-ui)
