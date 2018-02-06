# Useful commands & links

Examples for the service YAML format can be found here:
https://kubernetes.io/docs/concepts/services-networking/service/

```
kind: Service
apiVersion: v1
metadata:
    name: my-service
    labels:
        app: my-service
spec:
    type: NodePort # Attached to node's port
    selector:
        app: <POD'S_LABEL>
    ports:
        - name: http
          protocol: TCP
          port: 80
          targetPort: 9376
          nodePort: 30000 # Attached to node's port
```

# Instructions

## Let's access Wordpress And Mysql Pods

In the last exercise we've created a multi-container pod that runs wordpress
and mysql containers.

Although the containers were running perfectly, we didn't expose the services to
traffic outside IBM Cloud cluster. Let's do it now!

1. Create a YAML service definition to route traffic to the wordpress container from the previous exercise.
2. Check that the new service has any active endpoints using the `kubectl describe svc ...` command.
2. Make sure that you can connect to the wordpress UI with a browser, use
`minikube service ...` command to connect via the newly created service.

Services are Layer 4 constructs which means you aren't restricted to HTTP only,
you can expose TCP and UDP traffic too.

1. Add another service, this time expose mysql's standard port (3306). As
before, write a small YAML definition and use the `kubectl apply` command to
submit it to the cluster.
2. Check that you can access the mysql port using `telnet`.

## I'm feeling lucky

>You can review the YAML specification that Kubernetes created for you with the
`kubectl get svc <NAME> -o yaml` command. Is it different from what you've
created yourself before?

