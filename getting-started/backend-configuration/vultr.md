# Vultr

This is a basic summary of the steps required to create a production ready server using [Vultr](https://www.vultr.com/?ref=9032189-8H).

There are many ways to create a server, but this is intended to be an example beginners can use to create their first server with no experience required.

## Create Vultr Account and Create Server

Using the link above, create a Vultr account and select products to create your first server.

The Cloud Compute option running Debian 11 with 25GB NVMe is sufficient for 500 connections with high traffic and will cost around $6.00 USD.

Adjust your selection based on your needs.

## Install Docker and Docker Compose

After deploying the server, ssh into the server using the following:

```bash
ssh root@IP_ADDRESS_OF_YOUR_SERVER
```
You will be asked for the password found on your server dashboard.

From the terminal, you can install Docker using [this guide from Vultr](https://www.vultr.com/docs/how-to-install-docker-ce-on-debian-11/).

Once docker is installed and working, install Docker Compose to simplify the start up process.

```bash
sudo apt install -y python3 python3-pip

sudo pip3 install docker-compose

docker-compose -v
```

If it is set up correctly, you will see the version listed in the terminal.

## Create `docker-compose.yml` and Start the Soketi Docker Image

```bash
touch docker-compose.yml

vim docker-compose.yml
```
This will create a `docker-compose` file that will be used to setup Socketi and adjust environment variables and open it in vim within the terminal.

The following is an example of the `docker-compose` file:

```yml
# Set the version of docker compose to use
version: '3.9'

# The containers that compose the project
services:
  soketi:
    container_name: "soketi_server"
    restart: unless-stopped
    image: "quay.io/soketi/soketi:1.0-16-distroless"
    ports:
      - "6001:6001"
      - "9601:9601"
    environment:
      DEBUG: 1
      SOKETI_DEFAULT_APP_ID: app-id
      SOKETI_DEFAULT_APP_KEY: app-key
      SOKETI_DEFAULT_APP_SECRET: app-secret
    networks:
      - soketi_network
```
To save and exit vim, press `:wq`

To start Soketi run:

```bash
docker-compose up -d
```
After installing Soketi, it will start the server.

You can verify that it is running with:

```bash
docker container ls
```

## Nginx Setup

This step is not required and there are many ways to accomplish the same thing, but this approach is beginner friendly(ish). This will make the SSL and domain assignment process easier.

```bash
sudo apt update

sudo apt install nginx

sudo systemctl start nginx.service

sudo systemctl status nginx.service 
```
The above commands will install and then start Nginx for you. The status should be `active` when this process is complete.

Next, we need to direct the default HTTP Port (80) to our Soketi port.

```bash
cd /etc/nginx/sites-available/

vim default
```
This will open the default Nginx config file to edit.

Replace the `location /` section with the following and add the `server_name` section:

```
server {
  ...
  server_name soketi.your-domain.com

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
}
```
:wq to save and exit.

Use whatever domain / subdomain you want to.

Next, restart nginx with the new config:

```bash
sudo systemctl restart nginx.service
```

You will now need to add an `A Record` to your DNS records pointing to the Vultr IP Address for your server.

When that is complete, you should be able to access the Soketi server directly from your chosen domain without needing to access port 6001, but the connection will be unsecure.

You should see a blank screen with `OK` when you visit that url.

## SSL Setup

Again, there are many ways to do this, but this approach is one that works.

We will create an SSL for your domain using `let's encrypt`.

```bash
sudo apt-get install certbot
```
Now we will create the SSL:
```bash
certbot --nginx
```
You will be asked for your email and other simple questions you can answer.

Before the process completes, it will ask you to confirm the domain names you are securing and it should display the `server_name` you selected above.

Your domain should now be secure with a free SSL certificate.

###

Automatic SSL Renewal

The SSL will only last 3 months, but can be renewed. You can setup a cron job to handle that for you.

```bash 
sudo crontab -e
```
Add the following to the file that is opened for you:

```
0 6 * * 0 certbot renew -n -q --post-hook "systemctl reload nginx"
```

This will ask certbot to attempt to renew the SSL every Sunday at 6am. The day and time is not important, but this will ensure it is checked within the renewal window at some point.

## Connect Your Pusher SDKs to the new Server

The following are javascript client creation objects that work with the new, secure setup.

```typescript
// FRONTEND CLIENT

import Pusher from "pusher-js";

export const pusher = new Pusher("app-key", {
  cluster: "",
  wsHost: "soketi.your-domain.com",
  httpHost: "soketi.your-domain.com",
  wsPort: 80,
  wssPort: 443,
  forceTLS: true,
  disableStats: true,
  enabledTransports: ["ws", "wss"],
});
```

```typescript
// BACKEND
export const pusher = new Pusher({
  appId: "app-id",
  key: "app-key",
  secret: "app-secret",
  cluster: "",
  useTLS: true,
  host: "soketi.your-domain.com",
  port: 443
});
```
Be sure to adjust the id, key, and secret to the values you selected in the `docker-compose.yml`.
