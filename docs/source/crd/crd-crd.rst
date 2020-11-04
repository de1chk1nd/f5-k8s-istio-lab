CRD Import
==========


Once the controller is installed, we import the CRD definition.


Change folder to /home/ubuntu/k8s/crd::

   cd /home/ubuntu/k8s/crd


Take a look at the config file *customresourcedefinitions.yaml*. 

Deploy the config::

   ubuntu@kube-master:~/k8s/crd$ kubectl apply -f customresourcedefinitions.yaml
   customresourcedefinition.apiextensions.k8s.io/virtualservers.cis.f5.com created
   customresourcedefinition.apiextensions.k8s.io/tlsprofiles.cis.f5.com created
   customresourcedefinition.apiextensions.k8s.io/transportservers.cis.f5.com created


.. toctree::
   :hidden:
   :caption: Chapter 5 - Custom Ressource Definition

   Introduction <crd/introduction>
   New CIS Instance <crd/crd-cis>
   Import CRD Definition <crd/crd-crd>
   Create Services <crd/crd-deploy>