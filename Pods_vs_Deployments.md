## Kubernetes: Pods vs Deployments

| **Feature**         | **Pod**                                                                 | **Deployment**                                                                 |
|---------------------|-------------------------------------------------------------------------|--------------------------------------------------------------------------------|
| **Definition**       | The smallest unit in Kubernetes. A Pod wraps one or more containers.   | A higher-level abstraction that manages Pods and ensures desired state.       |
| **Purpose**          | Runs container(s) directly. Ideal for single-use or tightly coupled apps. | Manages lifecycle, scaling, and updates of Pods.                              |
| **Lifecycle**        | Ephemeral. If a Pod dies, it won’t be automatically replaced.           | Self-healing. Automatically replaces failed Pods to maintain availability.    |
| **Scaling**          | Manual. You’d need to create more Pods yourself.                        | Declarative. You define replicas, and Kubernetes handles scaling.             |
| **Rolling Updates**  | Not supported natively.                                                  | Supports rolling updates and rollbacks out of the box.                        |
| **Use Case**         | Debugging, one-off jobs, or tightly coupled containers (e.g., sidecars). | Production workloads, stateless services, scalable







