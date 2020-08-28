# Install Nginx on new server (SUSE 12)

1. `sudo zypper addrepo -G -t yum -c 'http://nginx.org/packages/sles/12' nginx`
1. `wget http://nginx.org/keys/nginx_signing.key`
1. `sudo rpm --import nginx_signing.key`
1. `sudo zypper install nginx`
1. `sudo systemctl enable nginx`
1. Set your Nginx configurations:
    * `cd /etc/nginx/conf.d`
    * create `http.conf` with:

    ```conf
    server {
      listen 80;
      server_name (server name).cech.uc.edu;

      return 301 https://$server_name$request_uri;
    }
    ```

    * create `ssl.conf`:

    ```conf
    server {
      listen 443 ssl;
      server_name (server name).cech.uc.edu;

      ssl_certificate      /etc/nginx/certs/(cert name).cer;
      ssl_certificate_key  /etc/nginx/certs/(cert name).key;

      ssl_session_cache    shared:SSL:1m;
      ssl_session_timeout  5m;

      ssl_ciphers  HIGH:!aNULL:!MD5;
      ssl_prefer_server_ciphers  on;

      ssl_protocols TLSv1.1 TLSv1.2;

      client_max_body_size 50M;

      location / {
        proxy_pass  http://(app name);
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection 'upgrade';
        proxy_set_header Host $host;
        proxy_cache_bypass $http_upgrade;
      }
    }
    ```

    * create `applications.conf` with:

    ```conf
    upstream (app name) {
      server 127.0.0.1:(port);
    }
    ```

1. `sudo systemctl start nginx`
1. `sudo yast firewall`
1. Use down arrow to select `Allowed Services` and press enter
1. Use tab to select `Advanced` and press enter
1. Use tab to highlight the entry under `TCP Ports` and type `80 443` to allow incoming http connections
1. Use tab to select `OK` and press enter
1. Use tab to select `Next` and press enter
1. Press enter on the `Finish` button

# Update Nginx on existing server (SUSE 12)

1. `sudo zypper refresh`
1. `sudo zypper up nginx`
    * If you get a warning ending in `NOKEY`
    1. `wget http://nginx.org/keys/nginx_signing.key`
    1. `sudo rpm --import nginx_signing.key`
1. `sudo nginx -t`
    * If it says the config file passed the tests, you are done. otherwise you need to fix the config files

# Making changes to Nginx config files

If you make any changes to `nginx.conf` or `conf.d/*.conf`

1. `sudo nginx -t` to make sure your changes do not break nginx
1. `sudo systemctl reload nginx && sudo systemctl restart nginx` to apply your changes
