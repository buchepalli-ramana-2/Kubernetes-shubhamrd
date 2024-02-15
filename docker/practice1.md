
## Practice: Hosting a Website with Apache HTTP Server Container

**Objective:**
To provide hands-on experience with Docker, hosting a website using the Apache HTTP Server container, modifying the website content inside the container, and utilizing port forwarding.

### Practice Steps:

**Step 1: Pull Apache HTTP Server Container**

```bash
docker pull httpd:latest
```

**Step 2: Run Apache HTTP Server Container**

```bash
docker run -d -p 8080:80 --name my-apache-container httpd:latest
```

This command runs the Apache HTTP Server container in detached mode (-d), maps host port 8080 to container port 80 (-p 8080:80), and assigns a name to the container (--name my-apache-container).

**Step 3: Verify the Running Container**

```bash
docker ps
```

Ensure the Apache HTTP Server container is running.

**Step 4: Access the Website**

Open a web browser and navigate to [http://localhost:8080](http://localhost:8080) to see the default Apache welcome page.

**Step 5: Get Inside the Container**

```bash
docker exec -it my-apache-container /bin/bash
```

Access the container's shell interactively (-it).

**Step 6: Change Index.html Content**

```bash
echo "<h1>Welcome to My Dockerized Website</h1>" > /usr/local/apache2/htdocs/index.html
```

Modify the content of the index.html file with a unique message.

**Step 7: Exit the Container**

```bash
exit
```

**Step 8: Refresh the Website**

Visit [http://localhost:8080](http://localhost:8080) in your web browser again to see the updated content.

## Practice Task2:

1. Host a container with image `docker.io/pengbai/docker-supermario` on port 8090.
   
   ```bash
   docker run -d -p 8090:80 --name supermario-container docker.io/pengbai/docker-supermario
   ```

2. Verify the running container.

   ```bash
   docker ps
   ```

**Stop and Remove Both Containers:**

```bash
docker stop my-apache-container supermario-container
docker rm my-apache-container supermario-container
```


