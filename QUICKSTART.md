# Quickstart

## Create namespaces
kubectl create ns dev1
kubectl create ns dev2
kubectl create ns qa
kubectl create ns prod

## Apply overlays directly (optional test)
kubectl apply -k apps/dummy-car/overlays/dev1
kubectl apply -k apps/dummy-car/overlays/dev2
kubectl apply -k apps/dummy-car/overlays/qa
kubectl apply -k apps/dummy-car/overlays/prod

## Test URLs
http://k8s-ingressn-albtongi-dbafdf282d-728769480.us-east-1.elb.amazonaws.com/dev1/app
http://k8s-ingressn-albtongi-dbafdf282d-728769480.us-east-1.elb.amazonaws.com/dev2/app
http://k8s-ingressn-albtongi-dbafdf282d-728769480.us-east-1.elb.amazonaws.com/qa/app
http://k8s-ingressn-albtongi-dbafdf282d-728769480.us-east-1.elb.amazonaws.com/prod/app

## Enable ArgoCD GitOps
kubectl apply -f argocd/applications/

## CI/CD
In repo `dummy-car-app`, add Actions secret `GITOPS_PAT` (write access to tbhuvaneswar/car-gitops).
Push to main -> builds/pushes image -> updates overlay image tags -> ArgoCD auto-sync deploys.
