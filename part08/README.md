# A. Creating ConfigMaps

## exercise 01: Create ConfigMap from command line

1. Look at the help output
   * `kubectl create configmap --help`
2. Create a ConfigMap with two values
   * `kubectl create configmap myconfig --from-literal=key1=value1 --from-literal=key2=value2`
3. List ConfigMaps
   * `kubectl get configmaps`
4. Inspect the ConfigMap
   * `kubectl get configmap myconfig -o yaml`
5. Delete the ConfigMap
   * `kubectl delete configmap myconfig`


## exercise 02: Create ConfigMap from files

1. Create two text files with any content `file1.txt` and `file2.txt`
2. Create a ConfigMap from the files
   * `kubectl create configmap myconfig --from-file=file1.txt --from-file=file2.txt`
3. Inspect the ConfigMap
   * `kubectl get configmap myconfig -o yaml`
4. Delete the ConfigMap
   * `kubectl delete configmap myconfig`


## exercise 03: Create ConfigMap with YAML

1. Create a YAML file defining a ConfigMap with:
   * `key1=value1`
   * `key2=value2`
2. Apply the configuration
   * `kubectl apply -f configmap.yaml`
3. Inspect the ConfigMap
   * `kubectl get configmap myconfig -o yaml`
4. Delete the ConfigMap
   * `kubectl delete -f configmap.yaml`



# B. Use ConfigMap as environment variables

## exercise 01: Use ConfigMap as environment variables

1. Create a ConfigMap containing MySQL password
   * Note: this is only for demonstration
2. Create a Deployment using image `mysql`
3. Use the ConfigMap value as `MYSQL_ROOT_PASSWORD`
4. Apply the configuration
   * `kubectl apply -f file.yaml`
5. Verify the Pod starts successfully
   * `kubectl get pods`
   * `kubectl logs <pod_name>`
6. Open shell in the Pod
   * `kubectl exec -it <pod_name> -- /bin/bash`
7. Connect to MySQL
   * `mysql -u root -p`
8. Enter the password from the ConfigMap
9. Make sure you connect successfully



# C. Use ConfigMap as files

## exercise 01: Use ConfigMap as files

1. Create a file `myfile.html` with any HTML content
2. Create a ConfigMap from that file
   * `kubectl create configmap myhtml --from-file=myfile.html`
3. Create a Deployment with nginx
4. Mount the ConfigMap file into the container as:
   * `/usr/share/nginx/html/index.html`
5. Create a Service of type NodePort
6. Apply the configuration
7. Access the application via NodePort
8. Do you see your custom HTML?



# D. Secrets

## exercise 01: Using Secrets

1. Create a Secret from command line
   * `kubectl create secret generic mysecret --from-literal=password=test123`
2. Verify the Secret
   * `kubectl get secret mysecret -o yaml`
3. Create a Pod or Deployment that uses the Secret as environment variable
4. Apply the configuration
   * `kubectl apply -f file.yaml`
5. Open a shell in the Pod
   * `kubectl exec -it <pod_name> -- /bin/sh`
6. Print the environment variable
   * `echo $PASSWORD`
7. Does it match the Secret value?
