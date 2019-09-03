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
  name: nginx-dep   # //kubectl get deployments `name`
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
```
kubectl create -f nginx-dep.yaml
kubectl get deployments
```

```
kubectl describe deployment nginx-dep
```

##### 5:11
```
kubectl set image deployment/nginx-dep nginx=nginx:1.8
```
```
kubectl rollout status deployment/nginx-dep
kubectl rollout history deployment/nginx-dep --revision=3
kubectl rollout undo deployment/nginx-dep --to-revision=2
```

### Service Networking
```
kubectl expose deployment nginx-dep --type="NodePort" --port 80
kubectl get service
```

### Ingress
```
kubectl expose pod web-01 --type="ClusterIP" --port 80
```
