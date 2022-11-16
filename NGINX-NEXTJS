#Setup NextJS on Digital Ocean Ubuntu server Terminal Commands
#based on my YouTube video

#login to server
ssh root@ip_address

#Upgrade Server
sudo apt update && sudo apt upgrade

#Install NGINX and Certbot
sudo apt install nginx certbot python3-certbot-nginx

#Allow Firewall Access
sudo ufw allow "Nginx Full"
ufw allow OpenSSH
ufw enable

#Install NPM
apt install npm

#Install pm2
npm install -g pm2

#Check pm2 is working
pm2 status

#go to www root
cd /var/www

#install nvm and nodejs
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.1/install.sh | bash
exec $SHELL
nvm install --lts

#Create NextJS App or clone here
npx create-next-app@latest name_of_app

#Go inside new app directory
cd name_of_app

#(if you cloned the repo from somewhere else, make sure to npm install first
npm install)

#Build it
npm run build

#Create NGINX config file and edit it
cd /etc/nginx/sites-available
touch name_of_app
nano name_of_app

[SEE OTHER GIST FOR CONFIG FILE CONTENTS] 
#https://gist.github.com/oelbaga/5019647715e68815c602ff05cff2416e#file-ubuntu-nextjs-nginx-config-file

#Option1 Syslink the file in sites-enabled
sudo ln -s /etc/nginx/sites-available/name_of_app /etc/nginx/sites-enabled/name_of_app

#Option 2 No need to use sites-enabled
nano /etc/nginx/nginx.conf  
change  include /etc/nginx/sites-enabled/*; to  include /etc/nginx/sites-available/*;

#make Sure NGINX file is good
nginx -t

#remove the default config files
cd /etc/nginx/sites-available
rm default
cd /etc/nginx/sites-enabled
rm default

#restart NGINX to reload config files
systemctl restart nginx

#Go to site directory and launch it with pm2
cd /var/www/name_of_app

#launch app with pm2
pm2 start npm --name name_of_app -- start

#Create SSL with letsencryot
sudo certbot --nginx -d domainname.com



————— helpful commands ————
pm2 start npm --name name_of_app -- start  (make sure you're inside the site's directory first)
systemctl restart nginx (restart NGINX)
sudo certbot --nginx -d domainname.com (Add SSL)
