It isn't just pods which end up being created in the underlying cluster, it is
also services, ingresses and other resources such as persistent volume claims.

In order to expose the service create an Ingress resource by executing:

```terminal:execute
command: |-
  cat >> nginx-sample/ingress.yaml << EOF
  apiVersion: networking.k8s.io/v1
  kind: Ingress
  metadata:
    name: nginx
    labels:
        app: nginx
  spec:
    rules:
    - host: {{session_namespace}}-nginx.{{ingress_domain}}
      http:
        paths:
        - path: "/"
          pathType: Prefix
          backend:
            service:
              name: nginx
              port:
                number: 8080
  EOF
```

and reapply the resources for the deployment.

```terminal:execute
command: kubectl apply -f nginx-sample -n website
```

The ingress is still being created in the virtual Kubernetes cluster, but we
set the hostname for the ingress to be a name which we know will be mapped to
the inbound ingress router of the underlying Kubernetes cluster.

The website can then be access outside:

```terminal:execute
command: curl {{session_namespace}}-nginx.{{ingress_domain}}
```

This works without needing to deploy a separate ingress control in the virtual
Kubernetes cluster.
