# Useful commands & links

Examples of mounting a volume:
https://kubernetes.io/docs/concepts/storage/volumes/#hostpath

# Instructions

## Volumes

If you didn't notice it yet, but once our mysql container is terminated, all
the data is lost too.

The easiest solution to this problem is to make the mysql's `/var/lib/mysql`
data directory reside on a volume.

1. Modify the mysql's deployment file from lesson `03-deployments` to mount a
hostPath type volume at the `/var/lib/mysql` path inside the mysql container.

>To check that your configuration is working, you can run the following command
to write some data to the directory:

```
kubectl exec -ti <MYSQL_POD_NAME> -- touch /var/lib/mysql/its_a_test
```

2. Then restart the mysql pod using the `kubectl delete pod <POD_NAME>` command,
and check that your data is still on disk with the next command:

```
kubectl exec -ti <NEW_MYSQL_POD_NAME> -- ls /var/lib/mysql/
```