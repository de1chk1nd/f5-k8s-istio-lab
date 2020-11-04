Container Ingress Service
=========================

========  ========  ==========
 Device   Username   Password
========  ========  ==========
 bigip     admin    f5twister!
========  ========  ==========


* First change folder to  k8s/calico/CIS/::

   cd k8s/calico/CIS/


* Create BigIP Login::
   
   kubectl create secret generic bigip-login -n kube-system --from-literal=username=admin --from-literal=password=f5twister!


* Create a service account for deploying CIS::

   kubectl create serviceaccount bigip-ctlr -n kube-system


* Create a Cluster Role and Cluster Role Binding on the Kubernetes Cluster using the examples below::

   kubectl apply -f  k8s_rbac.yaml


* Create a CIS deployment using cis_deploy.yaml as shown below::

   kubectl apply -f  cis_deploy.yaml


.. toctree::
   :numbered:
   :hidden:
   :caption: Chapter 3 - Ingress Service

   Introduction <k8s-ingress/introduction>
   Calico - BGP <k8s-ingress/cis>
   F5 BigIP - BGP <k8s-ingress/basic-ingress>