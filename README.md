# ppk8srecipe
## 2. Configuring Kubertenes Cluster
### Installation of Kubernetes Cluster
```
kubeadm init --pod-network-cidr=10.4.0.0/16
```
### Verification of Kubernetes Services
```
kubectl cluster-info
kubectl cluster-info dump
```
### Cluster Communication Details
```
--kubelet-certificate-authority
```
## 3. KUbernetes Administration
### Deployments, Rolling Updates and Rollbacks
handson
```
apiVersion:
kind:
metadata:
  name:
spec:
  selector:
    matchLabels:
      app:
  replicas: 2
  template:
    metadata:
      labels:
        app:
    spec:
      containers:
      - name: nginx
        image: nginx:1.7.9
        ports:
        - containerPort: 80
```
