Custom Ressource Definition - Introduction
==========================================

CRDs are the newest way to deploy services.
They just archieved general access - but still are quite new. New features will be added shortly. 
On the long run, CRDs might replace config maps (felxibility) while keeping a strucured appraoch as in *ingress* service.


What is a custom Ressource Definition
-------------------------------------

Definition from clouddocs.f5.com:

.. admonition:: What is a custom Ressource...

   * Custom resources are extensions of the Kubernetes API
   * A resource is an endpoint in the Kubernetes API that stores a collection of API objects. For example, the built-in pods resource contains a collection of Pod objects
   * A custom resource is an extension of the Kubernetes API that is not necessarily available in a default Kubernetes installation. It represents a customization of a particular Kubernetes installation. However, many core Kubernetes functions are now built using custom resources, making Kubernetes more modular
   * Custom resources can appear and disappear in a running cluster through dynamic registration, and cluster admins can update custom resources independently of the cluster itself. Once a custom resource is installed, users can create and access its objects using kubectl, just as they do for built-in resources like Pods
   * CIS supports the following Custom Resources:
      * VirtualServer (VirtualServer resource defines load balancing configuration for a **domain name**)
      * TLSProfile (TLSProfile is used to specify the TLS termination for a single/list of services in a VirtualServer Custom Resource. **TLS termination relies on SNI**)
      * TransportServer (The TransportServer resource exposes the **non-HTTP traffic** configuration for a virtual server address in BIG-IP)

   For an overview about supported parameters and a link to the schema file, please check here `here <https://clouddocs.f5.com/containers/latest/userguide/crd.html#id1>`_


.. warning::

   CRD are not working with config maps and Ingress - see notes below from clouddocs.f5.com:

   * --custom-resource-mode=true deploys CIS in Custom Resource Mode.
   
   * CIS does not watch for Ingress/Routes/ConfigMaps when deployed in CRD Mode.
   
   * CIS does not support combination of CRDs with any of Ingress/Routes and ConfigMaps.


.. toctree::
   :hidden:
   :caption: Chapter 5 - Custom Ressource Definition

   Introduction <crd/introduction>
   New CIS Instance <crd/crd-cis>
   Import CRD Definition <crd/crd-crd>
   Create Services <crd/crd-deploy>
   