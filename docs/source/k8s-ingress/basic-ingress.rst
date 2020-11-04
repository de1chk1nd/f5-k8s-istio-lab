Ingress
=======

Install Service / App::

    kubectl apply -f k8s/apps/coffee-1.yaml

    ubuntu@kube-master:~$ kubectl get pods
    NAME                      READY   STATUS    RESTARTS   AGE
    coffee-5f56ff9788-fp89s   1/1     Running   0          7s
    coffee-5f56ff9788-z8pqx   1/1     Running   0          7s

Install Ingress::

    kubectl apply -f k8s/basic-ingress/ingress-coffee-1.yaml


Check configuration on bigip:

.. image:: ../images/basic-ingress-coffee.PNG
   :width: 400
   :alt: Lab Overview
   :align: center

Ingress Service created on F5.

.. toctree::
   :maxdepth: 2