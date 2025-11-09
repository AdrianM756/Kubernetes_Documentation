**Init containers** are specialized containers that run **before** the main application containers in a Kubernetes Pod. They're designed to perform setup scripts, configuration tasks, or prerequisite checks that must complete successfully before the main application can start.

---

## Characteristics of Init Containers

| Characteristic | Description |
| :--- | :--- |
| **Execution Order** | Init containers **always run to completion** one by one, **sequentially**, in the order they are defined. |
| **Main Container Startup** | The main application containers in the Pod will **not** start until all init containers have run successfully. |
| **Failure Handling** | If an init container fails (exits with a non-zero status code), Kubernetes **restarts the entire Pod** repeatedly until the init container succeeds, enforcing the prerequisite. |
| **Resource Isolation** | They share the Pod's network, volumes, and security context, but their **resource requests/limits** (CPU, memory) are handled separately and do not overlap with the main containers. |
| **Purpose** | They are primarily used for tasks like **preparing the environment**, fetching configuration, or **delaying startup** until a dependency (like a database service) is available. |

---

## Common Use Cases

Init containers are crucial for preparing an environment that is clean, configured, and ready for the main application.

* **Waiting for Services:** Delaying startup until an external service (like a database or a configuration server) is reachable. This prevents the main application from crashing during initialization due to missing dependencies.
* **Environment Setup:** Running setup scripts, performing necessary permission changes, or creating initial directories and files in a **shared volume**.
* **Configuration Retrieval:** Using tools like `wget` or `git` to clone configuration files, security certificates, or application binaries from a remote location and placing them in a shared volume.
* **Security Context Setup:** Setting correct file ownership and permissions for application data stored in a volume before the main process attempts to access it.
