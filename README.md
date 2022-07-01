# K3s cluster setup

### Cluster setup
```
vagrant up
```

### Install Nginx ingress
```
export KUBECONFIG=/etc/rancher/k3s/k3s.yaml
helm repo add nginx-stable https://helm.nginx.com/stable 
helm install nginx-ingress nginx-stable/nginx-ingress \
--set controller.hostNetwork=true
```

### Install Grafana
```
helm repo add bitnami https://charts.bitnami.com/bitnami
helm install grafana bitnami/grafana
```