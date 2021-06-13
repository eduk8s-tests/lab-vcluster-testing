LAB - Virtual Cluster
=====================

This workshop demonstrates how to create a virtual Kubernetes cluster for
each Educates workshop session created. When the workshop session is deleted,
the virtual Kubernetes cluster will also be deleted.

A virtual Kubernetes cluster created using this workshop can be used in
workshops where cluster admin access is required to a Kubernetes cluster.
Instead of operating against the underlying Kubernetes cluster hosting
Educates, everything will be against a virtual Kubernetes cluster contrained
within the bounds of a namespace created for the workshop session.

Note that this is still a work in progress as some tweaks are still required
to have the virtual Kubernetes cluster work seamlessly within the restricted
RBAC that an Educates session provides, as well as ensuring it is secure.
There are also some bugs that need to be fixed in the Educates operator as
well as changes to the workshop base environment image.

* https://github.com/eduk8s/pkgs-k8s-tools/issues/6
* https://github.com/eduk8s/eduk8s-operator/issues/108

So consider it a reflection of what could be possible in the future but don't
try it yourself for now.
