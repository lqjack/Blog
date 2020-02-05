#!/bin/bash
#
#
#
#this is nginx-install.sh
#author : Jack
#date 2018.10.6
#
#
#
#

[ $(id -u) != "0" ]&& echo "The shell execute need the root permission." && exit 1


# check the user role
if [ ! -d /opt ];then
	# check whether /opt exist
	mkdir /opt && cd /opt
else
	cd /opt
fi


read -p "Start to install Nginx(y/n):" cho


case $cho in
y)
	wget http://nginx.org/download/nginx-1.14.0.tar.gz
	a=nginx-1.14.0
	;;
n)
	exit 1
	;;
*)
	echo "Please input the right command（y/n）:"
	exit 1
	;;
esac



if [ $? -eq 0 ];then
#unzip the file
	tar zxf $a.tar.gz
else
	echo "Cannot download the file correctly ！"
	exit 1
fi



nginxu=`awk -F: '$0~/nginx/' /etc/passwd|wc -l`
nginxg=`awk -F: '$0~/nginx/' /etc/group|wc -l`



# configure the environment
if [ $nginxu -ne 0 ] && [ $nginxg -ne 0 ];then
# check the user/group 
	echo "nginx user group exist."
else
	useradd -M -s /sbin/nologin nginx
fi



yum install gcc gcc-c++ pcre pcre-devel zlib-devel -y

cd /opt/$a
./configure \
--prefix=/usr/local/nginx \
--user=nginx \
--group=nginx \
--with-http_stub_status_module


make && make install


if [ $? -eq 0 ];then
	# create the soft link
	ln -s /usr/local/nginx/sbin/nginx /usr/local/sbin/
else
	echo "install failed !!!"
fi