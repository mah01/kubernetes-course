# A. Pods, imperative commands

## exercise 01: Create a Pod (imperative)

1. Run a Pod with `nginx` image
   * `kubectl run mynginx --image nginx`
2. List pods
   * `kubectl get pods`
3. Describe the pod
   * `kubectl describe pod mynginx`
4. Delete the pod
   * `kubectl delete pod mynginx`


## exercise 02: Different namespace

Repeat exercise 01 but in a different namespace.
You can use `kube-system` namespace for this purpose.



# B. Pods, declarative commands

## exercise 01: Create a Pod

1. Create a file `pod.yaml` with the following content
   * ```yaml
     apiVersion: v1
     kind: Pod
     metadata:
       name: mynginx
     spec:
       containers:
       - name: nginx
         image: nginx
     ```
2. Apply the configuration
   * `kubectl apply -f pod.yaml`
3. List pods
   * `kubectl get pods`
4. Delete the pod using the file
   * `kubectl delete -f pod.yaml`


## exercise 02: Update the Pod

1. Modify `pod.yaml`
   * Change the image to Apache HTTP server
   * Hint: search for `httpd` on Docker Hub
   * Use a tag that is not `latest`
2. Apply the configuration again
   * `kubectl apply -f pod.yaml`
3. List pods
4. Describe the pod
5. Verify
   * Which image is being used?
   * Which tag is being used?
6. Change the image tag to another version
7. Apply the configuration again
   * `kubectl apply -f pod.yaml`
8. Describe the pod again and verify the change
9. Delete the pod using the file
   * `kubectl delete -f pod.yaml`


## exercise 03: Namespaces

We will cover namespaces in detail later.
For now, we will try creating a pod in a different namespace.

1. Using reference documentation figure out how to supply pod namespace in yaml file
   * https://kubernetes.io/docs/reference/kubernetes-api/workload-resources/pod-v1/
   * Hint look at the `metadata` section
2. Create a namespace
   * `kubectl create namespace mytest`
3. Modify `pod.yaml`
   * Add namespace to metadata
     * ```yaml
       metadata:
         name: mynginx
         namespace: mytest
       ```
4. Apply the configuration
   * `kubectl apply -f pod.yaml`
5. List pods in that namespace
   * `kubectl get pods -n mytest`
6. Describe the pod
   * `kubectl describe pod mynginx -n mytest`



# C. kubectl explain

## exercise 01: kubectl explain

1. Explore Pod definition
   * `kubectl explain pod`
2. Inspect metadata section
   * `kubectl explain pod.metadata`
3. Inspect containers section
   * `kubectl explain pod.spec.containers`
4. Try to find
   * Where to define image
   * Where to define name



# D. Logs

## exercise 01: Logs

1. Analyze help output of logs command
   * `kubectl logs --help`
2. Find how to
   * Follow logs (similar to `tail -f`)
   * Show last N lines of logs
3. Run a Pod (if not already running)
   * `kubectl run mynginx --image nginx`
4. View logs
   * `kubectl logs mynginx`
5. Try
   * `kubectl logs -f mynginx`
   * `kubectl logs --tail=5 mynginx`


## exercise 02: Debugging a failing Pod (MySQL)

Running a database in Kubernetes requires configuration.  
We will intentionally start it incorrectly and debug the problem.

1. Create a `pod.yaml` with MySQL image
   * ```yaml
     apiVersion: v1
     kind: Pod
     metadata:
       name: mysql
     spec:
       containers:
       - name: mysql
         image: mysql
      ```
2. Apply the configuration
   * `kubectl apply -f pod.yaml`
3. Check pod status
   * `kubectl get pods`
4. Describe the pod
   * `kubectl describe pod mysql`
5. Inspect logs
   * `kubectl logs mysql`
6. Identify the problem
   * What error do you see?
   * Why does the container fail?
7. Fix the issue
   * Hint: MySQL requires environment variables
   * Look at Docker Hub documentation:
     * https://hub.docker.com/_/mysql
8. Update pod.yaml to include:
    * ```yaml
      env:
        - name: MYSQL_ALLOW_EMPTY_PASSWORD
          value: "true"
      ```
9. Reapply the configuration
   * You may need to delete the pod first
     * `kubectl delete pod mysql`
   * Then
     * `kubectl apply -f pod.yaml`
10. Verify the pod is running
    * `kubectl get pods`
11. Check logs again
    * `kubectl logs mysql`



# E. run and exec

## exercise 01: Run custom command

1. Run a Pod with a custom command
   * `kubectl run mynginx --image nginx -- echo testhest`
2. Check pod status
   * `kubectl get pods`
3. What is the status of the pod?
4. Inspect logs
   * `kubectl logs mynginx`
5. Delete the pod
   * `kubectl delete pod mynginx`


## exercise 02: kubectl exec

1. Run a Pod
   * `kubectl run mynginx --image nginx`
2. Execute a command inside the container
   * `kubectl exec mynginx -- date`
3. Start interactive shell
   * `kubectl exec -it mynginx -- /bin/sh`
4. Inside the container:
   * Run `ls`
   * Run `ps`
5. Exit the container
6. Delete the pod
   * `kubectl delete pod mynginx`


## exercise 03: Modify running container

1. Run a Pod with Apache HTTP server
   * `kubectl run myhttpd --image httpd`
2. Start interactive shell
   * `kubectl exec -it myhttpd -- /bin/bash`
3. Inside the container:
   * Update package list  
     `apt-get update`
   * Install curl  
     `apt-get install -y curl`
   * Verify web server  
     `curl localhost`
4. Modify default page
   * Edit file:
     `/usr/local/apache2/htdocs/index.html`
   * Example:
     `echo "testhest" > /usr/local/apache2/htdocs/index.html`
5. Verify change
   * `curl localhost`
6. Exit container
   * `exit`
7. Delete the pod
   * `kubectl delete pod myhttpd`

  
## exercise 04: MySQL client (optional)

1. Run a MySQL Pod
   * Make sure to include:
     * `MYSQL_ALLOW_EMPTY_PASSWORD=true`
     * see https://kubernetes.io/docs/reference/kubernetes-api/workload-resources/pod-v1/#environment-variables
     * or see `kubectl run --help` for environment variable syntax
2. Start interactive shell
   * `kubectl exec -it <pod_name> -- /bin/bash`
3. Run MySQL client
   * `mysql`
4. Explore:
   * Try basic commands
5. Exit and delete the pod



# F. Labels

## exercise 01: Labels

1. Run three Pods with different labels
   * `kubectl run pod1 --image=nginx --labels="app=web,env=dev"`
   * `kubectl run pod2 --image=nginx --labels="app=web,env=prod"`
   * `kubectl run pod3 --image=nginx --labels="app=db,env=dev"`
2. List pods with labels
   * `kubectl get pods --show-labels`
3. Select pods by label
   * All pods with `app=web`  
     `kubectl get pods -l app=web`
   * All pods with `env=dev`  
     `kubectl get pods -l env=dev`
4. Select using multiple labels
   * `kubectl get pods -l app=web,env=dev`
5. Delete the pods
   * `kubectl delete pod pod1 pod2 pod3`


## exercise 02: Labels (declarative)

1. Create a Pod yaml with a label
   * Use reference:
     * https://kubernetes.io/docs/reference/kubernetes-api/workload-resources/pod-v1/
   * Hint:
     * `kubectl explain pod.metadata`
2. Note:
   * Labels are defined as a map:
     * `key: value`
3. Apply the configuration
   * `kubectl apply -f pod.yaml`
4. List pods with labels
   * `kubectl get pods --show-labels`
5. Add another label to the YAML file
6. Apply the configuration again
   * `kubectl apply -f pod.yaml`
7. What happens to the Pod?
8. List pods with labels
   * `kubectl get pods --show-labels`
9. Delete the pod
   * `kubectl delete -f pod.yaml`
