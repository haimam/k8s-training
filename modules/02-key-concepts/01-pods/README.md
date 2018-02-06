# Useful commands & links

Pod YAML examples:
https://github.com/kubernetes/contrib/blob/master/apparmor/loader/example-pod.yaml

Another example:

```
apiVersion: v1
kind: Pod
metadata:
  name: example
  labels:
    app: example
spec:
  restartPolicy: Always
  containers:
    - name: example
      image: repo/image:tag
      command: ["run"]
      args: ["--export", "something"]
      ports:
        - containerPort: 80
      env:
        - name: SERVER_PROTOCOL
          value: tcp
```

# Instructions

## Simple Single Pod

We'll get our hands dirty by creating and running a simple pod from scratch.

The simplest pod we can run is a `busybox` container. To simulate a long
running process, we'll specify a sleep command that will make the container run
indefinitely.

1. Create a Kubernetes YAML definition for an equivalent of the following
Docker run command:

```
docker run -ti busybox:latest sleep 1000
```

>This is the part of the YAML that specifies the sleep command, make sure to fill
in the rest of the YAML:

```
containers:
    command: ["sleep"]
    args: ["1000"]
```

## Multi-Container Pods

For this exercise we would like to run a wordpress and a mysql containers in one
pod.

We'll use the official docker images, here are a few examples for how you would
run them in your local machine:

```
docker run -p 8080:80 wordpress
docker run -p 3306:3306 mysql:5.5
```

Create a Kubernetes YAML definition of a pod that will run:

1. One `wordpress` container (version *latest*)
2. One `mysql` container (version *5.5*)
3. Remember, since both of these containers run in a pod, they can communicate via localhost (127.0.0.1)
4. Connect the `wordpress` container to it's local `mysql` by specifying the
following environment variables in the pod's YAML definition:
`WORDPRESS_DB_PASSWORD` (should be `root`) and `WORDPRESS_DB_HOST`
5. For the `mysql` container, specify the following environment variable: `MYSQL_ROOT_PASSWORD` (should be `root`)
6. Specify container's port for each container, `80` for wordpress and `3306` for mysql

## Coming up, services..

1. Use the following service to access the wordpress UI
```
apiVersion: v1
kind: Service
metadata:
  name: wp-svc
  labels:
    app: wp-svc
spec:
  type: NodePort
  ports:
    - name: http
      protocol: TCP
      port: 80
      targetPort: 80
      nodePort: 30000
  selector:
    app: <POD'S_LABEL> # for example above -> app: example
```
2. Browse to `http://<WORKER_PUBLIC_IP>:30000`


