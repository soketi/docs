# Nginx Configuration

Serving soketi behind a web server such as Nginx can allow you to access the soketi server via a specific hostname, such as `socket.example.com`. If you wish, you may also choose to allow Nginx to negotiate your SSL connections instead of providing your SSL certificate information to soketi.

An example Nginx configuration is provided below; however, small adjustments may be required or desired for your specific server environment:

```nginx
server {
    listen 6002 ssl http2;
    listen [::]:6002 ssl http2;
    server_name socket.example.com;
    server_tokens off;
    root /home/forge/default/public;

    # FORGE SSL (DO NOT REMOVE!)
    ssl_certificate /path/to/ssl/certificate.crt;
    ssl_certificate_key /path/to/ssl/key.key;

    ssl_protocols TLSv1.2 TLSv1.3;
    ssl_ciphers TLS13-AES-256-GCM-SHA384:TLS13-CHACHA20-POLY1305-SHA256:TLS_AES_256_GCM_SHA384:TLS-AES-256-GCM-SHA384:TLS_CHACHA20_POLY1305_SHA256:TLS-CHACHA20-POLY1305-SHA256:ECDHE-ECDSA-AES256-GCM-SHA384:ECDHE-ECDSA-CHACHA20-POLY1305:ECDHE-ECDSA-AES256-SHA384:ECDHE-RSA-AES256-GCM-SHA384:ECDHE-RSA-CHACHA20-POLY1305:ECDHE-RSA-AES256-SHA384:ECDHE-ECDSA-AES256-SHA:ECDHE-RSA-AES256-SHA;
    ssl_prefer_server_ciphers on;
    ssl_dhparam /etc/nginx/dhparams.pem;

    add_header X-Frame-Options "SAMEORIGIN";
    add_header X-XSS-Protection "1; mode=block";
    add_header X-Content-Type-Options "nosniff";

    index index.html index.htm index.php;

    charset utf-8;

    location / {
        proxy_pass             http://127.0.0.1:6001;
        proxy_read_timeout     60;
        proxy_connect_timeout  60;
        proxy_redirect         off;

        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection 'upgrade';
        proxy_set_header Host $host;
        proxy_cache_bypass $http_upgrade;
    }

    access_log off;
    error_log  /var/log/nginx/socket.example.com.log error;
}
```
