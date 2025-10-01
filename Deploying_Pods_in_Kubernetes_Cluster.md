## Deploying Pods in Kubernetes Cluster

For this demo, we will a pod named ```pod-httpd``` using the ```httpd``` image with the ```latest``` tag using the ```kubectl``` commmand. We will then set the ```app``` label to ```httpd_app```, and name the container as ```httpd-container```. To know more about Deployments and pods, you can visit this [link](https://github.com/AdrianM756/Kubernetes_Documentation/blob/main/Pods_vs_Deployments.md) for a more info.

```
kubectl run pod-httpd --image=httpd:latest --labels=app=httpd_app --dry-run=client --output=yaml > pod-httpd.yaml
```
<br>

*Explaination:*
<br>

```--dry-run=client``` - simulates the execution of a ```kubectl``` command without actually applying changes to the cluster.

```--output=yaml > pod-httpd.yaml``` - This controls the format of the output. In this case, it tells ```kubectl``` to return the result in ```YAML``` format and save it to ```pod-httpd.yaml``` file.
<br>

This will be the result:

```
apiVersion: v1
kind: Pod
metadata:
  creationTimestamp: null
  labels:
    app: httpd_app
  name: pod-httpd
spec:
  containers:
  - image: httpd:latest
    name: pod-httpd
    resources: {}
  dnsPolicy: ClusterFirst
  restartPolicy: Always
status: {}
```
<br>

Next, let's edit the ```pod-httpd.yaml``` file. We will need to delete the ```creationTimestamp: null```, ```resources: {}```, ```dnsPolicy: ClusterFirst```, ```restartPolicy: Always```, ```status: {}```  then change the ```name: pod-httpd``` under the ```container:``` to ```name: httpd-container```. Once done, save the file. This will be the final result:

```
apiVersion: v1
kind: Pod
metadata:
  labels:
    app: httpd_app
  name: pod-httpd
spec:
  containers:
  - image: httpd:latest
    name: httpd-container
```
<br>

Next, Let update this file using the following commands:

```
kubectl apply -f pod-httpd.yaml
```
<br>

We will then need to use the ```kubectl get pods``` command to check the list of all the pods. We should be able to get a similar output:

```
NAME        READY   STATUS    RESTARTS   AGE
pod-httpd   1/1     Running   0          2m8s
```
<br>














