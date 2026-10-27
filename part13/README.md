# A. Persistent storage

## exercise 01: Persistent storage with PVC

1. Create a YAML file with:
   * A PersistentVolumeClaim
     * storageClassName: `do-block-storage`
     * size: `1Gi`
   * A Pod running `nginx`
     * Mount the PVC to:
       * `/usr/share/nginx/html`
2. Apply the configuration  
   * `kubectl apply -f file.yaml`
3. Verify PVC is created and bound  
   * `kubectl get pvc`
4. Verify Pod is running  
   * `kubectl get pods`
5. Forward a port to the Pod  
   * `kubectl port-forward pod/<pod_name> 8080:80`
6. Verify application is accessible  
   * `curl localhost:8080`
7. Modify content inside the container  
   * `kubectl exec -it <pod_name> -- /bin/bash`
   * `echo "hello from pvc" > /usr/share/nginx/html/index.html`
   * `exit`
8. Verify updated content  
   * `curl localhost:8080`
9. Delete the Pod  
   * `kubectl delete pod <pod_name>`
10. Recreate the Pod  
    * `kubectl apply -f file.yaml`
11. Forward port again if needed  
    * `kubectl port-forward pod/<pod_name> 8080:80`
12. Verify content again  
    * `curl localhost:8080`
13. Is the content still there?


## exercise 02: Inspect PVC (optional)

1. List PersistentVolumeClaims  
   * `kubectl get pvc`
2. Describe the PVC  
   * `kubectl describe pvc <pvc_name>`
3. Observe
   * Status (Bound)
   * Storage size
   * StorageClass used
   * Volume name
