# Install Redis on a new server (SUSE 12)

1. [Install Docker](Docker.md)
2. `docker run --restart=always --name redis -d -p 6379:6379 redis`

# Dump/Erase Redis Cache

1. `docker exec -it redis redis-cli FLUSHALL`
