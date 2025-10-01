## Deploy Applications with Kubernetes Deployments

On this demo, we will deploy an ```httpd``` application named httpd to deploy the application ```httpd``` using the image ```httpd:latest``` (ensure to specify the tag) using kubernetes deployments. To know more about Deployments and pods, you can visit this [link](https://github.com/AdrianM756/Kubernetes_Documentation/blob/main/Pods_vs_Deployments.md) for a more info.

We will use the ```kubectl``` command to instruct the Kubernetes cluster to create a new deployment.

```
kubectl create deployment httpd --image=httpd:latest
```
<br>

*Explaination:*
<br>

| **Command**                          | **Description**                                               |
|-------------------------------------|---------------------------------------------------------------|
| `kubectl create deployment httpd`   | Creates a Deployment named `httpd`.                          |
| `--image=httpd:latest`              | Pulls the latest version of the httpd container image.       |
<br>

To verify the creation we can use the command ```kubectl get deployment```. You you should be able to get a similar result.

```
NAME    READY   UP-TO-DATE   AVAILABLE   AGE
httpd   0/1     1            0           6s
```
<br>

*Explaination:*

| **Status**      | **Value** | **Meaning**                                           |
|-----------------|-----------|-------------------------------------------------------|
| `READY`         | `1/1`     | One Pod is running and ready to serve traffic.        |
| `UP-TO-DATE`    | `1`       | The current state matches the desired configuration.  |
| `AVAILABLE`     | `1`       | The Pod is accessible and serving requests.           |
<br>

We can also verify the Kubernetes cluster nodes to ensure the control plane was operational using the ```kubectl get nodes``` command.

```
NAME                      STATUS   ROLES           AGE   VERSION
control-plane   Ready    control-plane   25m   v1.27.16-1+f5da3b717fc217
```
<br>


