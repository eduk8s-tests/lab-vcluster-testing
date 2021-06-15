It isn't just pods which end up being created in the underlying cluster, it is
also services, ingresses and other resources such as persistent volume claims.

Like with pods, you can see the corresponding service for the deployment
created in the underlying cluster.

```terminal:execute
command: kubectl get services -o name -n {{session_namespace}}-vc --context eduk8s
clear: true
```

To see what happens with an ingress, create an Ingress resource by executing:

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

Note that in this case we set the hostname for the ingress to be a name
which we know will be mapped to the inbound ingress router of the underlying
Kubernetes cluster. Even though the deployment and ingress were created via
the virtual Kubernetes cluster, that the pod and ingress end up actually
being created in the underlying Kubernetes cluster, it becomes available
externally.

To test access run:

```terminal:execute
command: curl {{session_namespace}}-nginx.{{ingress_domain}}
```

