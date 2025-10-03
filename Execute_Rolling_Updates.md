## Execute Rolling Updates

For this demo, we will execute a rolling update on an nginx web server to ```nginx:1.18``` using this command:

```
kubectl set image deployment/nginx-deployment nginx-container=nginx:1.18

```
<br>

*Explaination:*
<br>

| Segment                         | Description                                                                 |
|---------------------------------|-----------------------------------------------------------------------------|
| `kubectl`                       | Kubernetes CLI tool                                                        |
| `set image`                     | Subcommand to update container images                                      |
| `deployment/nginx-deployment`  | Specifies the target Deployment named `nginx-deployment`                   |
| `nginx-container=nginx:1.18`   | Updates the container named `nginx-container` to use the `nginx:1.18` image |
<br>

To verify the rollback, we can use the following commands:

```
kubectl rollout status deployment/nginx-deployment
```
```
kubectl describe deployment nginx-deployment
```
<br>


