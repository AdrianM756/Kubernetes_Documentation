## Deploying Nginx Web Server on Kubernetes Cluster
<br>

For this demo, we will create a deployment with a NodePort Service for our ```nginx``` web server.
<br>

Firstm we need to create a deployment using ```nginx``` image with ```latest``` tag only(remember to mention the tag i.e ```nginx:latest```). Name it as ```nginx-deployment```. The container should be named as ```nginx-container```, also make sure replica counts are ```3```. We will then input this to a ```yaml``` file named ```nginx-deployment.yaml```. We should be able to get this output:

```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
spec:
  replicas: 3
  selector:
    matchLabels:
      app: nginx-app
  template:
    metadata:
      labels:
        app: nginx-app
    spec:
      containers:
        - name: nginx-container
          image: nginx:latest
          ports:
            - containerPort: 80
```
<br>

Next, we need to create a ```NodePort``` type service named ```nginx-service```. The nodePort should be ```30011```. We will then input this to a ```yaml``` file named ```nginx-service.yaml```. We should be able to get this output:

```
apiVersion: v1
kind: Service
metadata:
  name: nginx-service
spec:
  type: NodePort
  selector:
    app: nginx-app
  ports:
    - protocol: TCP
      port: 80
      targetPort: 80
      nodePort: 30011
```
<br>

We will then need to use the ```kubectl apply``` command to execute the ```yaml``` file:

```
kubectl apply -f nginx-deployment.yaml
```
```
kubectl apply -f nginx-service.yaml
```
<br>

We can use the following commands to check if it is configured the way that we've set it:

```
kubectl describe deployment nginx-deployment
```

```
kubectl describe service nginx-service
```
<br>








