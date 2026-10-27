# A. Probes

## exercise 01: Readiness probe

1. Create a Deployment with nginx
2. Add a readiness probe:
   * HTTP GET `/`
   * port 80
3. Apply configuration
   * `kubectl apply -f file.yaml`
4. Verify:
   * `kubectl get pods`
   * `kubectl describe pod <pod_name>`
5. Check Service endpoints
   * `kubectl describe service <service_name>`
6. Is the Pod included in endpoints?


## exercise 02: Failing readiness probe

Continue from previous exercise.

1. Change readiness path to something invalid
   * `/doesnotexist`
2. Apply configuration
3. Observe
   * `kubectl get pods`
   * `READY` status
4. Check Service endpoints
5. Is the Pod receiving traffic?


## exercise 03: Liveness probe

1. Create a Deployment
2. Add a liveness probe
   * HTTP GET `/`
   * port 80
3. Apply configuration
4. Check liveness probe definition and status
   * `kubectl describe pod <pod_name>`


## exercise 04: Liveness probe (failing)

1. Create a Deployment with nginx
2. Add a liveness probe
   * exec command
     * `cat /tmp/healthy`
3. Apply configuration
   * `kubectl apply -f file.yaml`
4. Verify Pod is running
   * `kubectl get pods`
5. Create the file inside the container
   * `kubectl exec -it <pod_name> -- /bin/sh`
   * `touch /tmp/healthy`
   * `exit`
6. Verify
   * Pod stays running
7. Remove the file
   * `kubectl exec -it <pod_name> -- /bin/sh`
   * `rm /tmp/healthy`
   * `exit`
8. Observe
   * `kubectl get pods`
   * `kubectl describe pod <pod_name>`
9. Verify
   * Container is restarted
