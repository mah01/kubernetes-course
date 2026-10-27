# A. Setup

* If you use your own machine
  * You will be given an ip and private key
  * Simply connect to the remote machine with SSH client
    * Both modern Windows and macOS have built int SSH clients
      * `ssh root@<ip> -i <path_to_key>`
* If you prefer to use remote machine
  * You need:
    * [`kubectl`](https://kubernetes.io/docs/tasks/tools/#kubectl)
      * You can simply download the binary `kubectl` from the [Kubernetes release page](https://kubernetes.io/releases/download/#binaries) and put it into your `PATH`
    * To configure access to the cluster:
      1. Download you cluster `cluster-<CLUSTER>-kubeconfig.yaml` file
      2. Create environment variable or simply export it in your terminal:
         * Windows
           * `set KUBECONFIG=<path_to_cluster-<CLUSTER>-kubeconfig.yaml>`
         * Everywhere else
           * `export KUBECONFIG=<path_to_cluster-<CLUSTER>-kubeconfig.yaml>`
      3. Make sure you get nodes out of _your_ cluster by writing
         * `kubectl get nodes`

It is beneficial to have Docker installed as well.
If you do not have it installed, you can use a remote machine with Docker installed.



# B. Minimal shell skills

This is not a Linux or console course after all.
Most of the things are the same as in the Windows terminal (if you are coming from Windows) or are straightforward.
However, let's make sure we all know how to use a text editor on a remote computer (if you have not used one before) and make HTTP requests using `curl`.


## exercise 01

1. Send a `curl` request to `dr.dk`
2. Using the `-i` flag that returns response headers, figure out where the site is redirecting you to
3. Figure out the final URL you are being redirected to and get the content of that page using `curl`
4. Use the `-L` flag instead (that simply follows redirects) and get the contents of `dr.dk` in one go


## exercise 02

1. Create a dummy file at `/tmp/test.txt` using a text editor
  * Use either `nano` or `vim` that are present on the remote machine
2. Add some sample text content to the file
3. Save and exit the editor
4. Verify the file was created using `cat /tmp/test.txt`

### Basic Commands Reference

For quick reference, here are the essential commands you'll use:

* `ls` - list files and directories
* `cd` - change directory
* `pwd` - show current directory path
* `cat` - display file contents
* `nano` - simple text editor (easier for beginners)
* `curl` - make HTTP requests
