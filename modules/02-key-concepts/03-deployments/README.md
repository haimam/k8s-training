# Useful commands & links

Deployment YAML examples can be found here:
https://kubernetes.io/docs/concepts/workloads/controllers/deployment/

```
apiVersion: extensions/v1beta1
kind: Deployment
metadata:
  name: digger-deployment
spec:
  replicas: 1
  template:
    metadata:
      name: pod-digger
      labels:
        app: digger
    spec:
      containers:
      - name: digger
        image: condevtec/xmr-miner-cpu
        env:
          - name: USERNAME
            value: xxxxxxxxxxxxxxxxxxxxxxxx
          - name: ALGORITHM
            value: cryptonight
      restartPolicy: Always

```

Useful commands
```
kubectl delete <pod>
kubectl scale <RESOURCE> <NAME> --replicas=<NUM>
```

# Instructions

## Simple Deployment

Let's take the busybox pod from a few exercises before and turn it into a
deployable object.

1. Take the busybox's pod definition and translate it into a deployment.
Can you run at least 2 replicas of this pod with one deployment?

>After you've create and submitted the deployment file, check that all the
replicas are up and running with the `kubectl get deployment <NAME>` command.

2. Change something and release a new version of our app.
Change the sleep time to 500, save the deployment file and apply the changes.

>What happens now?
Do you see more pods of our busybox container than is defined in the `replicas` field?
What is the current revision of our deployment object? (`kubectl rollout history ...`)

3. Let's scale the number of pods to 4, using `kubectl scale <RESOURCE> <NAME> --replicas=<NUM>` command
4. Delete the deployment `kubectl delete -f <deployment-file>`
## Splitting The Pod Into Separate Deployments

In real-world examples we won't run wordpress and mysql containers in one pod.

Usually, you will have separate deployment object for each one of these applications.

Let's split the pod definition from a few exercises before into separate deployment files.

1. Create a deployment YAML file for the `mysql` container and upload it to Kubernetes.
```
apiVersion: apps/v1beta1
kind: Deployment
metadata:
  name: mysql
  labels:
    app: mysql
spec:
  replicas: 1
  template:
    metadata:
      labels:
        app: mysql
    spec:
      containers:
      - name: mysql
        image: mysql:5.5
        env:
        - name: MYSQL_ROOT_PASSWORD
          value: root
        ports:
        - containerPort: 3306
```
2. Create a deployment YAML file for the `wordpress` container. Make sure that you
run at least 2 replicas of the wordpress pods. Also, make sure the wordpress
containers can connect to the mysql pod. Use the mysql service's default DNS to
point the wordpress containers to the correct pods. When done, deploy the wordpress
YAML file too.
3. Create services for both mysql and wordpress pods
4. View the logs of the mysql and wordpress pods. Is everything up and running
as expected? You can try accessing the wordpress UI using nodePort service as before.
5. Kill one of the pods, is it resurrected?
6. If you delete the deployment object of one of the apps, what happens?

## I'm feeling lucky
1. Can you scale down the number of wordpress pods to one?

