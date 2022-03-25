# How to set up a v2ray client at a linux server

## download and uncompress
```bash
wget https://github.com/v2fly/v2ray-core/releases/download/v4.31.0/v2ray-linux-64.zip

unzip v2ray-linux-64.zip 
```

## set up config
```bash
cd v2ray-linux/

vim config.json

# put the config content copyed from your mobile app, such as `v2rayNG`
```

## run it
```bash
./v2ray

#or

./v2ray &
```

## set up proxychains
```bash
apt install proxychains

vim /etc/proxychains.conf

# change the port number

# use it as `proxychains ping xxx`
```