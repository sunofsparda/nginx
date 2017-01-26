# nginx

#TASK1

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

