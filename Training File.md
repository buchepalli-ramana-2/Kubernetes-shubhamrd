**Client: Mass Mutual** 

**Subject: Docker & Kubernetes**

**Play wit kubernetes: [https://labs.play-with-k8s.com/](https://labs.play-with-k8s.com/)**

**\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_**

**Lab setup:**

Open vmware on windows lab.

Start node1

Login to node 1 with username root and password root

Check ip with commanmd “ip ad”

Note the ip starting with 192.169.174.x

Minimize vmware and open the git bash installed on lab.

Run command to connect to vmware.

ssh root@192.169.174.x

(replace x with ip addresses)

Password \- root

 

 

**Run Hello World Container**

docker run hello-world

Practice: Create Containers

Create a centos container

1\. Pull a Base Image:

Choose a base image from Docker Hub.

**docker pull centos:centos7**

 

2\. Run a Container:

Start a basic container without specifying a command.

**docker run \-it centos:centos7**

 

3\. Explore the Container:

Once inside the container, you can explore its filesystem or execute commands.

**ls**

**cat /etc/os-release**

 

4\. Exit the Container:

To exit the container, type exit.

**exit**

 

5\. View Exited Containers:

Check the list of all containers, including the exited ones.

**docker ps**

**docker ps \-a**

Copy container id

 

6\. Start the stopped container

**docker start container-id**

**docker ps**

 

7\. Connect to the container

**docker exec \-it container-id bash**

**exit**

 

6\. Remove Containers

Remove the container.

**docker stop container-id**

**docker rm container-id**

 

 

Create a ubuntu container container.

1\. Pull a Base Image:

Choose a base image from Docker Hub.

**docker pull ubuntu**

 

2\. Run a Container:

Start a basic container without specifying a command.

**docker run \-itd \--name ubuntu-container ubuntu**

**docker exec \-it ubuntu-container bash**

 

3\. Explore the Container:

Once inside the container, you can explore its filesystem or execute commands.

**ls**

**cat /etc/os-release**

 

4\. Exit the Container:

To exit the container, type exit.

**exit**

 

5\. View Exited Containers:

Check the list of all containers, including the exited ones.

 

**docker ps**

6\. stop and remove the container.

**docker stop container-id**

**docker rm container-id**

**Practice: Hosting a Website with Apache HTTP Server Container**

Objective:

To provide hands-on experience with Docker, hosting a website using the Apache HTTP Server container, modifying the website content inside the container, and utilizing port forwarding.

 

Practice Steps:

Step 1: Pull Apache HTTP Server Container

docker pull httpd:latest

 

Step 2: Run Apache HTTP Server Container

docker run \-d \-p 8080:80 \--name my-apache-container httpd:latest

This command runs the Apache HTTP Server container in detached mode (-d), maps host port 8080 to container port 80 (-p 8080:80), and assigns a name to the container (--name my-apache-container).

 

Step 3: Verify the Running Container

docker ps

Ensure the Apache HTTP Server container is running.

 

Step 4: Access the Website

Open a web browser and navigate to http://node-ip:8080 to see the default Apache welcome page.

 

Step 5: Get Inside the Container

docker exec \-it my-apache-container /bin/bash

Access the container's shell interactively (-it).

 

Step 6: Change Index.html Content

echo "\<h1\>**Welcome to My Dockerized Website**\</h1\>" \> /usr/local/apache2/htdocs/index.html

Modify the content of the index.html file with a unique message.

 

Step 7: Exit the Container

exit

 

Step 8: Refresh the Website

Visit http://node-ip:8080 in your web browser again to see the updated content.

 

 

**Docker Installation:**

**1\. Remove old docker packages**

 

sudo yum \-y remove docker\*

**This command updates the system to ensure you have the latest packages and dependencies.**

 

**2\. Install Required Dependencies**

sudo yum install \-y yum-utils

**Install necessary packages for Docker.**

 

**3\. Add Docker Repository**

sudo yum-config-manager \--add-repo [https://download.docker.com/linux/centos/docker-ce.repo](https://download.docker.com/linux/centos/docker-ce.repo)

**This adds the Docker repository to your system.**

 

**4\. Install Docker Engine**

sudo yum  install \-y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin

 

**5\. Start and Enable Docker**

sudo systemctl start docker

sudo systemctl enable docker

 sudo systemctl status docker

**Start and enable Docker to ensure it runs on system boot.**

 

 

**7\. Verify Docker Installation**

docker \--version

**Check the installed Docker version to confirm a successful installation.**

 

**Day 2:**

**Challenge:** 

Host supermario game on container

Image: [pengbai/docker-supermario](http://docker.io/pengbai/docker-supermario)

Solution:

 

docker run \--name mario \-d \-p 8090:8080 pengbai/docker-supermario 

Open a browser  with node1-IP:8090

**Practice: Host a MYSQL with env variable**

docker run \--name db2 \-d \-e MYSQL\_ROOT\_PASSWORD=admin1234 \-e MYSQL\_USER=shubham \-e MYSQL\_PASSWORD=shubham1234 \-e MYSQL\_DATABASE=testdb mysql

 

docker ps \-a

docker logs db2

docker exec \-it db2 mysql \-u root \-padmin1234

 

\> create database abc;

\> show databases;

\> exit;

 docker exec \-it db2 mysql \-u shubham \-pshubham1234

\>exit

docker rm \-f db2

**Practice Scenario: Docker Bind Mount with Index.html**

 

In this updated practice, students will work with a Docker bind mount to share an index.html webpage between the host and the container. Sample website data will be used for demonstration.

Practice Overview:

Bind Mount Practice with Index.html:

Scenario: Students will create an Nginx container, bind-mounting a local directory containing an index.html file with sample website data.

 

Step-by-Step Guide:

1\. Bind Mount Practice with Index.html:

Create Web Content Directory:

mkdir /web-content

 

Create Sample /web-content/index.html :

echo “sample application” \>  /web-content/index.html

 

Run Nginx Container with Bind Mount:

docker run \-d \--name nginx-container \-v /web-content:/usr/share/nginx/html \-p 8080:80 nginx:latest

 

Verify Sample Website:

Open http://nodeip:8080 in a web browser.

 

Update Content Locally:

Make changes to web-content/index.html locally.

 echo “new updates” \>\> /web-content/index.html

Verify Updated Content in Container:

Refresh the web browser at http://nodeip:8080 to see the changes reflected.

 

Verify Container Data Locally:

Check the modified web-content/index.html file on the local machine to ensure changes persist.

**Practice Guide: Docker Commit and Push to Docker Hub**

Objective:

Demonstrate the use of the docker commit command to create a new Docker image and push it to Docker Hub.

 

Practice Steps:

Step 1: Sign Up for Docker Hub

Visit Docker Hub and sign up for a new account.

Step 2: Create a Private Repository

Log in to Docker Hub.

In the top navigation, click on "Repositories" and then "Create Repository."

Provide a name for the repository (e.g., my-public-repo) and set it to private. Click "Create."

 

Step 3: Get User Access Keys

In the Docker Hub dashboard, go to "Account Settings" \> Personal Access Tokens → Generate new tokens."

Generate a new access token, providing the necessary permissions. (read-write)

 

Step 4: Connect to Docker Hub

In the terminal, log in to Docker Hub using the Docker CLI.

docker login \-u YOUR\_DOCKER\_HUB\_USERNAME \-p YOUR\_ACCESS\_TOKEN

 

Step 5: Create a Container

Launch a new container from a base image.

docker run \-itd \--name my-container centos:7

 

Step 6: Connect to the Container

docker exec \-it my-container /bin/bash

 

 

Step 7: Make Changes in the Container

Create a sample file using the text editor.

echo “Enter some content and save the file.” \> sample.txt

 

 

Step 8: Commit Changes to a New Image

Exit the container.

exit

 

Use the docker commit command to create a new image.

docker commit my-container YOUR\_DOCKER\_HUB\_USERNAME/reponame:latest

 

Step 9: Push the Image to Docker Hub

Push the newly created image to Docker Hub.

docker push YOUR\_DOCKER\_HUB\_USERNAME/my-custom-image:latest

 

Step 10: Verify on Docker Hub

Stop and remove the currently running container.

Get the new image path, uploaded your repository.

Create container with same image.

Connect to container and check for same file.

**DockerFile** 

**Docker Practice: Build and Run a Custom Image**

**1\. Create a Working Directory**

mkdir custom-app

cd custom-app/

 

**2\. Create and Edit Dockerfile**

nano Dockerfile

**Paste the following content into the Dockerfile:**

FROM ubuntu

WORKDIR /mnt

COPY app.code  .

RUN touch app.config

RUN echo "applition configuration" \> app.config

ADD https://templatemo.com/tm-zip-files-2020/templatemo\_591\_villa\_agency.zip  .

* Press Ctrl \+ X, then Y, and Enter to save and exit the editor.

 

**3\. Verify Dockerfile**

cat Dockerfile

 

**4\. Create a Sample App Code File**

touch app.code

echo "some code" \> app.code

 

**5\. Build the Docker Image**

docker build \-t app2-image:v1 .

 

**6\. List Docker Images**

docker images

 

**7\. Run a Container from the Image**

docker run \-itd \--name app2 app2-image:v1

 

**8\. List Running Containers**

docker ps

 

**9\. Access the Running Container**

docker exec \-it app2 bash

 

**Inside the container, run the following:**

ls

cat app.code

cat app.config

exit

Docker File Practice:

Complete part 1 of [https://docs.docker.com/get-started/workshop/02\_our\_app/](https://docs.docker.com/get-started/workshop/02_our_app/)

Day3

Challenge:

1. deploy mysql  
2. connect and test locally  
3. deploy wordpress and connect with db  
4. Test WP over browser 

deploy mysql

docker run \--name wpdb \-d \-e MYSQL\_ROOT\_PASSWORD=admin1234 \-e MYSQL\_USER=wpuser \-e MYSQL\_PASSWORD=wppassword \-e MYSQL\_DATABASE=wpdb mysql

docker ps

docker logs wpdb

docker exec \-it wpdb mysql \-u wpuser \-pwppassword

\> show databases;

\> exit;

 

docker inspect wpdb

copy db ip address

docker run \--name wp1 \-d \-p 8092:80 \-e WORDPRESS\_DB\_HOST=\<db-ip-address\> \-e WORDPRESS\_DB\_USER=wpuser \-e WORDPRESS\_DB\_PASSWORD=wppassword \-e WORDPRESS\_DB\_NAME=wpdb \-e WORDPRESS\_TABLE\_PREFIX=wp\_ wordpress

docker ps

docker logs wp1

open browser with nodeip and port no 8092 

Kuberntes Setup with kubeadm: [https://github.com/shubhamrd/Kubernetes/tree/main/kubernetes-setup](https://github.com/shubhamrd/Kubernetes/tree/main/kubernetes-setup)

Minikube setup

1. open gitbash, you are automatily logeed o  
2. open vmware and power off node1ut  
3. run command ‘minikube start \--nodes 3’  
4. run command ‘minikube status’ or ‘kubectl get nodes’  
5. open vscode app from desktop and open the terminal

**practice : Managing Pods**

**Create pod**

kubectl run pod1 \--image=nginx

 

**List pods**

kubectl get pods

 kubectl get pods \-o wide

 

**Get pods events**

  kubectl describe pod pod1

 

**Get pods logs**

 kubectl logs pod1

**Get inside pod**

 kubectl exec \-it pod1 bash

\> exit 

**Delete pod**

kubectl delete pod pod1

 

Just for refarance Minikube Setup Document

1\. INstall Minicube

Create a Folder: Create a new folder on your system where you will download all the necessary files. For example, C:\\Minikube.

Download Minikube:

URL: https://github.com/kubernetes/minikube/releases

Download minikube-windows-amd64.exe into your folder. 

2\. Download kubectl: 

URL: https://kubernetes.io/docs/tasks/tools/install-kubectl-windows/

Use curl or direct download to get the executable in the same folder.

3\. Download VMware Driver:

URL: https://github.com/machine-drivers/docker-machine-driver-vmware/releases

Get docker-machine-driver-vmware\_0.1.5\_windows\_amd64.tar.gz and extract it to your folder.

Add Folder to PATH: 

4\. Add C:\\Minikube to your system PATH.

Instructions: Right Click on My Computer \--\> Properties → Advanced → Environment Variables → Path → Edit → New → Add folder path.

Add a path for VMware Workstation installed location : C:\\Program Files (x86)\\VMware\\VMware Workstation 

Verify the path before adding.

5\. Start Minikube:

Open Command Prompt as administrator.

Navigate to your folder: cd C:\\Minikube.

Start Minikube: 

minikube config set driver vmware

minikube start 

Troubleshooting:

If any error regarding 'vmrun' not found occurs, make sure VMware Workstation's path is correctly added to PATH.

Minikube Releases:

https://github.com/kubernetes/minikube/releases

Kubectl Windows Download:

https://kubernetes.io/docs/tasks/tools/install-kubectl-windows/

VMware Driver for Minikube:

https://github.com/machine-drivers/docker-machine-driver-vmware/releases

Create a Single-Node Cluster:

minikube start

Create a Multi-Node Cluster:

minikube start \--nodes 2

Delete the Cluster:

minikube delete

Interact with the Cluster:

Access the Kubernetes Dashboard:

minikube dashboard

Connect to a Specific Node with SSH

minikube node list

minikube ssh    

or 

minkube ssh \-n NodeName

Stop the Cluster:

minikube stop

**Labels**

kubectl get pods \--show-labels

kubectl run pod2 \--image=httpd

kubectl get pods \--show-labels

kubectl label pod pod1 app=webapp

 kubectl label pod pod1 project=projectRed CC=accountRed

kubectl get pods \--show-labels

 kubectl label pod pod2 project=projectble CC=accountblue app=webapp

kubectl get pods \--show-labels

kubectl label pod pod1 \--overwrite run=newpod

kubectl get pods \--show-labels

 kubectl label pod pod2 CC-

 kubectl get pods \--show-labels

kubectl run pod3 \--image=httpd \--dry-run \-o yaml \> pod.yaml

open pod.yml in vscode editor

Do changes like the following

apiVersion: v1

kind: Pod

metadata:

  labels:

	app: webapp

  name: pod3

spec:

  containers:

  \- image: httpd

	name: pod3

 

save the file 

 

kubectl apply \-f pod.yml

 kubectl get pods

kubectl delete \-f pod.yml

**Multi-container**

create a file multi-pod.yml

apiVersion: v1

kind: Pod

metadata:

  labels:

    ownser: shubham1

  name: pod4

spec:

  containers:

  \- image: httpd

    name: web-container

  \- image: ubuntu

    name: load-balancer

    command: \["/bin/bash","-c","while true; do echo hello; sleep 10; done"\]

 

 kubectl apply \-f multi-pod.yml

  kubectl get pods \-w

  kubectl describe pod pod4

  kubectl logs pod4

kubectl logs pod4 \-c load-balancer

 

 kubectl exec \-it pod4 bash

\>exit

 

kubectl exec \-it pod4 bash \-c load-balancer

\>exit

 

kubectl delete \-f multi-pod.yml

Services

kubectl run webapp \--image=nginx \--port=80

kubectl expose pod webapp \--port=80

 kubectl get pods

  kubectl get svc

minikube ssh

 curl \<service-ip\>:80

exit

NodeIP servoie

kubectl delete svc webapp

kubectl expose pod webapp \--port=80 \--type=NodePort

 kubectl get svc

Check external port no. 

 ![][image1]

My case it is 31744

minikube ip

Open browser with minikube ip and port no

Labels and selectors with service

Step 1: Create a Pod with Labels using YAML

Create a YAML file named pod-with-labels.yaml with the following content:

apiVersion: v1

kind: Pod

metadata:

  name: my-nginx

  labels:

    app: my-nginx

    env: production

spec:

  containers:

    \- name: nginx-container

      image: nginx

Apply the YAML file:

kubectl apply \-f pod-with-labels.yaml

Step 2: List Labels for the Pod

List labels for the created pod:

kubectl get pod my-nginx \--show-labels

Step 3: Create a Service with the Same Selectors using YAML

Create service-with-selectors.yaml with the following content:

apiVersion: v1

kind: Service

metadata:

  name: my-nginx-svc

spec:

  selector:

    app: my-nginx

    env: production

  type: NodePort

  ports:

    \- protocol: TCP

      port: 80

      targetPort: 80

      nodePort: 31555

	

Apply the YAML file:

kubectl apply \-f service-with-selectors.yaml

Step 4: Test the Service

kubectl get svc my-nginx-svc

open broser with minikube ip and port

Extend the demos of service:

Step 1: Remove Selectors from Existing Pod

kubectl label pod podname \--overwrite app=webapp

kubectl label pod podname \--overwrite env=test

Step 2: Check Connectivity to the Service (Expect Failure)

\# Access the service internally after removing selectors (Expect failure)

check on browser

**Working with ReplicaSet**

**Create a ReplicaSet (RS)**

 

YAML Definition: Create nginx-rs.yaml with the following content:

apiVersion: apps/v1

kind: ReplicaSet

metadata:

  name: nginx-rs

spec

  replicas: 3

  selector:

    matchLabels:

      app: nginx

  template:

    metadata:

      labels:

        app: nginx

    spec:

      containers:

      \- name: nginx

        image: nginx

 

kubectl apply \-f nginx-rs.yaml

 

Verify the ReplicaSet

 

Command: kubectl get rs

Expectation: nginx-rs should be running with 3 replicas.

 

Scale the ReplicaSet

Scale Up: kubectl scale rs nginx-rs \--replicas=5

Verify: kubectl get rs

Scale Down: kubectl scale rs nginx-rs \--replicas=2

Verify again.

edit the label of any pod under rs and check the reaction.

restore the label to original and again check

 

kubectl get pods \--show-labels

select any pod

kubectl label pod pod-name app=webapp \--overwrite 

kubectl get pods \--show-labels

kubectl label pod pod-name app=nginx 

**Deployment**

Step 1: Create a Deployment

Create a YAML file for the Deployment: Name it nginx-deployment.yaml. This will create a Deployment running an Nginx server.

apiVersion: apps/v1

kind: Deployment

metadata:

  name: nginx-deployment

spec:

  replicas: 5

  selector:

    matchLabels:

      app: nginx

  template:

    metadata:

      labels:

        app: nginx

    spec:

      containers:

      \- name: nginx

        image: nginx:1.17.0

 

 

 

Create the Deployment:

kubectl apply \-f nginx-deployment.yaml

 

 kubectl annotate deployment nginx-deployment kubernetes.io/change-cause="version change1" \--overwrite=true

 

Step 2: Update the Deployment

Update the Deployment to Use a New Version of Nginx:

 

Edit the nginx-deployment.yaml file, changing the image from nginx:1.17.0 to stable-perl

 Apply the yaml file

 

Chck deployment

Kubectl get pods \-w

 kubectl annotate deployment nginx-deployment kubernetes.io/change-cause="upgraded to stable-perl" \--overwrite=true

 

Do the same for image  nginx:1.18.0

 

Step 3: Monitor the Update

Monitor the Status of the Deployment:

kubectl rollout status deployment/nginx-deployment

 

 

Step 5: Rollback if Necessary

Rollback to the Previous Version:

If you need to rollback the update for any reason:

 kubectl rollout history deployment/nginx-deployment

 kubectl get rs \-o wide

Rollback deployment

 

kubectl rollout undo deployment/nginx-deployment

 

or

Kubectl rollout undo –to-revision=2 deployment name \# last version

Day 5:

Using Volumes in Pods

Using an emptyDir Volume

 

Create a Pod with an emptyDir volume to share data between containers:

apiVersion: v1

kind: Pod

metadata:

  name: mypod

spec:

  containers:

    \- name: myfrontend

      image: nginx

      volumeMounts:

        \- name: myvolume

          mountPath: /var/www/html

  volumes:

    \- name: myvolume

      emptyDir: {}

 

Verify :

kubectl get pod

kubectl describe pod mypod

check for volume configuration

 

 

 

 

Using a hostPath Volume

minikube ssh \-n minikube-m02

sudo su \- 

\> mkdir /mnt/data

\> touch /mnt/data/config.txt

\> echo “some text” \> /mnt/data/config.txt

\>exit

\> exit

kubectl lable node minikube-m02 nodetype=worker1

Useful for accessing host filesystem, typically for advanced use cases:

 

apiVersion: v1

kind: Pod

metadata:

  name: app2

spec:

  containers:

    \- image: nginx

      name:  con1

      volumeMounts:

        \- name: testvolume

          mountPath: /mnt/data

  affinity:

    nodeAffinity:

      requiredDuringSchedulingIgnoredDuringExecution:

          nodeSelectorTerms:

            \- matchExpressions:

              \- key: nodetype

                operator: In

                values:

                  \- worker1

  volumes:

    \- name: testvolume

      hostPath:

        path: /mnt/data

        type: Directory

 

Apply the file 

kubectl exec \-it app2 

cd /mnt/data

ls

cat config.txt

exit

[image1]: <data:image/png;base64,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>