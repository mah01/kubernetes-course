# A. Container basics

## exercise 01: Verify Docker setup

1. Login to the machine  
   * or open a terminal if using your own computer
2. Run:
   * `docker run hello-world`
3. Verify that you get a `Hello from Docker!` message


## exercise 02: Run a web server

1. Find an Apache HTTP server image on Docker Hub  
   * Hint: search for `httpd`
2. Run the container and expose it on port `9000`
   * `docker run -p 9000:80 httpd`
3. Verify that the application is accessible
   * `curl localhost:9000`


## exercise 03: Explore running containers

1. List running containers
   * `docker ps`
2. Inspect logs of your container
   * `docker logs <container_id>`
3. Stop the container
   * `docker stop <container_id>`


## exercise 04: Explore container configuration

1. Find a MySQL image on Docker Hub
2. Run the container (you will need environment variables)
   * `-e MYSQL_ROOT_PASSWORD=testhest`
3. Try to inspect the configuration file
   * `/etc/mysql/my.cnf`
4. Use
   * `docker exec -it <container_id> /bin/sh`
5. Print the file contents
