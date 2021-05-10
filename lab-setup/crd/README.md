# f5-k8s-istio-lab

Please find a lab overview and guide on readthedocs

https://f5-k8s-istio-lab.readthedocs.io/en/latest/

The lab is based on UDF blueprint: "f5 k8s istio lab"

# Set Up CIS

kubectl create secret generic bigip-login -n kube-system --from-literal=username=admin --from-literal=password=<password>

kubectl create serviceaccount bigip-ctlr -n kube-system

kubectl apply -f  /home/ubuntu/k8s/crd/CIS/k8s_rbac.yaml

kubectl create -f /home/ubuntu/k8s/crd/CIS/customresourcedefinitions.yaml -n kube-system

kubectl apply -f  /home/ubuntu/k8s/crd/CIS/cis_deploy.yaml