---
layout: post
title: Certificate 
date: 2016-02-24 22:44
image: /assets/images/markdown.jpg
headerImage: false
tag:
- certificate
star: true
category: blog
author: Jack
description: Certificate 
---

* 使用keytool命令生成证书：
```shell
keytool 
-genkey
-alias test(别名) 
-keypass lqjacklee(别名密码) 
-keyalg RSA(算法) 
-keysize 1024(密钥长度) 
-validity 365(有效期，天单位) 
-keystore test.keystore(指定生成证书的位置和证书名称) 
-storepass lqjacklee(获取keystore信息的密码)
```

```shell
keytool -genkey -alias test -keypass lqjacklee -keyalg RSA -keysize 1024 -validity 365 -keystore test.keystore -storepass lqjacklee
```

为客户端生成证书:
```shell
keytool 
-genkey 
-alias client 
-keypass lqjacklee
-keyalg RSA
-storetype PKCS12 
-keypass lqjacklee 
-storepass lqjacklee 
-keystore client.p12
```

```Shell
keytool -genkey -alias client1 -keypass lqjacklee -keyalg RSA -keysize 1024 -validity 365 -storetype PKCS12 -keystore client1.p12 -storepass lqjacklee
```

* 让服务器信任客户端证书:
1. 由于不能直接将PKCS12格式的证书库导入，
必须先把客户端证书导出为一个单独的CER文件，使用如下命令：
```shell
keytool -export -alias client1 -keystore client1.p12 -storetype PKCS12 -keypass lqjacklee -file client.cer
```

注意：keypass：指定CER文件的密码，但会被忽略，而要求重新输入

2. 将该文件导入到服务器的证书库，添加为一个信任证书：
keytool -import -v -file client.cer -keystore test.keystore -storepass lqjacklee


完成之后通过list命令查看服务器的证书库，可以看到两个证书，一个是服务器证书，一个是受信任的客户端证书：
 

* 让客户端信任服务器证书:
1. 由于是双向SSL认证，客户端也要验证服务器证书，
因此，必须把服务器证书添加到浏览器的“受信任的根证书颁发机构”。
由于不能直接将keystore格式的证书库导入，必须先把服务器证书导出为一个单独的CER文件，使用如下命令：
keytool -keystore D:/keys/tomcat.keystore -export -alias tomcat6 -file D:/keys/server.cer

2. 双击server.cer文件，按照提示安装证书，
将证书填入到“受信任的根证书颁发机构”。
填入方法：
打开浏览器   - 工具  -  internet选项-内容- 证书-把中级证书颁发机构里的www.localhost.com(该名称即时你前面生成证书时填写的名字与姓氏)证书导出来-再把导出来的证书导入  受信任的根颁发机构  就OK了。


# 配置Tomcat服务器:
```shell 
<Connector  port="8443"
protocol="org.apache.coyote.http11.Http11NioProtocol" SSLEnabled="true"
maxThreads="150"
scheme="https"
secure="true"
clientAuth="true"
sslProtocol="TLS"
keystoreFile="D:/keys/tomcat.keystore"
keystorePass="123456"
truststoreFile="D:/keys/tomcat.keystore"
truststorePass="123456" />
```

 
> 属性说明：
clientAuth:设置是否双向验证，默认为false，设置为true代表双向验证
keystoreFile:服务器证书文件路径
keystorePass:服务器证书密码
truststoreFile:用来验证客户端证书的根证书，此例中就是服务器证书
truststorePass:根证书密码
 

注意：
① 设置clientAuth属性为True时，需要手动导入客户端证书才能访问。
② 要访问https请求 需要访问8443端口，访问http请求则访问Tomcat默认端口（你自己设置的端口，默认8080）即可。


强制 https 访问

在 tomcat /conf/web.xml 中的 </welcome- file-list> 后面加上这

```
<login-config>    
	<!-- Authorization setting for SSL -->    
	<auth-method>CLIENT-CERT</auth-method>    
	<realm-name>Client Cert Users-only Area</realm-name>    
</login-config>    

<security-constraint>    
	<!-- Authorization setting for SSL -->    
	<web-resource-collection >    
		<web-resource-name >SSL</web-resource-name>    
		<url-pattern>/*</url-pattern>    
	</web-resource-collection>    
	<user-data-constraint>    
		<transport-guarantee>CONFIDENTIAL</transport-guarantee>    
	</user-data-constraint>    
</security-constraint> 
```

完成以上步骤后，在浏览器中输入http的访问地址也会自动转换为https了。

--------------------------------------------------

* generate key store : 
```shell
keytool -genkey -alias client -keysize 2048 -validity 3650 -keyalg RSA -dname "CN=localhost" -keypass lqjacklee -storepass lqjacklee -keystore ClientCert.jks
```
```shell
export certificate:
keytool -export -alias client -keystore ClientCert.jks -storepass lqjacklee -file ClientCert.crt
```
keytool工具不支持导出私钥。


* 生成公钥私钥：
```shell
openssl genrsa -des3 -out private.pem 1024
```

* 创建证书请求：
```shell
openssl req -subj "/C=CN/ST=BJ/L=BJ/O=HW/OU=HW/CN=CL/emailAddress=huawei@huawei.com" -new -out cert.csr -key private.pem	
 ```

* 自签发证书：
```shell
openssl x509 -req -in cert.csr -out public.crt -outform pem  -signkey private.pem -days 3650
```

* keytool生成的证书转换为PEM格式:
```shell
keytool -importkeystore -srcstoretype JKS -srckeystore ServerCert.jks -srcstorepass 123456 -srcalias server -srckeypass 123456 -deststoretype PKCS12 -destkeystore client.p12 -deststorepass 123456 -destalias client -destkeypass 123456 -noprompt
```

* 导出证书：
```shell
openssl pkcs12 -in client.p12 -passin pass:$passwd -nokeys -out client.pem
```

* 导出私钥：
```shell
openssl pkcs12 -in client.p12 -passin pass:$passwd -nocerts -out client.crt
```

* PEM格式证书转换为jks文件:
转换为pkcs12格式：
```shell
openssl pkcs12 -export -in public.crt -inkey private.pem -out server.p12 -name server -passin pass:${passwd} -passout pass:${passwd}
```

* 导入到jks中：
```shell
keytool -importkeystore -srckeystore server.p12 -srcstoretype PKCS12 -srcstorepass ${passwd} -alias server -deststorepass ${passwd} -destkeypass ${passwd} -destkeystore ServerCert.jks
```
