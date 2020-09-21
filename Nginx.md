# Install Nginx on new server (SUSE 12)

1. `sudo zypper addrepo -G -t yum -c 'http://nginx.org/packages/sles/12' nginx`
1. `wget http://nginx.org/keys/nginx_signing.key`
1. `sudo rpm --import nginx_signing.key`
1. `sudo zypper install nginx`
1. `sudo systemctl enable nginx`
1. Set your Nginx configurations:
    * Do not modify /etc/nginx/nginx.conf
    * Put the application upstream declaration in a file at /etc/nginx/conf.d/applications.conf
    * Put your HTTP proxy declaration in /etc/nginx/conf.d/http.conf
    * Put your SSL Configuration in /etc/nginx/conf.d/ssl.conf

1. `sudo systemctl start nginx`
1. `sudo yast firewall`
1. Use down arrow to select `Allowed Services` and press enter
1. Use tab to select `Advanced` and press enter
1. Use tab to highlight the entry under `TCP Ports` and type `80 443` to allow incoming http connections
1. Use tab to select `OK` and press enter
1. Use tab to select `Next` and press enter
1. Press enter on the `Finish` button

# Making changes to Nginx config files

If you make any changes to `nginx.conf` or `conf.d/*.conf`

1. `sudo nginx -t` to make sure your changes do not break nginx
1. `sudo systemctl reload nginx && sudo systemctl restart nginx` to apply your change