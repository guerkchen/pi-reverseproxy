# pi-reverseproxy
Access port 22 &amp; 80 of my raspberry pi behind firewall by using a reverse tunnel over a linux server in the internet.
It is kind of a no brainer, I want my Pi to be accessible from the internet via Webhooks or SSH.
Since my pi is mostly powered behind a Router with dynamic IP and Firewall, this setup helps me to be independent from these factors.

# setup
![grafik](https://github.com/guerkchen/pi-reverseproxy/assets/29518587/d574db30-7eb1-421e-8397-6ef0639cb2d7)

# SSH Setup
My setup mostly relies on [this](https://www.rustimation.eu/index.php/reverse-ssh-tunnel-schritt-fur-schritt/) tutorial.
There is just a small mistake: To make the reverse SSH Tunnel accessible from any device, a '*' must be added to the command:
```ssh -fN -R *:2200:localhost:22 user@gateway```

# HTTP Setup
Since getting a SSL-Certificate on my raspberry by using Let's encrypt can raise issues, when it is running behind a proxy, I choose to let my Gateway-Server handle the SSL-Encryption.
The connection between my gateway and pi is encrypted by SSH anyway.
By using this setup I do not have to worry about expiration of the pi certificates, when it is offline for several month, since my server is online 24/7.
I choose a subdomain ```pi.gateway``` which will be forwarded to my pi, containing the path.
This way, I can easily add Sub-Subdomains in the nginx conf on my pi and do not have to touch my gateways nginx config.
