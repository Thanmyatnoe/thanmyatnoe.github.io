---
layout: post
title:  "Angular Deployment"
subtitle: "Angular App Deployment"
tags: [Deployment]
---

#### Angular Build and Release  
Asp.Net Core Build and Release ပြုလုပ်ဖို့ ပထမဆုံး Development PC or Release ထုတ်မဲ့စက်မှာ Node.js and Angular-CLI ရှိဖို့လိုအပ်ပါတယ်။

```
https://nodejs.org/en/download/
npm install –g @angular/cli
```

Node.js and Angular-CLI ထည့်သွင်းပြီးပြီဆို Build လုပ်ပါ။

```
ng build --prod 
```
Build and Relase လုပ်ပြီးလျှင် Deploy လုပ်မဲ့ Server ထဲကို Copy ကူးပါ။ 

```
scp -r /dist/project_name remote_servername@remote_serverip:/server_path
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

