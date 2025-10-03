## Kubectl Commands
<br>

## Inspect Deployments, Pods, and Containers

| Command | Purpose |
|--------|---------|
| `kubectl get pods` | Lists all pods and their status |
| `kubectl describe pod <pod-name>` | Shows detailed pod info including events and container states |
| `kubectl logs <pod-name>` | Displays logs from the main container in a pod |
| `kubectl logs <pod-name> -c <container-name>` | Logs from a specific container in a multi-container pod |
| `kubectl get deployment` | Lists deployments and their status |
| `kubectl describe deployment <deployment-name>` | Shows deployment details including rollout history |
<br>

## Diagnose Failures and Events

| Command | Purpose |
|--------|---------|
| `kubectl get events --sort-by=.metadata.creationTimestamp` | Lists cluster events in chronological order |
| `kubectl get pod <pod-name> -o yaml` | Full YAML output for deep inspection |
| `kubectl get nodes` | Lists nodes and their status |
| `kubectl describe node <node-name>` | Shows node conditions and resource pressure |
<br>

## Rollouts and Recovery

| Command | Purpose |
|--------|---------|
| `kubectl rollout status deployment/<deployment-name>` | Monitors rollout progress |
| `kubectl rollout history deployment/<deployment-name>` | Shows previous rollout revisions |
| `kubectl rollout undo deployment/<deployment-name>` | Rolls back to the last stable deployment |
| `kubectl set image deployment/<deployment-name> <container-name>=<new-image>` | Updates container image in a deployment |
<br>

## Live Debugging

| Command | Purpose |
|--------|---------|
| `kubectl exec -it <pod-name> -- /bin/sh` | Opens a shell inside the container (if supported) |
| `kubectl port-forward <pod-name> <local-port>:<remote-port>` | Forwards traffic to a pod for local testing |
| `kubectl top pod` | Shows resource usage (requires Metrics Server) |
<br>

## Cleanup and Restart

| Command | Purpose |
|--------|---------|
| `kubectl delete pod <pod-name>` | Deletes a pod (it will restart if part of a deployment) |
| `kubectl delete deployment <deployment-name>` | Removes a deployment and its pods |
| `kubectl scale deployment <deployment-name> --replicas=0` | Stops all pods in a deployment |
| `kubectl scale deployment <deployment-name> --replicas=N` | Restarts with N replicas |
<br>
