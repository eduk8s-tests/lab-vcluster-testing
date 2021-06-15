To demonstrate that the user of this workshop session does indeed have cluster
admin access, lets start poking around within the virtual Kubernetes cluster
and see what we can do.

First up, lets list all the namespaces in the cluster:

```terminal:execute
command: kubectl get ns
```

You should see output similar to:

```
NAME              STATUS   AGE
default           Active   5m
kube-system       Active   5m
kube-public       Active   5m
kube-node-lease   Active   5m
```

Now create a new namespace:

```terminal:execute
command: kubectl create ns website
```

Although in a normal Educates workshop session you can list all namespaces
in the Kubernetes cluster, it is not possible to see inside of namespaces
you haven't been granted access to, nor can you create new namespaces.

To show that it is possible to look in a namespace which would normally only
be accessible to a cluster admin, list the resources in the ``kube-system``
namespace:

```terminal:execute
command: kubectl get -n kube-system all -o name
```

The output should be similar to:

```
pod/coredns-66c464876b-qbzzt
service/kube-dns
deployment.apps/coredns
replicaset.apps/coredns-66c464876b
```
