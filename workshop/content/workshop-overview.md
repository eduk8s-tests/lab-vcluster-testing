This workshop demonstrates how to create a virtual Kubernetes cluster for each
Educates workshop session created. When the workshop session is deleted, the
virtual Kubernetes cluster will also be deleted.

A virtual Kubernetes cluster created using this workshop can be used in
workshops where cluster admin access is required to a Kubernetes cluster.
Instead of operating against the underlying Kubernetes cluster hosting
Educates, everything will be against a virtual Kubernetes cluster constrained
within the bounds of a namespace created for the workshop session.
