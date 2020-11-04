Deploy Apps
-----------

* Change folder to /home/ubuntu/k8s/crd::

    cd /home/ubuntu/k8s/crd


Simple HTTP Service
+++++++++++++++++++

* Deploy *simple_http.yaml* Service::

    ubuntu@kube-master:~/k8s/crd$ kubectl apply -f simple_http.yaml
    virtualserver.cis.f5.com/cafe-virtual-server created


* Verify if the service is running::

    ubuntu@kube-master:~/k8s/crd$ kubectl get virtualserver
    NAME                  AGE
    cafe-virtual-server   10s


Now check if the CRD is applied to the bigip successfully.

Virtual Server:

.. image:: ../images/crd-vs.PNG
   :width: 400
   :alt: Lab Overview
   :align: center


LTM Policy:

.. image:: ../images/crd-LTMpol.PNG
   :width: 400
   :alt: Lab Overview
   :align: center


and Pool-Member:

.. image:: ../images/crd-pool.PNG
   :width: 400
   :alt: Lab Overview
   :align: center


* Now delete the service again::

    ubuntu@kube-master:~/k8s/crd$ kubectl delete virtualserver cafe-virtual-server
    virtualserver.cis.f5.com "cafe-virtual-server" deleted



Simple HTTPs Service
++++++++++++++++++++

* Deploy *TLSprofile.yaml* Service::

    ubuntu@kube-master:~/k8s/crd$ kubectl apply -f TLSprofile.yaml


* Deploy *simple_https.yaml* Service::

    ubuntu@kube-master:~/k8s/crd$ kubectl apply -f simple_https.yaml




.. toctree::
   :hidden:
   :caption: Chapter 5 - Custom Ressource Definition

   Introduction <crd/introduction>
   New CIS Instance <crd/crd-cis>
   Import CRD Definition <crd/crd-crd>
   Create Services <crd/crd-deploy>