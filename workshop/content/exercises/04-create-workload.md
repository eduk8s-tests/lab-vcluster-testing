Deploying workloads to the virtual Kubernetes cluster is the same as for
a normal Kubernetes cluster.

To deploy the ``nginx`` web server using the supplied sample configuration
run:

```terminal:execute
command: kubectl apply -f nginx-sample -n website
```

To monitor the deployment run:

```terminal:execute
command: kubectl rollout status deployment/nginx -n website
```

To list the pods created for the deplouyment run:

```terminal:execute
command: kubectl get pods -l app=nginx -n website
```

Now this is where things get rather interesting. That is that for any
workloads that are created for the virtual Kubernetes cluster, although the
control plane of the virtual Kubernetes manages them, they are created as pods
within the namespace of the underlying Kubernetes cluster the control plane
runs in.

To see this, run:

```terminal:execute
command: kubectl get pods -o name -n {{session_namespace}}-vc --context eduk8s
```

This will include a pod named something like:

```
pod/nginx-55dcfcc8b7-7k22b-x-website-x-vc
```

To avoid name clashes, the name is suffixed with information about the
namespace in the virtual Kubernetes cluster and the identifier for the control
plane, which in this case was ``vc``.
