# Tomcat 配置证书服务
以下是PFX证书的安装
    <Connector port="8443"
    protocol="HTTP/1.1"
    SSLEnabled="true"
    scheme="https"
    secure="true"
    keystoreFile="/usr/local/cert/213969248020359.pfx"
    keystoreType="PKCS12"
    keystorePass="证书密码"
    clientAuth="false"
    ciphers="TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256"
    SSLProtocol="TLSv1+TLSv1.1+TLSv1.2"
    SSLCipherSuite="ECDHE-RSA-AES128-GCM-SHA256:ECDHE:ECDH:AES:HIGH:!NULL:!aNULL:!MD5:!ADH:!RC4"/>
    
    
将证书导入到服务器上，放到/usr/local/cert目录下，路径名跟证书实际存放目录一致即可，然后填上证书的密码

# Ngnix证书的安装
以下属性中ssl开头的属性与证书配置有直接关系，其它属性请结合自己的实际情况复制或调整
    server {
      listen 443;
      server_name localhost;
      ssl on;
      root html;
      index index.html index.htm;
      ssl_certificate   cert/213969248020359.pem;
      ssl_certificate_key  cert/213969248020359.key;
      ssl_session_timeout 5m;
      ssl_ciphers ECDHE-RSA-AES128-GCM-SHA256:ECDHE:ECDH:AES:HIGH:!NULL:!aNULL:!MD5:!ADH:!RC4;
      ssl_protocols TLSv1 TLSv1.1 TLSv1.2;
      ssl_prefer_server_ciphers on;
      location / {
          root html;
          index index.html index.htm;
      }
    }
    
    
重启ngnix,https默认端口443
