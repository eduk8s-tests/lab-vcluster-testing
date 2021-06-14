For details of how this workshop demonstrating creation of virtual Kubernetes
clusters is constructed. see:

* https://github.com/eduk8s-tests/lab-vcluster-testing

Note that this is still a work in progress as some tweaks are still required
to have the virtual Kubernetes cluster work seamlessly within the restricted
RBAC that an Educates session provides, as well as ensuring it is secure.
There are also some bugs that need to be fixed in the Educates operator as
well as changes to the workshop base environment image.

* https://github.com/eduk8s/pkgs-k8s-tools/issues/6
* https://github.com/eduk8s/eduk8s-operator/issues/108
* https://github.com/eduk8s/eduk8s-operator/issues/109

So consider it a reflection of what could be possible in the future but don't
try it yourself for now.
