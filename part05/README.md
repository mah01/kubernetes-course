# A. ReplicaSet

## exercise 01: Create a ReplicaSet

1. Create a ReplicaSet yaml with 3 replicas of nginx
2. Apply the configuration
   * `kubectl apply -f replicaset.yaml`
3. List pods
   * `kubectl get pods`
4. List ReplicaSets
   * `kubectl get rs`
5. Describe the ReplicaSet
   * `kubectl describe rs <name>`


## exercise 02: Self healing

Continuation of the previous exercise

1. Delete one of the Pods
   * `kubectl delete pod <pod_name>`
2. List pods again
   * `kubectl get pods`
3. Observe what is hapenning?
   * Was the pod recreated?
4. Describe the ReplicaSet
   * Look at events


## exercise 03: Scaling

Continuation of the previous exercise

1. Edit the yaml file, change replicas to 5 and apply the yaml again
2. List pods
   * `kubectl get pods`
3. Change replicas back to 2 and apply the configuration


## exercise 04: Deletion

Continuation of the previous exercise

1. Delete the ReplicaSet either by using the yaml file or by using `kubectl delete rs <name>`
2. List pods
   * `kubectl get pods`
3. Were the pods deleted?


## exercise 05: ReplicaSet pod acquisition (optional)

1. Make sure no Pods or ReplicaSets are running
2. Create a Pod manually with a label
   * `kubectl run mynginx --image nginx --labels "app=mynginx"`
3. Verify the Pod is running
   * `kubectl get pods --show-labels`
4. Create a ReplicaSet with:
   * 3 replicas
   * selector matching `app=mynginx`
5. Apply the ReplicaSet
   * `kubectl apply -f replicaset.yaml`
6. List Pods
   * `kubectl get pods`
7. How many Pods are running?
8. Delete the ReplicaSet
   * `kubectl delete -f replicaset.yaml`
9. List Pods again
   * `kubectl get pods`
10. What happened to the manually created Pod?



# B. kubectl edit

## exercise 01: Editing resources

1. Create a ReplicaSet with 3 replicas
2. Edit the ReplicaSet
   * `kubectl edit rs <name>`
3. Change number of replicas to 5
4. Save and exit the editor
5. List Pods
   * `kubectl get pods`
6. How many Pods are running?
7. Change replicas back to 2
8. Observe the result


## exercise 02: apply vs edit

1. Create a ReplicaSet using a YAML file with 3 replicas
   * `kubectl apply -f replicaset.yaml`
2. Verify number of Pods
   * `kubectl get pods`
3. Edit the ReplicaSet
   * `kubectl edit rs <name>`
4. Change replicas to 5
5. Verify number of Pods
6. Now apply the original YAML again
   * `kubectl apply -f replicaset.yaml`
7. Verify:
   * `kubectl get pods`
8. What happened to the number of Pods?


## exercise 03: Editing labels (optional)

1. Create a ReplicaSet with labeled Pods
2. Edit one of the Pods
   * `kubectl edit pod <pod_name>`
3. Change its label
4. What happens to the ReplicaSet?



# C. Deployment

## exercise 01: Create a Deployment

1. Create a Deployment YAML with:
   * 3 replicas
   * `nginx` image
2. Apply the configuration
   * `kubectl apply -f deployment.yaml`
3. List Deployments
   * `kubectl get deployments`
4. List ReplicaSets
   * `kubectl get rs`
5. List Pods
   * `kubectl get pods`
6. Verify basic ReplicaSet functionality
   * Try deleting a pod and see if it is recreated


## exercise 02: Update Deployment using YAML

1. Create a Deployment with 3 replicas
   * `kubectl apply -f deployment.yaml`
2. Verify number of Pods
   * `kubectl get pods`
3. Modify the YAML file
   * Change replicas from 3 to 5
4. Apply the configuration again
   * `kubectl apply -f deployment.yaml`
5. Verify:
   * `kubectl get pods`
   * How many Pods are running?
6. Edit the Deployment directly
   * `kubectl edit deployment mynginx`
7. Change replicas to 2
8. Verify:
   * `kubectl get pods`
9. Apply the YAML file again
10. Verify:
    * `kubectl get pods`
11. What happens to the number of Pods?
12. Why do we prefer to use yaml files together with `kubectl apply` instead of using `kubectl edit`?


## exercise 03: Deploying new version

1. Create a Deployment YAML with:
   * `3` replicas
   * image `redis:5.0`
2. Apply the configuration
   * `kubectl apply -f deployment.yaml`
3. Watch Deployment status
   * `kubectl get deployments -w`
4. Open another terminal
5. Change the image in the YAML file
   * from `redis:5.0`
   * to `redis:6.0-alpine`
6. Apply the configuration again
   * `kubectl apply -f deployment.yaml`
7. Observe:
   * What happens to the Pods?
   * Are Pods replaced all at once or gradually?
   * How does Deployment status change?


## exercise 04: Wrong image tag

Continuation of the previous exercise.

1. Start from a working Deployment with:
   * `3` replicas
   * image `redis:6.0-alpine`
2. Change the image in the YAML file to a wrong tag
   * Example: `redis:testhest`
3. Apply the configuration
   * `kubectl apply -f deployment.yaml`
4. Inspect the Deployment and Pods
   * `kubectl get deployments`
   * `kubectl get pods`
   * `kubectl get rs`
5. Describe one of the failing Pods
   * `kubectl describe pod <pod_name>`
6. Observe:
   * What error do you see?
   * Are old working Pods still running?


## exercise 05: Scaling a Deployment (optional)

There are several other imperative commands which we do not prefer to use for live environments.
But of course you are welcome to experiment with them here

1. Scale the Deployment
   * `kubectl scale deployment mynginx --replicas=5`
2. List Pods
   * `kubectl get pods`
3. Scale back to 2 replicas using `kubectl scale`


## exercise 06: Updating a Deployment (optional)

Another imperative command `kubectl set`, which we do not prefer to use for live environments.
But feel free to experiment with it here.

1. Check out examples
   * `kubectl set --help`
2. Update the image
   * `kubectl set image deployment mynginx nginx=nginx:1.21`
3. Observe rollout
   * `kubectl get pods -w`
4. Check rollout status
   * `kubectl rollout status deployment mynginx`
5. List ReplicaSets
   * `kubectl get rs`
6. Observe:
   * How many ReplicaSets exist?



# D. kubectl port-forward

## exercise 01: Port-forward to a pod

1. Create a Deployment with nginx
   * `kubectl apply -f deployment.yaml`
2. Forward a local port
   * `kubectl port-forward <pod> 8080:80`
3. `curl localhost:8080`
4. Do you see nginx page?
5. Stop port-forward
   * CTRL+C


## exercise 02: Change container data and see the effect

1. Run a Pod with nginx
   * `kubectl run mynginx --image nginx`
2. Start port-forward
   * `kubectl port-forward mynginx 8080:80`
3. In another terminal, open a shell inside the Pod
   * `kubectl exec -it mynginx -- /bin/bash`
4. Update the default page
   * `echo XX > /usr/share/nginx/html/index.html`
5. Exit the shell
   * `exit`
6. Verify the updated output through the forwarded port
   * `curl localhost:8080`
7. Stop port-forward and delete the Pod
   * `kubectl delete pod mynginx`



# E. Multiple resources in one file

## exercise 01: Multiple resources in one file

1. Create a YAML file with two Pods
   * Separate them using `---`
2. Apply the file
   * `kubectl apply -f file.yaml`
3. List Pods
   * `kubectl get pods`
4. Delete both Pods using the same file
   * `kubectl delete -f file.yaml`


## exercise 02: Multiple files (optional)

1. Create a new directory
2. Inside the directory, create two YAML files
   * Each file defines one nginx Pod
3. Apply all resources in the directory
   * `kubectl apply -f .`
4. Verify Pods are running
   * `kubectl get pods`
5. Delete the resources
   * `kubectl delete -f .`
6. Go one level up and apply using directory name
   * `kubectl apply -f <directory_name>`
7. Delete the resources again
