# CloudFlare Tunnel

## Download Cloudflared Tool

```
wget https://github.com/cloudflare/cloudflared/releases/latest/download/cloudflared-linux-amd64.deb
```

## Install Cloudflared Tool

```
sudo dpkg -i cloudflared-linux-amd64.deb
```

## Start Local Web Server

```
sudo service apache2 start
```

## Run Cloudflared

```
cloudflared --url localhost
```

{% hint style="info" %}
Visit the given URL
{% endhint %}

