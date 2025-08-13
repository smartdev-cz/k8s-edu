# lokalni nastroje

- kubectl
- helm
- lens / freelens
- k3d / minikube / k0s

# Zakladni setup

### Helm repozitare 

```
helm repo add bitnami https://charts.bitnami.com/bitnami                                            
helm repo add ingress-nginx https://kubernetes.github.io/ingress-nginx                                    
helm repo add openebs https://openebs.github.io/charts                                              
helm repo add camunda https://helm.camunda.io                                                       
helm repo add nfs-provisioner https://kubernetes-sigs.github.io/nfs-ganesha-server-and-external-provisioner/
helm repo add mailu https://mailu.github.io/helm-charts/                                          
helm repo add wiremind https://wiremind.github.io/wiremind-helm-charts                               
helm repo add gitlab https://charts.gitlab.io/                                                     
helm repo add jetstack https://charts.jetstack.io                                                    
helm repo add prometheus-community https://prometheus-community.github.io/helm-charts                            
helm repo add sentry https://sentry-kubernetes.github.io/charts                                    
helm repo add metrics-server https://kubernetes-sigs.github.io/metrics-server/                             
helm repo add vmware-tanzu https://vmware-tanzu.github.io/helm-charts                                    
helm repo add triliovault-operator http://charts.k8strilio.net/trilio-stable/k8s-triliovault-operator            
helm repo add minio https://charts.min.io/                                                        
helm repo add rancher-latest https://releases.rancher.com/server-charts/latest                             
helm repo add traefik https://traefik.github.io/charts                                              
helm repo add longhorn https://charts.longhorn.io                                                    
helm repo add metallb https://metallb.github.io/metallb                                             
helm repo add rancher-stable https://releases.rancher.com/server-charts/stable
```

### MetalLB
```
helm install metallb metallb/metallb -n metallb-system --create-namespace
```

### ingress-nginx
```
helm install ingress-nginx ingress-nginx/ingress-nginx -n ingress-nginx --create-namespace
```
### cert-manager
```
helm install cert-manager jetstack/cert-manager --set crds.enabled=true -n cert-manager --create-namespace
```

### longhorn
```
helm install longhorn longhorn/longhorn -n longhorn-system --create-namespace
```

### Wordpress (testovaci appka)
```
helm install wp-test2 bitnami/wordpress -n wp-test2 --create-namespace
```

### Konfigurace certbota pro PROD Letsencrypt
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

### Konfigurace MetalLB
```
apiVersion: metallb.io/v1beta1
kind: IPAddressPool
metadata:
  name: pool
  namespace: metallb-system
spec:
  addresses:
  - xxx.xxx.xxx.xxx/xx
```

```
kubectl apply -f metallb.yaml
```

### Ziskani values z helm chartu
```
helm show values harbor/harbor > values.yaml
```

values file pak jde vyuzit pri instalaci nebo upgrade

```
helm upgrade harbor harbor/harbor -n harbor --install --create-namespace -v values.yaml
```
