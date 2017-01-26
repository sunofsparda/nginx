# nginx

#TASK1
1. Install latest stable version of NGINX using yum package manager.
2. Install nginx from source using latest stable version with following conditions:
install under path “/home/<user>/nginx” replace <user> with any username here and in the following conditions.
binary file path “/home/<user>/nginx/sbin/nginx”
config file path “/home/<user>/nginx/conf/nginx.conf”
error log path “/home/<user>/nginx/logs/error.log”
access log path “/home/<user>/nginx/logs/access.log”
PID file path  “/home/<user>/nginx/logs/nginx.pid”
NGINX should run under user <user>
build with http_ssl module
build with http_realip module
build without http_gzip module
build with 3rd party module nginx-module-vts (https://github.com/vozlt/nginx-module-vts)
nginx should be compiled with PCRE and OpenSSL

During installation process you’ll need some additional packages:
Packages for configuring and compiling source code (requires superuser):
   yum install -y gcc gcc-c++ git
Perl Compatible Regular Expressions (PCRE) package: 
use latest version of PCRE (not PCRE2 !) for this task
can be downloaded from http://www.pcre.org/

OpenSSL package:
use latest 1.0* version (e.g. 1.0.2j but not 1.1.0b) for this task
can be downloaded from https://www.openssl.org/source/

3. Upload compiled NGINX to GitHub.
Create your own account on GItHub
Create public repository named “nginx” in your account
Push your compiled nginx to created repository
You can use guides on GitHub (https://guides.github.com/) or any other online documentation

4. Create init script for NGINX. 
Create your own script or find existing one in the internet and put it in /etc/init.d/nginx
Put the copy of that script to “/home/<user>/nginx/sbin/init_script.sh”

5. Create configuration files with the following conditions:
Extract files from “html.tar.gz” archive in lecture materials to your “/home/<user>/nginx/html” folder
Set number of worker processes to 1
Set number of connections per worker to 1024
NGINX should serve your site on port 8080
NGINX should serve your site on domain name same as host’s ip address
<ip-address>:8080 should return “html/index.html” file
<ip-address>:8080/pictures should return files from “html/resources/pictures” 
(e.g. <ip-address>:8080/pictures/01.jpg)
<ip-address>:8080/status should return status page of nginx-module-vts 3rd party module and should be only available from your workstation’s ip-address
<ip-address>:8080/admin should return “html/admin.html” file and should be protected by basic authentification with one or more users, one of which should be user “admin” with password “nginx”. User file should be in “/home/<user>/nginx/conf/” folder
server block should be in a separate config file located under “/home/<user>/nginx/conf/vhosts/backend.conf”
Return custom 404 error page if unexisting file is requested (404.html)

To make nginx-module-vts status page to work, add:
following directive to http block
vhost_traffic_status_zone; 
following directives to “/status” location block
vhost_traffic_status_display;
vhost_traffic_status_display_format html;

6. Start NGINX
Use your init script to start NGINX

7. Upload your NGINX to GitHub
As a result content of your “/home/<user>/nginx/ folder should be in your GitHub “nginx” repository

8. Send email to trainer: 
With email Subject “MTN.NIX.08.NGINX_Task_1”
In the body email should contain text as following:

username=<username>
repository=<repository_clone_url>
ipaddress=<ip_address>

Where:
 <username> - name of the user You run nginx
 <repository_clone_url> - URL to clone Your repository
 <ip_address> You use as a server_name in configs

################################################


yum install -y gcc gcc-c++ git unzip

cd ~

mkdir ~/temp/nginx-install

cd ~/temp/nginx-install

#download nginx
wget http://nginx.org/download/nginx-1.11.9.tar.gz

wget https://ftp.pcre.org/pub/pcre/pcre-8.40.tar.gz

wget https://www.openssl.org/source/openssl-1.0.2j.tar.gz

tar nginx-1.11.9.tar.gz

tar pcre-8.40.tar.gz

tar openssl-1.0.2j.tar.gz

#download nginx-module-vts
wget https://github.com/vozlt/nginx-module-vts/archive/master.zip

unzip master.zip
#rename just to know what is it
mv master.zip nginx-module-vts.zip

cd nginx-1.11.9

#configure and install nginx
./configure --prefix=/home/user/nginx --user=user --with-http_ssl_module --with-http_realip_module --without-http_gzip_module --add-module=/home/user/temp/nginx-module-vts-master --with-pcre=/home/user/temp/pcre-8.40 --with-openssl=/home/user/temp/openssl-1.0.2j

make

make install

