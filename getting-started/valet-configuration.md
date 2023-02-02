# Valet Usage with Nginx Proxy Pass

In order to make your [Docker method](../getting-started/installation/docker.md) work with [Laravel Valet](https://laravel.com/docs/valet), there are some pretty simple steps to take.

{% hint style="info" %}
These instructions will assume you are using the `soketi.test` domain for your application.

These instructions will asume your **sites** directory is located at `~/Sites`.

These instructions will asume your docker port is the default suggested which is **6001**.

You can just change the `soketi` term to what your domain us using, and the `test` term to what your valet TLD is using.
{% endhint %}

### Create & Secure a subdomain

Navigate to the root of your projects and create a new directory named `sockets.soketi.test`. This will be the directory that Valet will use to secure the application and setup the configuration for it.

```shell
# Create the subdomain folder in your Sites folder
mkdir -p ~/Sites/sockets.soketi.test
```

```shell
# CD into the newly created folder
cd ~/.config/valet/Sites/sockets.soketi.test

# Run the secure command to create the configuration & SSL certificates
valet secure
```

### Change the generated configuration file

Open in a preferred editor the configuration file `~.config/valet/Nginx/sockets.soketi.test` and locate the `location /` block that should look like the following:

```nginx
# ... 

    location / {
        rewrite ^ "/Users/your-username/.composer/vendor/laravel/valet/server.php" last;
    }
    
# ...
```

Replace that with the following block:

```nginx
# ...

    location / {
        proxy_pass      http://127.0.0.1:6001;
        proxy_set_header    Host             $host;
        proxy_set_header    X-Real-IP        $remote_addr;
        proxy_set_header    X-Forwarded-For  $proxy_add_x_forwarded_for;
        proxy_set_header    X-Client-Verify  SUCCESS;
        proxy_set_header    X-Client-DN      $ssl_client_s_dn;
        proxy_set_header    X-SSL-Subject    $ssl_client_s_dn;
        proxy_set_header    X-SSL-Issuer     $ssl_client_i_dn;
        proxy_read_timeout 1800;
        proxy_connect_timeout 1800;
        chunked_transfer_encoding on;
        proxy_set_header X-NginX-Proxy true;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection "upgrade";
        proxy_http_version 1.1;
        proxy_redirect off;
        proxy_buffering off;
    }
    
# ...
```

{% hint style="info" %}
Of course, you can make any tweaks to it if you need it.
{% endhint %}

### Restart your valet
```shell
valet restart
```

{% hint style="info" %}
Your newly created subdomain is now ready to be used with the the host `sockets.soketi.test`.
{% endhint %}
