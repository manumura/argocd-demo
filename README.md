# Install ArgoCD : 
## https://www.arthurkoziel.com/setting-up-argocd-with-helm/
## https://medium.com/devopsturkiye/self-managed-argo-cd-app-of-everything-a226eb100cf0
## https://medium.com/dzerolabs/turbocharge-argocd-with-app-of-apps-pattern-and-kustomized-helm-ea4993190e7c

``` helm repo add argo-cd https://argoproj.github.io/argo-helm ``` AND ``` helm dep update charts/argo-cd/ ```

``` helm install --namespace=argocd --create-namespace -f charts/argo-cd/values.yaml argo-cd-release charts/argo-cd/ ```

``` kubectl get pods -l app.kubernetes.io/name=argocd-server -o name | cut -d'/' -f 2 ```

``` kubectl port-forward -n argocd svc/argo-cd-release-argocd-server 8000:80 ```

``` echo "Username: admin" ``` AND ``` echo "Password: $(kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d)" ```

``` kubectl apply -f root/root-app.yaml ```

``` kubectl apply -f root/root-appproject.yaml ```

``` argocd login $ARGOCD_SERVER --username $ARGOCD_USERNAME --password $ARGOCD_PASSWORD ```

``` argocd app sync root-app ```

``` kubectl delete -f root/root-app.yaml ```

``` helm delete -n argocd argo-cd-release ``` 

## Set bcrypt password to "password"
``` 
kubectl -n argocd patch secret argocd-secret   -p '{"stringData": {
"admin.password": "$2a$10$rRyBsGSHK6.uc8fntPwVIuLVHgsAhAX7TcdrqW/RADU0uh7CaChLa",
"admin.passwordMtime": "'$(date +%FT%T%Z)'"
}}' 
```
