# Prerequisites

1. Running Kubernetes Cluster on IBM Cloud ([free for IBMers](https://console.bluemix.net/containers-kubernetes/clusters))
2. IBM Cloud CLI ([bx](https://clis.ng.bluemix.net/))
3. Container Service plugin installed - (bx plugin install container-service -r Bluemix)
4. Kubernetes CLI ([kubectl](https://kubernetes.io/docs/user-guide/prereqs/))

# Useful commands & links

```
bx login -a https://api.eu-gb.bluemix.net --sso
bx cs region-set <CLUSTER_LOCATION>

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
  4.a. Download the config `bx cs cluster-config <CLUSTER_NAME>`
  4.b. Copy and paste the output to your terminal (SET / export)
5. Check that your `kubectl` is connected to the new cluster. You can verify it by checking the node names in the cluster (`kubectl get nodes`)

3. Upload the configuration defined in `hello-world.yml` file (`kubectl create -f <file-name>`)
4. Wait until the application's pod will be in the **running** state by querying it's status with
`kubectl get pods` command
    1. If it's not running yet, can you check why? Use the describe command
    mentioned below and look at the **Events** field.
5. View the application's pod definition by using the `kubectl describe pod
<POD_NAME>` command
    1. Can you discover pod's internal IP address?
    2. How about it's node. Can you find the IP of the node that is running this pod?
6. Use `minikube service hello-world` to open the application in the browser
7. Now let's stop the application by running `kubectl delete pod <NAME>`
8. Can you access it's UI now? Are there any listed endpoints for the applications service? (`kubectl describe service hello-world`)
