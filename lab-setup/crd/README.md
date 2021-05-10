# f5-k8s-istio-lab

Please find a lab overview and guide on readthedocs

https://f5-k8s-istio-lab.readthedocs.io/en/latest/

The lab is based on UDF blueprint: "f5 k8s istio lab"

# Set Up CIS

kubectl create secret generic bigip-login -n kube-system --from-literal=username=admin --from-literal=password=<password>

kubectl create serviceaccount bigip-ctlr -n kube-system

kubectl apply -f  /home/ubuntu/k8s/crd/CIS/k8s_rbac.yaml

kubectl create -f /home/ubuntu/k8s/crd/CIS/customresourcedefinitions.yaml -n kube-system

Either (ClusterIP -> Overlay  Network w calico),

a) kubectl apply -f  /home/ubuntu/k8s/crd/CIS/cis_deploy.yaml

or (NodePort -> NodePort mode),

b) kubectl apply -f  /home/ubuntu/k8s/crd/CIS/cis_deploy-nodeport.yaml


# Deploy Apps

Either (ClusterIP -> Overlay  Network w calico),

kubectl apply -f  /home/ubuntu/k8s/apps/coffee-1.yaml
kubectl apply -f  /home/ubuntu/k8s/apps/tea-1.yaml

or (NodePort -> NodePort mode),

kubectl apply -f  /home/ubuntu/k8s/apps/coffee-1-nodeport.yaml
kubectl apply -f  /home/ubuntu/k8s/apps/tea-1-nodeport.yaml


# CRD Deployment

Install  certificates:
======================

kubectl apply -f /home/ubuntu/k8s/crd/cert-client.yaml
kubectl apply -f /home/ubuntu/k8s/crd/cert-server.yaml

Deploy TLS Profile:
===================

Either (ClusterIP -> Overlay  Network w calico),

EDGE: t.b.d.
Re-Encrypt: t.b.d.

or (NodePort -> NodePort mode),

EDGE:
kubectl apply -f /home/ubuntu/k8s/crd/TLSprofile-edge.yaml

Re-Encrypt:
kubectl apply -f /home/ubuntu/k8s/crd/TLSprofile-reencrypt.yaml


Deploy VirtualServer:
=====================

Either (ClusterIP -> Overlay  Network w calico),
t.b.d.

or (NodePort -> NodePort mode),
kubectl apply -f /home/ubuntu/k8s/crd/simple_https-reencrypt.yaml


