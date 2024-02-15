## Step-by-Step Guide to Install Docker on CentOS

1. **Update System**

    ```bash
    sudo yum update -y
    sudo yum -y remove buildah podman
    ```

    This command updates the system to ensure you have the latest packages and dependencies.

2. **Install Required Dependencies**

    ```bash
    sudo yum install -y yum-utils
    ```

    Install necessary packages for Docker.

3. **Add Docker Repository**

    ```bash
    sudo yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo
    ```

    This adds the Docker repository to your system.

4. **Install Docker Engine**

    ```bash
    sudo yum install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
    ```

    Install Docker Engine using the added repository.

5. **Start and Enable Docker**

    ```bash
    sudo systemctl start docker
    sudo systemctl enable docker
    sudo systemctl enable containerd
    ```

    Start and enable Docker to ensure it runs on system boot.

6. **Add User to Docker Group (Optional)**

    ```bash
    sudo usermod -aG docker $USER
    ```

    Add your user to the docker group to run Docker commands without sudo (logout and login may be required).

7. **Verify Docker Installation**

    ```bash
    docker --version
    ```

    Check the installed Docker version to confirm a successful installation.

    **Note:** Logout from user and login back.

8. **Run Docker Hello World**

    ```bash
    docker run hello-world
    ```

    Execute a simple container to ensure Docker is working correctly.
