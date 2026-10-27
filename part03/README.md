# A. kubectl basics

## exercise 01: Explore the cluster

1. List cluster nodes
   * `kubectl get nodes`
2. List pods in the default namespace
   * `kubectl get pods`
3. List pods in all namespaces
   * `kubectl get pods -A`
4. List namespaces
   * `kubectl get namespaces`


## exercise 02: Discover kubectl

1. Run
   * `kubectl`
2. Try the `--help` option with different commands
   * `kubectl get --help`
   * `kubectl describe --help`
3. Find
   * How to specify a namespace
   * How to list all resources


## exercise 03: Inspect resources

1. Pick one pod from the first exercise
   * There are pods only in other namespaces
2. Describe the pod
   * `kubectl describe pod <pod_name> -n <namespace>`
3. Look for
   * Events
   * Container image
   * Status
