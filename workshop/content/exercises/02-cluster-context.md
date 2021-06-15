Although what we see here is the virtual Kubernetes cluster for this specific
workshop session, it is still possible to interact with the underlying
Kubernetes cluster where Educates is running.

To do this it is necessary to specify the context of the cluster you want
to access.

To see what contexts exist, run:

```terminal:execute
command: kubectl config get-contexts
clear: true
```

The output should be:

```
CURRENT   NAME                                                 CLUSTER                                              AUTHINFO                                             NAMESPACE
          eduk8s                                               in-cluster-config                                    eduk8s                                               {{session_namespace}}
*         vcluster_lab-{{session_namespace}}-vc_vcluster   vcluster_lab-{{session_namespace}}-vc_vcluster   vcluster_lab-{{session_namespace}}-vc_vcluster   default
```

To see the list of namespaces for the Kubernetes cluster hosting Educates,
rather than the virtual Kubernetes cluster, run:

```terminal:execute
command: kubectl get ns --context eduk8s
```

This will output a potentially long list of namespaces as you will be able
to see namespaces corresponding to any Educates workshops being hosted on
the cluster, along with namespaces for each specific workshop session. You
will only be able to see inside of the namespaces which are associated with
your workshop session.

Of the namespaces you can see inside, the key one as far as the virtual
Kubernetes cluster is concerned is called ``{{session_namespace}}-vc``. This
is the namespace where the virtual Kubernetes cluster is being run.

To see what is currently running in that namespace run:

```terminal:execute
command: kubectl get all -n {{session_namespace}}-vc --context eduk8s
```

You should see output similar to:

```
NAME             READY   STATUS    RESTARTS   AGE
pod/vcluster-0   2/2     Running   0          10m

NAME                                  TYPE        CLUSTER-IP     EXTERNAL-IP   PORT(S)                  AGE
service/kube-dns-x-kube-system-x-vc   ClusterIP   10.96.245.84   <none>        53/UDP,53/TCP,9153/TCP   10m
service/vcluster                      ClusterIP   10.96.40.80    <none>        443/TCP                  10m
service/vcluster-headless             ClusterIP   None           <none>        443/TCP                  10m

NAME                        READY   AGE
statefulset.apps/vcluster   1/1     10m
```

All that is currently running is the control plane for the virtual Kubernetes
cluster.

Do note though that RBAC has been setup to allow only view access to the
workshop user for the namespace that the virtual Kubernetes cluster is running
in. So you can view details of some resources, but not interact with any
deployments directly within the namespace. Any interaction must be via the
virtual Kubernetes cluster.
