## Deploy Grafana on Kubernetes
<br>

For this demo, we will Grafana on a Kubernetes. For this, we will be using ```Deployment``` to manage the pods and ```NodePort``` for the service. 
<br>

First, we will need to create a ```yaml``` file for named ```Deployment.yaml``` for our deployment. We will be using the latest image of grafana and expose it to it's default port ```3000```. Copy the following context below:

```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: grafana-deployment-xfusion
  labels:
    app: grafana
spec:
  replicas: 1
  selector:
    matchLabels:
      app: grafana
  template:
    metadata:
      labels:
        app: grafana
    spec:
      containers:
      - name: grafana
        image: grafana/grafana:latest
        ports:
        - containerPort: 3000
```
<br>

Next, we will then need to create a ```yaml``` file named ```grafana-service.yaml``` for our NodePort. To make the Grafana application accessible from outside the Kubernetes cluster, a NodePort Service named ```grafana-service-xfusion``` was created. It specifically exposes the service on NodePort ```32000```, which routes traffic to the target container port ```3000```. Copy the following context below:

```
apiVersion: v1
kind: Service
metadata:
  name: grafana-service-xfusion
spec:
  type: NodePort
  selector:
    app: grafana
  ports:
    - port: 3000
      targetPort: 3000
      nodePort: 32000
      protocol: TCP
```
<br>

To deploy, We will be using the ```kubectl apply``` command:

```
kubectl apply -f Deployment.yaml
```

```
kubectl apply -f grafana-service.yaml
```
<br>






