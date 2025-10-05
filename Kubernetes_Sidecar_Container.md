## Kubernetes Sidecar Container
<br>
A Kubernetes sidecar container is a secondary container that runs alongside the main application container within the same Pod. Sidecar containers are used to extend or enhance the functionality of the primary application without modifying its code. They are helpful for separating concerns and offloading auxiliary tasks.
<br>

*Simple Analogy*
<br>

Think of the main application container as the Driver of a motorcycle, and the sidecar container as the Motorcycle Sidecar attached to it. 

The Driver (main container) is focused solely on the primary task: driving the motorcycle (running the core business logic).

The Sidecar (sidecar container) is a separate, dedicated compartment that travels with the driver to perform essential, supporting jobs without making the driver's job harder. They share the road and destination but handle different responsibilities.
<br>

## Demo
<br>

For this demo, we need to run a web server (nginx) inside a Kubernetes Pod and ship its logs to an aggregation service using the [Sidecar pattern](https://kubernetes.io/docs/concepts/workloads/pods/sidecar-containers/).

* Main Container: nginx-container serves web pages and generates access/error logs.
* Sidecar Container: sidecar-container (Ubuntu) reads the same logs every 30 seconds.
* Shared Storage: An emptyDir volume allows both containers to share log files during the Pod’s lifetime.
<br>

This pattern keeps responsibilities separated. The nginx focuses on serving web content, while the sidecar focuses on log collection.
<br>

First, we need to create a ```yaml``` file named ```webserver.yaml``` with the following contents inside:

```
apiVersion: v1
kind: Pod
metadata:
  name: webserver
spec:
  volumes:
  - name: shared-logs
    emptyDir: {}
  containers:
  - name: nginx-container
    image: nginx:latest
    volumeMounts:
    - name: shared-logs
      mountPath: /var/log/nginx
  - name: sidecar-container
    image: ubuntu:latest
    command: ["sh","-c","while true; do cat /var/log/nginx/access.log /var/log/nginx/error.log; sleep 30; done"]
    volumeMounts:
    - name: shared-logs
      mountPath: /var/log/nginx
```
<br>

Once done, save the file and use the ```kubectl apply``` command to create a pod from this file.

```
kubectl apply -f webserver.yaml
```
<br>

To inspect the pod, we can use the commands:

```
kubectl describe pod webserver
```
<br>

To view the sidecar logs, we can use the command:

```
kubectl logs -f webserver -c sidecar-containerkubectl logs -f webserver -c sidecar-container
```
<br>

*Explaination:*
<br>

| Part | Meaning | Analogy |
| :--- | :--- | :--- |
| **`kubectl logs`** | The base command used to fetch logs from a container. | "Show me the activity report..." |
| **`-f`** (or `--follow`) | This flag tells Kubernetes to **follow** the log output. Logs will be streamed in real-time as they are written by the container. | "...and keep updating it as new things happen." (like `tail -f` in Linux) |
| **`webserver`** | This is the **name of the Pod** you are targeting. Logs will be pulled from a container inside this Pod. | "...for the employee in room `webserver`." |
| **`-c sidecar-container`** | This flag specifies the **container name** within the Pod. You use this when a Pod has multiple containers (like a main app and a sidecar). | "...specifically from the `sidecar-container`'s notebook."
<br>

*Summary:*
The command instructs Kubernetes to **connect to the Pod named `webserver` and continuously stream the real-time output (logs) from the specific container named `sidecar-container`** inside that Pod.

