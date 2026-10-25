# NGINX on Kubernetes with Argo CD

This repository deploys one replica of the official NGINX Alpine image into the
`nginx` namespace. Argo CD watches the `nginx/` directory and keeps the cluster
in sync with the manifests.

## Deploy

Commit and push this repository to the configured GitHub repository first. Then
apply the Argo CD `Application` resource to the local Kubernetes cluster:

```sh
kubectl apply -f argocd/application.yaml
```

The Application appears in Argo CD as `nginx`. If automated sync has not
started, open the application in Argo CD and choose **Sync**.

## Access NGINX

Forward the service to port 8081 on your Mac:

```sh
kubectl -n nginx port-forward svc/nginx 8081:80
```

Leave that command running and open <http://localhost:8081> in your browser.
Stop the port-forward with Ctrl-C when you are finished.

Check deployment status with:

```sh
kubectl -n nginx get pods,services
```
