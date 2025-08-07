# lokalni nastroje

- kubectl
- helm
- lens / freelens
- k3d / minikube / k0s

# Zakladni setup lokalniho prostredi

### k3d
```
k3d cluster create -s 3 -i rancher/k3s:v1.32.7-k3s1

k3d cluster create -s 3 -i harbor.smartdev.cz/public/ks3:v1.33.3-k3s1

helm uninstall traefik traefik-crd -n kube-system
```
- kubectl config / KUBECONFIG
- otestovat kubectl a helm
### ingress-nginx
```
helm install ingress-nginx ingress-nginx/ingress-nginx -n ingress-nginx --create-namespace
```
### cert-manager
```
helm install cert-manager jetstack/cert-manager --set crds.enabled=true -n cert-manager --create-namespace
```
 konfigurace pro letsencrypt
```
apiVersion: cert-manager.io/v1  
kind: ClusterIssuer  
metadata:  
  name: letsencrypt-prod  
spec:  
  acme:  
    server: https://acme-v02.api.letsencrypt.org/directory  
    email: admin@trigama.eu  
    privateKeySecretRef:  
      name: letsencrypt-prod-key
```

```
kubectl apply -f cert-manager-letsencrypt.yaml
```
### longhorn
```
helm install longhorn longhorn/longhorn -n longhorn-system --create-namespace
```

### Wordpress
```
helm install wp-test2 bitnami/wordpress -n wp-test2 --create-namespace
```
```
helm show values bitnami/wordpress
```

* ukazt konfiguraci s nginxem a certbotem
