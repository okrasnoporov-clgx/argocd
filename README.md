# ArgoCD repo


installation:
kubectl create namespace argocd

kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml

error in Minikube:
The CustomResourceDefinition "applicationsets.argoproj.io" is invalid: metadata.annotations: Too long: may not be more than 262144 bytes

to resolve:
kubectl apply --server-side -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/crds/applicationset-crd.yaml

customresourcedefinition.apiextensions.k8s.io/applicationsets.argoproj.io serverside-applied


kubectl get pods -n argocd
NAME                                                READY   STATUS    RESTARTS   AGE
argocd-application-controller-0                     1/1     Running   0          2m16s
argocd-applicationset-controller-79bbd8c9cd-jth22   1/1     Running   0          2m16s
argocd-dex-server-6cdf75744-5l7ts                   1/1     Running   0          2m16s
argocd-notifications-controller-65878667c-cnvdr     1/1     Running   0          2m16s
argocd-redis-5f664b9b9c-8j8pl                       1/1     Running   0          2m16s
argocd-repo-server-7f58d7cdf7-bv6mc                 1/1     Running   0          2m16s
argocd-server-6ccd556fc9-lgl9l                      1/1     Running   0          2m16s

CLI
Invoke-WebRequest -Uri "https://github.com/argoproj/argo-cd/releases/latest/download/argocd-windows-amd64.exe" -OutFile "C:\tools\argocd.exe"

argocd version --client
argocd: v3.5.2+e258ee2
  BuildDate: 2026-08-27T09:34:36Z
  GitCommit: e258ee23c3e52266d407572f4bcdfe7d9ed36cb5
  GitTreeState: clean
  GoVersion: go1.26.4
  Compiler: gc
  Platform: windows/amd64

kubectl port-forward svc/argocd-server -n argocd 8080:443

Get password:

$encoded = kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}"
[System.Text.Encoding]::UTF8.GetString([System.Convert]::FromBase64String($encoded))
