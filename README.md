## ArgoCD on Local K8s Cluster

This is a simple guide to setup ArgoCD on a local K8s cluster.

### Prerequisites

- [Docker](https://www.docker.com/)
- [Kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/)

### Setup

1. ```kubectl create namespace argocd```
2. ```kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml```

3. Check the status of the pods

```kubectl get pods -n argocd```    

4. ```kubectl port-forward svc/argocd-server -n argocd 8080:443```
5. ```kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d; echo```
6. https://argo-cd.readthedocs.io/en/stable/cli_installation/ - Install ArgoCD CLI
7. ```kubectl patch svc argocd-server -n argocd -p '{"spec": {"type": "LoadBalancer"}}'```
8. ```kubectl get svc argocd-server -n argocd```
9. ```argocd login localhost``` - Login to ArgoCD CLI
10. ```argocd account update-password```
11. ```argocd cluster add docker-desktop```
12. ```argocd app list```
13. ```kubectl config set-context --current --namespace=argocd```
14. Add app from CLI - ```argocd app create guestbook --repo https://github.com/argoproj/argocd-example-apps.git --path guestbook --dest-server https://kubernetes.default.svc --dest-namespace default```
15. ```argocd app list```

### References

- [ArgoCD](https://argoproj.github.io/argo-cd/)
- [ArgoCD on Minikube](https://argoproj.github.io/argo-cd/getting_started/#1-install-argo-cd)
- [ArgoCD on Docker Desktop](https://argoproj.github.io/argo-cd/getting_started/#2-create-an-application)





argocd app create guestbook 
--repo https://github.com/argoproj/argocd-example-apps.git 
--path guestbook 
--dest-server 
https://kubernetes.default.svc 
--dest-namespace default