## Creating a Pod with Resource Limits

For this demo, we will create a pod named ```httpd-pod``` with a container named ```httpd-container``` that has specific resource requests and limits for CPU and memory.
<br>

## Create a Pod configuration file

First, we need to create a ```yaml``` file that defines the pod's specification, including its resource constraints. We can use a text editor like ```vi``` or ```nano``` to create a file named ```pod-resource-limits.yaml```.

*Requirements:*
<br>

* Requests: Memory: ```15Mi```, CPU: ```100m```
* Limits: Memory: ```20Mi```, CPU: ```100m```
<br>

This should the the content of the ```yaml``` file:

```
apiVersion: v1
kind: Pod
metadata:
  name: httpd-pod
spec:
  containers:
  - name: httpd-container
    image: httpd:latest
    resources:
      requests:
        memory: "15Mi"
        cpu: "100m"
      limits:
        memory: "20Mi"
        cpu: "100m"
```
<br>

*Explaination:*

* Your app needs at least ```100 millicores``` of CPU and ```15Mi``` of memory.
* It can’t use more than  ```100 millicores``` of CPU and ```20Mi``` of memory.

For more detail about requests and limits, you ca visit this [link](https://github.com/AdrianM756/Kubernetes_Documentation/blob/main/Request_vs_Limit.md) for more details.
<br>

Next, we will then use the ```kubectl apply``` command to apply the ```yaml``` file to your Kubernetes cluster.

```
kubectl apply -f pod-resource-limits.yaml
```
<br>

We can then verify it's creation using the ```kubectl get pods```. We should be able to get a similar output:

```
NAME        READY   STATUS    RESTARTS   AGE
httpd-pod   1/1     Running   0          85s
```
<br>

The output shows that the pod's ```status``` is ```Running``` and the ```READY``` state is ```1/1```, indicating that its container is ready and operational.
<br>






