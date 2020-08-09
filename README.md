These docker files will be used to build docker images for debugging tools like curl, telnet, nmap, ping, nping etc. 
In Kubernetes, its hard to install these tools on the non-root docker containers for debugging. 
So its better to install these images on the kube namespace/serviceaccount to debug using kubectl.

For example:

These images are already prebuilt in dockerhub:

`docker pull kalaipm/utils:latest`

To install packages in non-root docker container in k8s:

* Login to respective node by getting node ip using this command `kubectl get pods -o wide -n=default`
* ssh to node using respective ssh key
* To see the containers in node - `docker ps -a`
* exec into that container as root - `docker exec -it --user='root' <container id> sh`
* Then install these packages - `apt update && apt install curl -y`


To install in k8s using kubectl:
`kubectl run utils-pod --image=kalaipm/utils --namespace=default --serviceaccount=default`

