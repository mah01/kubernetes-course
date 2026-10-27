# A. Ingress

## exercise 01: Basic Ingress

1. Apply the provided YAML file
   * `kubectl apply -f app.yaml`
2. Verify resources
   * `kubectl get pods`
   * `kubectl get services`
   * `kubectl get ingress`
3. Get node IP
   * `kubectl get nodes -o wide`
4. Access the application
   * `curl -H "Host: testhest.dk" <node-ip>:30000`
5. Do you get nginx response?


## exercise 02: Change Ingress host

1. Edit the Ingress
   * `kubectl edit ingress my-ingress`
2. Change host to
   * `myapp.local`
3. Apply/save changes
4. Test access
   * `curl -H "Host: myapp.local" <node-ip>:30000`
5. Does it still work?
