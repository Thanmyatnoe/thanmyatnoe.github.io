---
layout: post
title:  "FortiGate and Mikrotik Site to Site VPN and Backup "
subtitle: "Site to Site VPN and Backup "
tags: [Networking]
---

#### Basic Firewall Configuration - FortiGate to Mikrotik IPsec VPN
Diagram 
[![ace](/img/IPSec%20VPN/HighLevel.png)]

IP Address Information 
```
172.17.1.1/24        Fortigate Server Farm 
172.17.10.1/24       Mikrotik Server Farm 

```

FortiGate IPsec VPN Config 

```
Go to VPN >> Click IPsec VPN Tunnel 
Create IPsec VPN 
```
[![ace](/img/IPSec%20VPN/FW_IPsec.png)]

Build လုပ်ပြီးရင် Release ထုတ်ပြီး ကိုထားမဲ့Folder Path လမ်းကြောင်းပေးရပါမယ်။
Release and Output Folder Path Command 

```
dotnet publish -c Release -o ./Folder_Path
```

### Asp.net Core Deploy on IIS 
Asp.Net Core App ကို IIS Web Server Deploy လုပ်မယ်ဆိုရင် Asp.net Core Windows Hosting Bundle Installation လုပ်ပေးဖို့လိုအပ်ပါမယ်။
Link 

```
https://dotnet.microsoft.com/en-us/download/dotnet/6.0
```

### Asp.net Core Deploy on Ubuntu 
Asp.Net Core ကို Ubuntu မှာ Deploy လုပ်မယ်ဆိုအရင်ဆုံး Runtime Installation လုပ်ထားရပါမယ်။ Runtime installation and Packages Link 

```
wget https://packages.microsoft.com/config/ubuntu/20.04/packages-microsoft-prod.deb -O packages-microsoft-prod.deb
sudo dpkg -i packages-microsoft-prod.deb
rm packages-microsoft-prod.deb
sudo apt-get update && \
  sudo apt-get install -y aspnetcore-runtime-6.0
```

Web Server ကို Nginx သုံးထားပါတယ်။ Ngnix မသုံးပဲ အခြား Web Server လဲအသုံးပြုလို့ရပါတယ်။
```
apt install nginx 
mv project folder /var/www/
```
Web Server installation လုပ်ပြီးရင် Release ထုတ်ထားတဲ့ Folder ကို /var/www/ ကိုပို့ပြီး permission ပေးပါမယ်။

```
mv project folder /var/www/
sudo chown -R username:username /var/www/path
sudo chmod -R 755 /var/www/path
```
Nginx web server configuration ရေးပေးရပါမယ်။
Create configuration file (/etc/nginx/sites-available/example.com or example)

```
server {
       listen 80;
       listen [::]:80;
       root /var/www/Release_Folder;
       index index.html;
       location / {
               try_files $uri $uri/ =404;
       }
}
```
ရေးထားတဲ့ Configuration File ကို Link လုပ်ပေးရပါမယ်။
```
sudo ln -s /etc/nginx/sites-available/example.com or example /etc/nginx/sites-enabled/example.com or example
```

