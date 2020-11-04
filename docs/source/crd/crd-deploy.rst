Deploy Apps
-----------

* Change folder to /home/ubuntu/k8s/crd::

    cd /home/ubuntu/k8s/crd


* Deploy *simple_http.yaml* Service::

    ubuntu@ip-10-1-1-4:~/k8s/crd$ kubectl apply -f 004a_crd_simple_http.yaml
    virtualserver.cis.f5.com/tea-virtual-server created

dsd

Check Service in k8s::

   ubuntu@ip-10-1-1-4:~/k8s/crd$ kubectl get VirtualServer
   NAME                 AGE
   tea-virtual-server   93s


.. toctree::
   :hidden:
   :caption: Chapter 5 - Custom Ressource Definition

   Introduction <crd/introduction>
   New CIS Instance <crd/crd-cis>
   Import CRD Definition <crd/crd-crd>
   Create Services <crd/crd-deploy>