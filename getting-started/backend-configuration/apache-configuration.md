# Apache Configuration

Serving soketi behind a web server such as Apache can allow you to access the soketi server via a specific hostname, such as `socket.example.com`. If you wish, you may also choose to allow Apache to negotiate your SSL connections instead of providing your SSL certificate information to soketi.

An example Apache configuration is provided below; however, small adjustments may be required or desired for your specific server environment:

```apache
ServerName socket.example.com
DocumentRoot /path/to/public_html
ErrorLog /path/to/error_log
DirectoryIndex index.html index.htm index.php index.php4 index.php5

SSLEngine on
SSLProxyEngine on
SSLProxyVerify none
SSLProxyCheckPeerCN off
SSLProxyCheckPeerName off
SSLProxyCheckPeerExpire off
SSLCertificateFile /path/to/ssl.combined
SSLCertificateKeyFile /path/to/ssl.key
SSLCACertificateFile /path/to/ssl.ca
SSLProtocol all -SSLv2 -SSLv3 -TLSv1 -TLSv1.1

ProxyPass / ws://127.0.0.1:6001/
ProxyPassReverse / ws://127.0.0.1:6001/
```
