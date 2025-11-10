[Kubernetes Secret](https://kubernetes.io/docs/concepts/configuration/secret/) is an object stores and manages sensitive information. When a Secret is created, the data values are stored as Base64 encoded strings, not truly encrypted by default. This is an encoding, not an encryption method, meaning the security primarily relies on controlling access to the Secret object itself.
<br>

# Creating Kubernetes Secrets

You can create Secrets using the `kubectl` command from literal values or files, or by defining them in a YAML manifest.

---

## 1. From Literal Values

This method is quick but requires you to pass the secret value directly on the command line.

```
kubectl create secret generic my-db-secret \
  --from-literal=username='admin' \
  --from-literal=password='S3cureP@ss'
```
<br>

## From Files

This method is generally more secure as it prevents the sensitive values from being stored in your shell history.

Preparation: Create Secret Files
```
echo -n 'admin' > ./username.txt
echo -n 'S3cureP@ss' > ./password.txt
```
<br>

Creation Command
```
kubectl create secret generic my-db-secret \
  --from-file=username=./username.txt \
  --from-file=password=./password.txt
```
<br>

From a YAML
When using a ```YAML``` manifest with the ```data``` field, you must first Base64-encode the sensitive values.

```my-secret.yaml```

YAML
```
apiVersion: v1
kind: Secret
metadata:
  name: my-db-secret-yaml
type: Opaque
data:
  username: YWRtaW4= # Base64 for 'admin'
  password: UzNjdXJlUEBzcw== # Base64 for 'S3cureP@ss'
```
<br>

Application

```
kubectl apply -f my-secret.yaml
```
<br>

***NOTE:*** Because Secrets are only Base64-encoded by default, the most important security measure is to enable encryption for etcd at rest on the Kubernetes control plane. This ensures that even if an attacker gains access to the underlying storage, the sensitive data remains encrypted.

