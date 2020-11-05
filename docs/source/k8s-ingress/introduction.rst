Introduction - Ingress Services
===============================

Now we're going to set up basic ingress services.

.. warning::
   
   You have to set up the BGP routing from the previous chapter. If not, bigip will not be able to access the apps (POD IPs).

We'll keep this basic and set up basic http and https service. Please work yourself through, as desired (choose what is interesting).

More example config and an detailed explanation about supported "attributes" (annotations), can be found on clouddocs.


.. toctree::
   :numbered:
   :hidden:
   :caption: Chapter 3 - Ingress Service

   Introduction <k8s-ingress/introduction>
   Container Ingress Service <k8s-ingress/cis>
   Basic Ingress <k8s-ingress/basic-ingress>
   Basic Ingress - TLS <k8s-ingress/basic-ingress-tls>
   Basic Ingress - L7 Routing <k8s-ingress/basic-ingress-l7-route>