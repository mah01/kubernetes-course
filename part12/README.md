# A. Requests and limits

## exercise 01: Requests and limits

1. Inspect nodes
   * `kubectl get nodes`
   * `kubectl describe node <node_name>`
2. Observe
   * Capacity
   * Pods
3. Create a Deployment with resource requests and limits
   * 3 replicas
   * `nginx`
   * requests:
     * 50m CPU
     * 50Mi memory
   * limits:
     * 100m CPU
     * 100Mi memory
4. Apply configuration
   * `kubectl apply -f file.yaml`
5. Describe the Pod
   * `kubectl describe pod <pod_name>`
6. Observe
   * requests and limits values
7. Increase requests to a very high value
8. Apply configuration again
9. Does the Pod start?
10. Is the Pod running?
    * `kubectl describe pod <pod_name>`


## exercise 02: Requests and limits (similr, but scaling instead)

1. Create a Deployment with
   * 1 replica
   * `nginx`
   * requests:
     * 50m CPU
     * 50Mi memory
   * limits:
     * 100m CPU
     * 100Mi memory
2. Apply configuration
3. Verify
   * `kubectl get pods`
   * Is the Pod scheduled?
4. Describe the node again
5. Observe
   * Has allocated resource usage changed?
6. Scale the Deployment to 10 replicas
7. Verify
   * `kubectl get pods`
8. * Are all Pods scheduled?
9. If some Pods are Pending
   * `kubectl describe pod <pod_name>`
10. What is the reason?
