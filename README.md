# Install ArgoCD : https://www.arthurkoziel.com/setting-up-argocd-with-helm/

``` helm repo add argo-cd https://argoproj.github.io/argo-helm ``` AND ```helm dep update charts/argo-cd/ ```

``` helm install --namespace=argocd --create-namespace -f charts/argo-cd/values.yaml argo-cd-release charts/argo-cd/ ```

``` kubectl get pods -l app.kubernetes.io/name=argocd-server -o name | cut -d'/' -f 2 ```

``` kubectl port-forward -n argocd svc/argo-cd-release-argocd-server 8080:80 ```

``` echo "Username: admin" ``` AND ``` echo "Password: $(kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d)" ```

``` helm template apps/ | kubectl apply -f - ```

``` helm delete -n argocd argo-cd-release ``` 

## Set bcrypt password to "password"
``` kubectl -n argocd patch secret argocd-secret   -p '{"stringData": {
"admin.password": "$2a$10$rRyBsGSHK6.uc8fntPwVIuLVHgsAhAX7TcdrqW/RADU0uh7CaChLa",
"admin.passwordMtime": "'$(date +%FT%T%Z)'"
}}' ```
