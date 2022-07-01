# K3s cluster setup

### Cluster setup command
Node 01
```
curl -sfL https://get.k3s.io | K3S_KUBECONFIG_MODE="644" sh -s server --cluster-init --node-ip 10.10.9.10
```

Get token from, cat /var/lib/rancher/k3s/server/node-token

Node 02
```
curl -sfL https://get.k3s.io | K3S_KUBECONFIG_MODE="644" K3S_TOKEN=<> sh -s - server --server https://10.10.9.10:6443 --node-ip 10.10.9.11
```

Node 02
```
curl -sfL https://get.k3s.io | K3S_KUBECONFIG_MODE="644" K3S_TOKEN=<> sh -s - server --server https://10.10.9.10:6443 --node-ip 10.10.9.12
```
