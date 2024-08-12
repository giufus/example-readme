
## EXAMPLE README from Axum

- cargo build --release
- docker buildx build --push --platform=linux/amd64,linux/arm64 . -t giufus/axum-example-readme

### create a k8s cluster 
- kind create cluster --name=example 
- kubectl config get-contexts
- kubectl config use-context example
- kubectl create namespace dev-example-readme

### deployments
- k create deployment example-readme --image giufus/axum-example-readme:latest --port 3000 --replicas 2 -n dev-example-readme --dry-run=client -oyaml  > k8s/example-readme-deployment.yaml
- k apply -f k8s/example-readme-deployment.yaml

## service
- kubectl expose deployment example-readme --type=ClusterIP --port=80 --target-port=3000 -n dev-example-readme --dry-run=client -oyaml  > k8s/example-readme-service.yaml
- k apply -f k8s/example-readme-service.yaml

# ingress
- minikube addons enable ingress
- kubectl get pods -n ingress-nginx
- k create ingress example-readme --dry-run=client -oyaml -n dev-example-readme > k8s/example-readme-ingress.yaml
- k apply -f k8s/example-readme-ingress.yaml
```

```
