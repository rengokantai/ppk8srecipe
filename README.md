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

sample file:
```
apiVersion: v1
kind: Service
meatadata:
  name: ingress-nginx
  namespace: ingress-nginx
  labels:
    app.kubernetes.io/name: ingress-nginx
    app.kubernetes.io/part-of: ingress-nginx
spec:
  type: NodePort
  ports:
  - name: http-new
    port: 80
    targetPort: 80
    protocol: TCP
    nodePort: 30090
selector:
  app.kubernetes.io/name: ingress-nginx
  app.kubernetes.io/part-of: ingress-nginx
```
```
kubectl get service --all-namespaces
```
##### 05:08 ingress
```
kind: Ingress
metadata:
  name: ingress-test
  annotations:
    kubernetes.io/ingress.class: nginx
    ingress.kubernetes.io/rewrite-target: /
spec:
  rules:
  - host: kube-master.labs.local
    http:
      paths:
        path: /
        backend:
          serviceName: web-01
          servicePort: 80
```
```
kubectl get ingress
```
##### 06:43
modify host file. modify
```
192.1.1.2 kube-master.labs.local
```
