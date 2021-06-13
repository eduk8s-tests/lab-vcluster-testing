Normally when working in an Educates workshop session the user would be given
access to a single namespace within the Kubernetes cluster to which they can
then deploy any applications. The user has admin rights over that namespace
but cannot access other namespaces, nor can they perform any cluster admin
type operations against the Kubernetes cluster as a whole.

It is possible to grant extra access rights to a user working in a workshop,
but because all the users doing a workshop are sharing the same Kubernetes
cluster, if any level of cluster admin rights is granted the users could
interfere with each other or break the whole Kubernetes cluster.

This has meant that Educates could be used for teaching developer focused
workshops, but has until now not been useful in teaching workshops about
cluster operations where cluster admin access was required.

The virtual Kubernetes cluster created for each workshop session in this
environment solves this problem as each user can be given what looks like a
unique Kubernetes cluster, including cluster admin rights over that cluster.
