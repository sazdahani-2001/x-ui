# x-ui

xray panel with multi-protocol multi-user support

# Function introduction

- System status monitoring
- Support multi-user and multi-protocol, web page visualization operation
- Supported protocols: vmess, vless, trojan, shadowsocks, dokodemo-door, socks, http
- Support for configuring more transport configurations
- Traffic statistics, limit traffic, limit expiration time
- Customizable XRray configuration templates
- Support HTTPS access panel (bring your own domain name + SSL certificate)
- Support one-click SSL certificate application and automatic renewal
- For more advanced configuration items, see the panel

# Installation & Upgrade
```
bash <(curl -Ls https://raw.githubusercontent.com/vaxilu/x-ui/master/install.sh)
```

## Manual installation & upgrade

1. Start with https://github.com/vaxilu/x-ui/releases Download the latest compressed package, generally selecting the 'amd64' architecture
2. Then upload this compressed package to the server `/root/`directory, and use `root`The user logs on to the server

> If your server CPU architecture is not 'amd64', replace 'amd64' in the command with a different architecture yourself

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

> This docker tutorial with docker image by [Chasing66](https://github.com/Chasing66) offer

1. Installation docker

```shell
curl -fsSL https://get.docker.com | sh
```

2. Installation x-ui

```shell
mkdir x-ui && cd x-ui
docker run -itd --network=host \
    -v $PWD/db/:/etc/x-ui/ \
    -v $PWD/cert/:/root/cert/ \
    --name x-ui --restart=unless-stopped \
    enwaiax/x-ui:latest
```

> Build Own mirror

```shell
docker build -t x-ui .
```

## SSL Certificate application

> This feature is used by the tutorial[FranzKafkaYu](https://github.com/FranzKafkaYu) offer

The script has a built-in SSL certificate application function, and the following conditions must be met to apply for a certificate using the script:

- Know your registered Cloudflare email address
- Know the Cloudflare Global API Key
- The domain name has been resolved to the current server through cloudflare

To get the Cloudflare Global API Key:
    ![](media/bda84fbc2ede834deaba1c173a932223.png)
    ![](media/d13ffd6a73f938d1037d0708e31433bf.png)

To use, just enter 'domain name', 'email', 'API KEY', the diagram is as follows:
        ![](media/2022-04-04_141259.png)

Notes:

- The script uses the DNS API for certificate request
- Use Let's Encrypt as the CA by default
- The certificate installation directory is the /root/cert directory
- The certificates requested by this script are all wildcard domain certificates

## TG robot use (under development, not available for the time being)

> This feature and tutorial by [FranzKafkaYu](https://github.com/FranzKafkaYu) offer

X-UI supports daily traffic notification, panel login reminder and other functions through Tg robot, and you need to apply by yourself to use Tg robot
For specific application tutorials, please refer to [blog link] (https://coderfan.net/how-to-use-telegram-bot-to-alarm-you-when-someone-login-into-your-vps.html)
Instructions: Set robot-related parameters in the background of the panel, including:

- Tg Robot Token
- Tg robot ChatId
- TG robot cycle run time, using crontab syntax  

Reference syntax:
- 30 * * * * * // 30s notification per minute
- @hourly // hourly notifications
- @daily // Daily notification (0:00 am)
- @every 8h //Every 8 hours notice  

TG Notice Content:
- Node traffic usage
- Panel login reminder
- Node expiration reminder
- Traffic alert alerts  

More features planned...
## Suggest the system

- CentOS 7+
- Ubuntu 16+
- Debian 8+

# Frequently Asked Questions

## Migrate from v2-ui

First install the latest version of X-UI on the server where v2-ui is installed, and then use the following command to migrate, the native v2-ui's 'all inbound account data' will be migrated to x-ui, 'panel settings and username and password will not be migrated'

> After successful migration, please 'close v2-ui' and 'restart x-ui', otherwise the inbound of v2-ui will cause a 'port conflict' with the inbound of x-ui.

```
x-ui v2-ui
```

## issue closed

All kinds of small white problems see high blood pressure

## Stargazers over time

[! [Stargazers over time] (https://starchart.cc/vaxilu/x-ui.svg)] (https://starchart.cc/vaxilu/x-ui)
