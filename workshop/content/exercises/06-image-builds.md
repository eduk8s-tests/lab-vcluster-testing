There are a lot more interesting aspects to how the virtual Kubernetes
cluster interacts and makes use of the underlying Kubernetes cluster, but
we will leave it at that for now.

One final thing worth being aware of is how the virtual Kubernetes cluster can
interact with the Educates environment.

To illustrate this, lets make use of the Educates workshop feature to allow
building of container images using ``docker`` and pushing them to an image
registry associated with the workshop session. We will then update the
deployment for out web site to use the image we just built and which was
store in the image registry for the session.

First we build the container image by running:

```terminal:execute
command: docker build -t nginx-website nginx-files
```

Tag the image with the details of the image registry for the workshop
session:

```terminal:execute
command: docker tag nginx-website {{registry_host}}/nginx-website:latest
```

and push the image to the registry.

```terminal:execute
command: docker push {{registry_host}}/nginx-website:latest
```

Next create an image pull secret with the credentials for the image registry.

```terminal:execute
command: kubectl create secret docker-registry session-registry --docker-server={{registry_host}} --docker-username={{registry_username}} --docker-password={{registry_password}} -n website
```

Patch the service account used for the deployment with the name of the image pull secret.

```terminal:execute
command: |-
  kubectl patch serviceaccount default -p '{"imagePullSecrets": [{"name": "session-registry"}]}' -n website
```

Set the image used by the deployment to use the image we just built.

```terminal:execute
command: kubectl set image deployment/nginx nginx={{registry_host}}/nginx-website:latest -n website
```

Wait for the redeployment to finish.

```terminal:execute
command: kubectl rollout status deployment/nginx -n website
```

And check that we get the desired result.

```terminal:execute
command: curl {{session_namespace}}-nginx.{{ingress_domain}}
```
