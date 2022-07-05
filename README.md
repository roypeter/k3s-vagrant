# K3s cluster setup
Vagrant file automates following tasks
- Setup 3 node etcd HA cluster
- Install Nginx ingress
- Run a sample demo app with deployment, service and ingress

## Cluster startup
```
# Bring up the Vagrant nodes
vagrant up

# Add vm ip to hosts /etc/hosts
echo '10.10.9.10 foo.bar.com' | sudo tee -a /etc/hosts

# Open below url in your browser
http://foo.bar.com/
```
