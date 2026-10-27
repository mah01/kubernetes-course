# A. Service as a stable IP

## exercise 01: Service and endopints

1. Create a YAML file with:
   * A Deployment with:
     * 3 replicas
     * image `httpd`
   * A Service pointing to the Deployment
     * Make sure selector matches Pods labels
2. Apply the descriptor
   * `kubectl apply -f file.yaml`
3. Verify:
   * Pods are running  
     `kubectl get pods`
   * Service is created  
     `kubectl get services`
   * Endpoints exist  
     `kubectl describe service <service_name>`
4. Observe:
   * How many endpoints are there?
5. Delete only the Deployment
   * `kubectl delete deployment <deployment_name>`
6. Verify:
   * No Pods are running  
   * Service still exists  
   * No endpoints are present  
7. Apply the descriptor again
   * `kubectl apply -f file.yaml`
8. Verify:
   * Pods are running again  
   * Endpoints are restored  
9. Edit the Deployment
   * `kubectl edit deployment <deployment_name>`
10. Change replicas to `5`
11. Verify:
    * `kubectl describe service <service_name>`
    * How many endpoints are there?
12. Scale the Deployment down to `3`
    * `kubectl scale deployment <deployment_name> --replicas=3`
13. Verify:
    * Endpoints are updated accordingly



# B. Service and port-forwarding

## exercise 01: Port-forward to a Service

1. Create a Deployment and a Service
2. Forward a local port to the Service
   * `kubectl port-forward service/<service_name> <hostport>:<serviceport>`
3. Verify access
   * `curl localhost:<hostport>`
4. Does it work the same as port-forward to Pod?
5. Stop port-forward
   * `CTRL+C`




# C. Service and DNS

## exercise 01: Access a Service from inside the cluster

1. Create a Deployment and a Service
   * Use nginx or Apache HTTP server
2. Verify the Service exists
   * `kubectl get services`
3. Run a debug Pod
   * `kubectl run mydebug --image yauritux/busybox-curl -it -- sh`
4. From inside the debug Pod, access the Service
   * `curl <service_name>:<service_port>`
5. Do you get a response?
6. Exit the debug Pod
   * `exit`
7. Delete the debug Pod
   * `kubectl delete pod mydebug`


## exercise 02: Debug Pod with MySQL (optional)

In this exercise, we will run a MySQL database and connect to it from another Pod.

1. Create a Deployment and Service for MySQL
   * Use image: `mysql`
   * Set environment variable:
     * `MYSQL_ROOT_PASSWORD=test`
   * Service name: `mysql-service`
   * Service port: `3306`
   * targetPort: `3306`
2. Apply the configuration
   * `kubectl apply -f file.yaml`
3. Verify:
   * Pods are running  
     `kubectl get pods`
   * Service exists  
     `kubectl get services`
   * Endpoints are created  
     `kubectl describe service mysql-service`
4. Run a debug Pod with MySQL client
   * `kubectl run mydebug --image=mysql -it --env MYSQL_ROOT_PASSWORD=test -- bash`
5. Inside the debug Pod, connect to the database
   * `mysql -h mysql-service -u root -p`
6. Enter password:
   * `test`
7. Do you connect successfully?
8. Exit the debug Pod
   * `exit`
9. Delete the debug Pod



# D. NodePort

## exercise 01: NodePort

1. Create a Deployment with nginx
2. Create a Service of type NodePort
   * port: 80
   * targetPort: 80
   * do not specify nodePort (let Kubernetes choose)
3. Apply the configuration
   * `kubectl apply -f file.yaml`
4. Get the assigned NodePort
   * `kubectl get services`
5. Find the node IP
   * `kubectl get nodes -o wide`
6. Access the application
   * `curl http://<node-ip>:<nodePort>`
7. Do you get a response?
