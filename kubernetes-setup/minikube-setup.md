# Minikube Installation Guide

This guide provides step-by-step instructions for setting up Minikube on a Windows system, including the necessary tools and configurations.

## 1. Install Minikube

### Create a Folder
Create a new folder on your system where you will download all the necessary files. For example, `C:\Minikube`.

### Download Minikube
Download the Minikube executable for Windows:
- URL: [Minikube Releases](https://github.com/kubernetes/minikube/releases)
- Download `minikube-windows-amd64.exe` into your folder `C:\Minikube`.
- Rename file from `minikube-windows-amd64.exe` to `minikube.exe`

## 2. Download kubectl

Download the `kubectl` executable for Windows:
- URL: [Install kubectl on Windows](https://kubernetes.io/docs/tasks/tools/install-kubectl-windows/)
- Use curl or direct download to get the executable in the same folder.

## 3. Download VMware Driver

Download and extract the VMware driver for Minikube:
- URL: [VMware Driver Releases](https://github.com/machine-drivers/docker-machine-driver-vmware/releases)
- Get `docker-machine-driver-vmware_0.1.5_windows_amd64.tar.gz` and extract it to your folder.

## 4. Add Folder to PATH

Add `C:\Minikube` to your system PATH:
1. Right-click on My Computer.
2. Select Properties.
3. Click on Advanced.
4. Choose Environment Variables.
5. Edit the PATH variable and add a new entry with your folder path.

Also, add the VMware Workstation installed location to your PATH (e.g., `C:\Program Files (x86)\VMware\VMware Workstation`). Verify the path before adding.

## 5. Start Minikube

### Open Command Prompt
Open Command Prompt as an administrator.

### Navigate to Your Folder
```sh
cd C:\Minikube
```

### Configure and Start Minikube
Set the driver to VMware:
```sh
minikube config set driver vmware
```

Start Minikube:
```sh
minikube start
```



________________________________________________________________________________________________________________________

## Minikube Commands and Usage

### Create a Single-Node Cluster
```sh
minikube start
```

### Create a Multi-Node Cluster
```sh
minikube start --nodes 2
```

### Delete the Cluster
```sh
minikube delete
```

### Interact with the Cluster
#### Access the Kubernetes Dashboard
```sh
minikube dashboard
```

#### Connect to a Specific Node with SSH
```sh
minikube node list
minikube ssh
```
or
```sh
minikube ssh -n NodeName
```

### Stop the Cluster
```sh
minikube stop
```
