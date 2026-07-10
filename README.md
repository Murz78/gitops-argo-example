# gitops-argo-example

At start we will install Argo CD via Helm

```
helm repo add argo https://argoproj.github.io/argo-helm
helm update
helm install -n argocd argocd argo/argo-cd
```

After installation provide secret for adding placeholders for future bootstrap

```
kubectl apply -n argocd -f - <<EOF
apiVersion: v1
kind: Secret
metadata:
  name: argocd-dev-cluster
  labels:
    argocd.argoproj.io/secret-type: cluster
type: Opaque
stringData:
  name: dev
  server: https://kubernetes.default.svc
EOF
```

And after that we may apply root app-of-apps

```
kubectl apply -f bootstrap/root.yaml
```
