# Install ArgoCD : https://www.arthurkoziel.com/setting-up-argocd-with-helm/

``` helm install argo-cd-release bitnami/argo-cd ```

``` kubectl port-forward --namespace default svc/argo-cd-release-server 8080:80 ```

``` echo "Username: admin" ``` AND ``` echo "Password: $(kubectl -n default get secret argocd-secret -o jsonpath="{.data.clearPassword}" | base64 -d)" ```