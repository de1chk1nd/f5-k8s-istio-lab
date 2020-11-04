Deploy Apps
-----------

* Change folder to /home/ubuntu/k8s/crd::

    cd /home/ubuntu/k8s/crd


* Deploy *simple_http.yaml* Service::

    ubuntu@kube-master:~/k8s/crd$ kubectl apply -f simple_http.yaml
    virtualserver.cis.f5.com/cafe-virtual-server created


* Verify if the service is running::

    ubuntu@kube-master:~/k8s/crd$ kubectl get virtualserver
    NAME                  AGE
    cafe-virtual-server   10s


Now check if the CRD is applied to the bigip successfully.


 

.. toctree::
   :hidden:
   :caption: Chapter 5 - Custom Ressource Definition

   Introduction <crd/introduction>
   New CIS Instance <crd/crd-cis>
   Import CRD Definition <crd/crd-crd>
   Create Services <crd/crd-deploy>