# A. Init containers

## exercise 01: nginx container with generated content

Create a Deployment where an init container generates the web page that is later served by nginx.

1. Create a yaml file with a Deployment that will have
   * A shared volume using `emptyDir` 
   * One init container
   * One main container running `nginx`
2. Configure init container to
   * Use `busybox`
   * Generate a `index.html` file into shared volume with a date in it
     * For instance using a command `["sh", "-c", "date && date > /data/index.html"]`
3. Configure the nginx container
   * Mount the same volume at `/usr/share/nginx/html`
   * This is the directory from which nginx serves files
4. Apply the Deployment and inspect the pods
5. Observe
   * Did the init container complete?
   * Is the nginx container running?
6. Inspect the init container logs (using `-c` flag in `kubectl logs`)
7. Verify that the main container returns the generated html back
8. Delete a pod from the Deployment
   * Did the init container run again?
   * Did the date on the page change?
   * Why was the previous `index.html` file not preserved?   


# B. "Native" sidecar containers

## exercise 01

Repeat the previous exercise.
But this time update the `busybox` init container to make it a native sidecar container that updates `index.html` continuously with a fresh timestamp.
