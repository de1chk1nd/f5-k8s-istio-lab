Container Ingress Service
=========================

========  ========  ==========
 Device   Username   Password
========  ========  ==========
 bigip     admin    f5twister!
========  ========  ==========


* First change folder to XXX::

   cd /r

* Create BigIP Login::
   
   kubectl create secret generic bigip-login -n kube-system --from-literal=username=admin --from-literal=password=f5twister!

* Create a service account for deploying CIS::

   kubectl create serviceaccount k8s-bigip-ctlr -n kube-system

* Create a Cluster Role and Cluster Role Binding on the Kubernetes Cluster using the examples below::

   kubectl apply -f  k8s_rbac.yaml

* Create a CIS deployment using cis_deploy.yaml as shown below::

   kubectl apply -f  cis_deploy.yaml





.. toctree::
   :maxdepth: 2