### Practice Guide: Using Horizontal Pod Autoscaler in Kubernetes

#### Objective
Learn how to implement the Horizontal Pod Autoscaler (HPA) in Kubernetes to automatically scale the number of pods in a deployment based on observed CPU utilization or other select metrics.

#### Prerequisites
- A running Kubernetes cluster (like Minikube).
- `kubectl` command-line tool installed.
- Basic understanding of Kubernetes deployments and metrics.

#### Part 1: Set Up a Sample Application

1. **Create a Deployment**
   - Deploy a sample application (e.g., NGINX) that you will later scale using HPA. Save the following as `nginx-deployment.yaml`:
     ```yaml
     apiVersion: apps/v1
     kind: Deployment
     metadata:
       name: nginx-deployment
     spec:
       replicas: 1
       selector:
         matchLabels:
           app: nginx
       template:
         metadata:
           labels:
             app: nginx
         spec:
           containers:
           - name: nginx
             image: nginx
             ports:
             - containerPort: 80
             resources:
               requests:
                 cpu: 100m
               limits:
                 cpu: 200m
     ```
   - Create the deployment:
     ```bash
     kubectl apply -f nginx-deployment.yaml
     ```

2. **Expose the Deployment**
   - Expose the NGINX deployment as a service:
     ```bash
     kubectl expose deployment nginx-deployment --port=80 --type=NodePort
     ```

#### Part 2: Install Metrics Server

HPA requires metrics from the Metrics Server in your Kubernetes cluster.

1. **Install Metrics Server**
   - Apply the Metrics Server using the YAML from the Kubernetes GitHub repository:
     ```bash
     kubectl apply -f https://github.com/kubernetes-sigs/metrics-server/releases/latest/download/components.yaml
     ```

2. **Verify Metrics Server Installation**
   - Ensure the Metrics Server is running:
     ```bash
     kubectl get deployment metrics-server -n kube-system
     ```

#### Part 3: Create Horizontal Pod Autoscaler

1. **Create HPA Resource**
   - Create an HPA resource that targets your NGINX deployment. Save the following as `nginx-hpa.yaml`:
     ```yaml
     apiVersion: autoscaling/v1
     kind: HorizontalPodAutoscaler
     metadata:
       name: nginx-hpa
     spec:
       scaleTargetRef:
         apiVersion: apps/v1
         kind: Deployment
         name: nginx-deployment
       minReplicas: 1
       maxReplicas: 3
       targetCPUUtilizationPercentage: 50
     ```
   - Apply the HPA resource:
     ```bash
     kubectl apply -f nginx-hpa.yaml
     ```

2. **Verify HPA Creation**
   - Check the HPA status:
     ```bash
     kubectl get hpa
     ```

#### Part 4: Testing the Autoscaler

1. **Simulate Load**
   - Generate load to trigger the scaling. One way to do this is to run a busy loop in one of the pods:
     ```bash
     kubectl run -i --tty load-generator --image=busybox /bin/sh
     ```
   - Then run: `while true; do wget -q -O- http://nginx-deployment; done`

2. **Observe Scaling**
   - Monitor the HPA and the number of pods, and observe how Kubernetes scales the deployment:
     ```bash
     kubectl get hpa nginx-hpa -w
     kubectl get deployment nginx-deployment
     ```

#### Part 5: Cleanup

1. **Remove Load Generator, HPA, and Deployment**
   - Clean up all resources to conclude the practice:
     ```bash
     kubectl delete -f nginx-hpa.yaml
     kubectl delete svc nginx-deployment
     kubectl delete -f nginx-deployment.yaml
     kubectl delete pod load-generator
     ```

### Conclusion

The Horizontal Pod Autoscaler in Kubernetes allows you to automatically scale the number of pods in a deployment or replicaset based on observed CPU utilization or other select metrics. This practice guide offers a hands-on approach to understanding and implementing basic autoscaling features in Kubernetes.