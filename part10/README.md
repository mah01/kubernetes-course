# A. Namespaces

## exercise 01: Namespaces

1. Create a namespace
   * `kubectl create namespace dev`
2. Create a Deployment in that namespace
   * `kubectl apply -f deployment.yaml -n dev`
3. List Pods in namespace
   * `kubectl get pods -n dev`
4. Are Pods visible in `default` namespace?
5. List all Pods
   * `kubectl get pods --all-namespaces`
   * `kubectl get pods -A`


## exercise 02: Same resource names

1. Create the same Deployment in:
   * `default` namespace
   * `dev` namespace
2. List Deployments
   * `kubectl get deployments`
   * `kubectl get deployments -n dev`
3. Observe same name, different namespaces


## exercise 03: Service access across namespaces (optional)

1. Create a Service in namespace `dev`
2. Run a debug Pod in `default` namespace
3. Try to access Service using:
   * `<service_name>.<namespace>`
4. Verify connectivity
