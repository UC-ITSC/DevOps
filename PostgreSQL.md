# Install Postgres on a server using docker

1. [Install Docker](Docker.md)
1. `docker run --name postgres -e POSTGRES_PASSWORD=(Some Password) -e POSTGRES_USER=itsc -e PGDATA=/var/lib/postgresql/data/pgdata -v pg:/var/lib/postgresql/data -p 5432:5432 --restart=always -d postgres`

# Install Postgres on a server using docker with SSL

_Certificate must be a .pem or .crt file_

1. Create postgres user group `sudo groupadd -g 999 postgres`
1. Add itsc to the postgres group `sudo usermod -a -G postgres itsc`
1. Make sure the SSL certificate .key and .crt/.pem files are owned by user root, group postgres, and have the right permissions
    * `sudo chown root (Path to SSL Key)`
    * `sudo chown root (Path to SSL Cert)`
    * `sudo chgrp postgres (Path to SSL Key)`
    * `sudo chgrp postgres (Path to SSL Cert)`
    * `sudo chmod 640 (Path to SSL Key)`
    * `sudo chmod 644 (Path to SSL Cert)`
1. [Install Docker](Docker.md)
1. Run the docker containter with SSL enabled
    * `docker run --name postgres -e POSTGRES_PASSWORD=(Some Password) -e POSTGRES_USER=itsc -e PGDATA=/var/lib/postgresql/data/pgdata -v pg:/var/lib/postgresql/data -v (Path to SSL Cert):/var/lib/postgresql/server.crt:ro -v (Path to SSL Key):/var/lib/postgresql/server.key:ro -p 5432:5432 --restart=always -d postgres -c ssl=on -c ssl_cert_file=/var/lib/postgresql/server.crt -c ssl_key_file=/var/lib/postgresql/server.key`
