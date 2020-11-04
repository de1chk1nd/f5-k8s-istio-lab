Basic Ingress Service - TLS
===========================

In this chapter we'll create basic ingress service - TLS encrypted to the client.

For this, we'll add another application (named **tea**) and add a second ingress service. We'll discover how to add certificate information to the service:
* by referencing a local certificate/ssl profile
* by adding a certificate from the k8s secret store

First, we'll add the application.

* Change to the app folder (/home/ubuntu/k8s/apps)::

   cd /home/ubuntu/k8s/apps


* Deploy the Application **tea-1** app & service::

   ubuntu@kube-master:~/k8s/apps$ kubectl apply -f tea-1.yaml
   deployment.apps/tea created
   service/tea-svc created


Now we can deploy the ingress service.





.. toctree::
   :numbered:
   :hidden:
   :caption: Chapter 3 - Ingress Service

   Introduction <k8s-ingress/introduction>
   Container Ingress Service <k8s-ingress/cis>
   Basic Ingress <k8s-ingress/basic-ingress>
   Basic Ingress - TLS <k8s-ingress/basic-ingress-tls>
   