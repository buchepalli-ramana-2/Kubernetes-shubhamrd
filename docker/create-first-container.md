

## Creating a CentOS Container

1. **Pull a Base Image:**

   Choose a base image from Docker Hub.

   ```bash
   docker pull centos
   ```


2. **Run a Container:**

   Start a basic container without specifying a command.

   ```bash
   docker run -it centos
   ```

3. **Explore the Container:**

   Once inside the container, you can explore its filesystem or execute commands.

   ```bash
   ls
   cat /etc/os-release
   ```

4. **Exit the Container:**

   To exit the container, type `exit`.

   ```bash
   exit
   ```

5. **View Exited Containers:**

   Check the list of all containers, including the exited ones.

   ```bash
   docker ps 
   docker ps -a
   ```

   Copy container id.

6. **Start the stopped container:**

   ```bash
   docker start container-id
   docker ps
   ```

7. **Connect to the container:**

   ```bash
   docker exec -it container-id bash
   exit
   ```

6. **Remove Containers:**

   Remove the container.

   ```bash
   docker stop container-id
   docker rm container-id
   ```

## Creating a Ubuntu Container

1. **Pull a Base Image:**

   Choose a base image from Docker Hub.

   ```bash
   docker pull ubuntu
   ```

2. **Run a Container:**

   Start a basic container without specifying a command.

   ```bash
   docker run -itd --name ubuntu-container ubuntu
   docker exec -it ubuntu-container bash
   ```

3. **Explore the Container:**

   Once inside the container, you can explore its filesystem or execute commands.

   ```bash
   ls
   cat /etc/os-release
   ```

4. **Exit the Container:**

   To exit the container, type `exit`.

   ```bash
   exit
   ```

5. **View Exited Containers:**

   Check the list of all containers, including the exited ones.

   ```bash
   docker ps
   ```

6. **Stop and remove the container:**

   ```bash
   docker stop container-id
   docker rm container-id
   ```


