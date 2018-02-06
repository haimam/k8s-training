# Prerequisites

1. Running Kubernetes Cluster on IBM Cloud ([free for IBMers](https://console.bluemix.net/containers-kubernetes/clusters))
2. IBM Cloud CLI ([bx](https://clis.ng.bluemix.net/))
3. Container Service plugin installed - (`bx plugin install container-service -r Bluemix`)
4. Kubernetes CLI ([kubectl](https://kubernetes.io/docs/user-guide/prereqs/))

# Useful commands & links

```
bx login -a https://api.eu-gb.bluemix.net --sso
bx cs region-set <CLUSTER_LOCATION>
bx cs clusters
bx cs workers <CLUSTER_ID>

kubectl create -f <YAML_FILE>
kubectl get nodes
kubectl get pods
kubectl get services
kubectl describe service <NAME>
kubectl describe pod <NAME>
kubectl logs <POD_NAME>
```

# Instructions

1. Make sure that your cluster is running on IBM Cloud ([View Clusters](https://console.bluemix.net/containers-kubernetes/clusters))
2. Log in to your IBM Cloud account using the CLI
3. Set the region to where your cluster is, for example `uk-south`
4. Download the kubernetes configuration files to configure your kubectl client's context  
    1. Download the config `bx cs cluster-config <CLUSTER_NAME>`  
    2. Copy and paste the output to your terminal (SET - Win, export - OSX)
5. Check that your `kubectl` is connected to the new cluster. You can verify it by checking the node names in the cluster (`kubectl get nodes`),
on free cluster you should see single worker node

6. Upload the configuration defined in `hello-world.yml` file (`kubectl create -f <file-name>`)
7. Wait until the application's pod will be in the **running** state by querying it's status with
`kubectl get pods` command
    1. If it's not running yet, can you check why? Use the describe command
    mentioned below and look at the **Events** field.
8. View the application's pod definition by using the `kubectl describe pod
<POD_NAME>` command
    1. Can you discover pod's internal IP address?
    2. How about it's node. Can you find the IP of the node that is running this pod?
9. Let's check the worker's public IP to access it via the browser
    1. `bx cs clusters` to list all the clusters, copy the relevant cluster's ID
    2. `bx cs workers <CLUSTER_ID>`, check the worker's public IP
10. Browse to `http://<WORKER_PUBLIC_IP>:30000` to open the application in the browser
11. Now let's stop the application by running `kubectl delete pod <NAME>`
12. Can you access it's UI now? Are there any listed endpoints for the applications service? (`kubectl describe service hello-world`)