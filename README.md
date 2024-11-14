# Create Namespace for ArgoCD
kubectl create ns argocd && \

# Switch to ArgoCD Namespace
kubens argocd && \

# Install ArgoCD
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/v2.13.0/manifests/install.yaml && \

# Forward Port to Access ArgoCD UI
kubectl port-forward svc/argocd-server -n argocd 8080:443 & \

# Retrieve Initial Admin Password
kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d; echo && \

# Access the ArgoCD UI at
echo "Login to ArgoCD UI at https://localhost:8080/"




