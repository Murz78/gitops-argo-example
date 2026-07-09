# gitops-argo-example

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
