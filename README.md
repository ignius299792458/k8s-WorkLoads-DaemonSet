# k8s-WorkLoads-DaemonSet
Runs a pod on every node in the cluster

## `DaemonSet`
`Definition`: 
A DaemonSet ensures that a copy of a pod runs on every node in the cluster. As nodes are added or removed from the cluster, pods are automatically added or garbage collected.

`Example`:
Imagine you're running a large e-commerce platform with a cluster of 50 nodes. You need to collect performance metrics and logs from every single node to monitor system health.
You deploy the Prometheus Node Exporter as a DaemonSet. This ensures that one Node Exporter pod runs on each of your 50 nodes, collecting CPU, memory, disk, and network metrics.
When you scale your cluster to 60 nodes during the holiday shopping season, the DaemonSet automatically deploys Node Exporter pods to the 10 new nodes without any manual intervention. 
This gives you continuous visibility into the health of your entire infrastructure.

# Kubernetes Workload Resources Comparison

Key differences between DaemonSet, StatefulSet, ReplicaSet, and Deployment in Kubernetes:

| Feature | DaemonSet | StatefulSet | ReplicaSet | Deployment |
|---------|-----------|-------------|------------|------------|
| **Purpose** | Runs a pod on every node in the cluster | Maintains state and unique identity for pods | Maintains a stable set of replica pods | High-level resource for deploying and updating applications |
| **Pod Identity** | Each pod is unique to a node | Each pod has persistent identity and stable hostname | Pods are interchangeable | Pods are interchangeable |
| **Scaling** | Automatically scales with nodes (one pod per node) | Manual or auto-scaling with ordered creation/deletion | Manual or auto-scaling with random creation/deletion | Manual or auto-scaling with random creation/deletion |
| **Pod Naming** | Usually `<name>-<node-name>` | `<name>-0`, `<name>-1`, etc. (ordered, sequential) | Random names with hash | Random names with hash |
| **Storage** | Typically uses node storage | Supports stable persistent storage per pod | Shared storage only | Shared storage only |
| **Load Balancing** | Not inherently load-balanced (one per node) | Not automatically load-balanced (identity matters) | Load-balanced (stateless) | Load-balanced (stateless) |
| **Updates** | Rolling updates possible | Ordered, sequential updates | All pods updated simultaneously | Rolling updates, canary deployments, rollbacks |
| **Use Cases** | Monitoring, logging, networking agents | Databases, messaging queues, stateful applications | Rarely used directly (deployment uses it) | Web applications, APIs, stateless workloads |
| **Deletion Order** | Random | Reverse order (highest to lowest index) | Random | Random |
| **Owns ReplicaSet** | No | No | No | Yes (manages ReplicaSets) |
