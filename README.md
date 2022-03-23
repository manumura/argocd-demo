# Install ArgoCD : https://www.arthurkoziel.com/setting-up-argocd-with-helm/

``` helm install argo-cd-release charts/argo-cd/ ```

``` kubectl get pods -l app.kubernetes.io/name=argocd-server -o name | cut -d'/' -f 2 ```

``` kubectl port-forward --namespace default svc/argo-cd-release-argocd-server 8080:80 ```

``` echo "Username: admin" ``` AND ``` echo "Password: $(kubectl -n default get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d)" ```