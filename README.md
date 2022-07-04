# K3s cluster setup

### Cluster setup
```
vagrant up
```

### Install Nginx ingress
```
vagrant ssh node-01
export KUBECONFIG=/etc/rancher/k3s/k3s.yaml
helm repo add nginx-stable https://helm.nginx.com/stable 
helm install nginx-ingress nginx-stable/nginx-ingress \
--set controller.hostNetwork=true \
--set controller.setAsDefaultIngress=true
```

### Install Grafana
```
vagrant ssh node-01
export KUBECONFIG=/etc/rancher/k3s/k3s.yaml
helm repo add bitnami https://charts.bitnami.com/bitnami
helm install grafana bitnami/grafana
```

### Install sample app
```
vagrant ssh node-01
kubectl appy -f /vagrant/sample-app.yaml
```
