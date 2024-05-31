### Implementing Network Policies with Service-Based Communication in Kubernetes

#### Objective
Learn to use Kubernetes Network Policies to control traffic between pods with service-based communication. This guide includes creating three pods (frontend, application, and backend) and configuring network policies to manage their communication.

#### Prerequisites
- Kubernetes cluster with a network plugin supporting Network Policies (e.g., Calico).
- `kubectl` command-line tool installed.

#### Part 1: Create Pods and Services

1. **Create Pods**
   - Create three pods for frontend, application, and backend tiers. Save the following YAML files and apply them:

     `frontend-pod.yaml`:
     ```yaml
     apiVersion: v1
     kind: Pod
     metadata:
       name: frontend
       labels:
         tier: frontend
     spec:
       containers:
       - name: nginx-frontend
         image: nginx
     ```
     `application-pod.yaml`:
     ```yaml
     apiVersion: v1
     kind: Pod
     metadata:
       name: application
       labels:
         tier: application
     spec:
       containers:
       - name: nginx-application
         image: nginx
     ```
     `backend-pod.yaml`:
     ```yaml
     apiVersion: v1
     kind: Pod
     metadata:
       name: backend
       labels:
         tier: backend
     spec:
       containers:
       - name: nginx-backend
         image: nginx
     ```
   - Apply the YAMLs:
     ```bash
     kubectl apply -f frontend-pod.yaml
     kubectl apply -f application-pod.yaml
     kubectl apply -f backend-pod.yaml
     ```

2. **Create Services**
   - Expose each pod with a Service. Save the following YAML files and apply them:

     `frontend-service.yaml`:
     ```yaml
     apiVersion: v1
     kind: Service
     metadata:
       name: frontend
     spec:
       selector:
         tier: frontend
       ports:
       - protocol: TCP
         port: 80
         targetPort: 80
     ```
     `application-service.yaml`:
     ```yaml
     apiVersion: v1
     kind: Service
     metadata:
       name: application
     spec:
       selector:
         tier: application
       ports:
       - protocol: TCP
         port: 80
         targetPort: 80
     ```
     `backend-service.yaml`:
     ```yaml
     apiVersion: v1
     kind: Service
     metadata:
       name: backend
     spec:
       selector:
         tier: backend
       ports:
       - protocol: TCP
         port: 80
         targetPort: 80
     ```
   - Apply the YAMLs:
     ```bash
     kubectl apply -f frontend-service.yaml
     kubectl apply -f application-service.yaml
     kubectl apply -f backend-service.yaml
     ```

#### Part 2: Implement Network Policies

1. **Allow Frontend to Communicate with Application**
   - Create and apply a Network Policy allowing traffic from the frontend to the application:
     ```yaml
     apiVersion: networking.k8s.io/v1
     kind: NetworkPolicy
     metadata:
       name: allow-frontend-to-application
     spec:
       podSelector:
         matchLabels:
           tier: application
       ingress:
       - from:
         - podSelector:
             matchLabels:
               tier: frontend
     ```
   
2. **Allow Application to Communicate with Backend**
   - Similarly, create and apply a Network Policy for traffic from the application to the backend.

#### Part 3: Testing the Network Policies

1. **Test Connectivity**
   - Test connectivity from the frontend to the application, and from the application to the backend, using the service names:
     ```bash
     kubectl exec frontend -- wget -qO- http://application
     kubectl exec application -- wget -qO- http://backend
     ```
   - Direct connectivity from frontend to backend should be blocked by the network policies.

#### Part 4: Cleanup

1. **Delete Resources**
   - Clean up the created resources:
     ```bash
     kubectl delete -f frontend-pod.yaml
     kubectl delete -f application-pod.yaml
     kubectl delete -f backend-pod.yaml
     kubectl delete -f frontend-service.yaml
     kubectl delete -f application-service.yaml
     kubectl delete -f backend-service.yaml
     kubectl delete networkpolicy allow-frontend-to-application
     kubectl delete networkpolicy allow-application-to-backend
     ```

### Conclusion
This guide provides a hands-on approach to understanding and implementing Kubernetes Network Policies using service-based communication. By setting up these policies and services, you can effectively manage and secure traffic flow within your Kubernetes cluster, ensuring that pods communicate only as intended.
