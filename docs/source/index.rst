Kubernetes Training Lab
=======================

**Guide is still work in progress.**
**Most parts are already covered - but more testing and review is required (plus content for the istio lab)**

UDF      : k8s training - calico/CIS/CRD/istio (incl. lab guide)

github   : https://github.com/de1chk1nd/f5-k8s-istio-lab


Welcome to my Lab Guide for integrating F5 Container Ingress Services in kubernetes (integration into the overlay network via calico).

**Purpose:** This lab is for getting familiar with-, and test, basic kubernetes ingress services and to start working with istio service mesh.
All from a f5 point of view (bigip CIS).

The lab (UDF) has following basic set up:

========  ========  ===========  ===========
 Device    IP MGMT   IP ext.      IP int.
========  ========  ===========  ===========
 bigip    10.1.1.4  10.1.10.5    10.1.20.5
 master   10.1.1.5  n/a          10.1.20.20
worker-1  10.1.1.6  n/a          10.1.20.21
worker-2  10.1.1.7  n/a          10.1.20.22
jumphost  10.1.1.8  n/a          10.1.20.200
client    10.1.1.9  10.1.10.200  n/a
========  ========  ===========  ===========

*Since MGMT IP is required by the lab network, but not really used in our example, it will be ignored*


.. image:: images/overview.png
   :width: 400
   :alt: Lab Overview
   :align: center


The lab currently runs on:

* TMOS 15.1.1
   * AS3 3.23.0-5

* Ubuntu 18.04
   * kubernetes v1.18.10

The infrastructure is set up (VLANs and IPs) and basic kubernetes cluster installation is completed.
Calico package (incl. calicoctl) is deployed - but not yet configured.
kubernetes partition was created in bigip (required for CIS).


.. warning::
   
   Since it is important for initilazing the calico sdn, please be aware, that *kubadm init* was initialized with *"--pod-network-cidr=192.168.0.0/16"*


If you want to set up the lab locally, you can still use the lab guide. Just prepare a kubernetes cluster and a f5. 
Just adjust IP Adresses accordingly to meet you local lab.

**Another option** to build a local lab, is to use the installation guide Nicola Mennant wrote on Dev Central.
Part-1 focuses on the basic infrastrucure - part-2 focuses on the CIS service itself. 
If you want to stick with this lab here guide, and not the one from Nicolas, you'll jusst need to work yourself thorugh part 1 and than get back to continue with this lab.

* `F5 & Calico Part I <https://devcentral.f5.com/s/articles/CIS-and-Kubernetes-Part-1-Install-Kubernetes-and-Calico>`_
* `F5 & Calico Part II <https://devcentral.f5.com/s/articles/CIS-and-Kubernetes-Part-2-Install-F5-Container-ingress-services>`_


From that point on, the infrastrucure needs to be build, like:
* Creating/configuring the overlay network
* Create Apps/Deployments in kubernetes
* Create the CIS controller

This guide is seperated into several chapters:

* **Chapter 1** focuses on basic information about the lab, kubernetes, calico and so on.

* **Chapter 2** shows the BGP configuration requried on kubernetes and f5 bigip

* **Chapter 3** installs basic ingress services

* **Chapter 4** shows AS3 config map integration

* **Chapter 5** shows the newest feature called *Custom Ressource Definition*

* **Chapter 6** showcases ISTIO


.. warning::
   
   Chapter 2 sets up the BGP and is mandatory to succeed in chapter 3 - 5!


**Please use the menu on the left, to jump to the desired chapter**


.. toctree::
   :hidden:
   :caption: Chapter 1 - Information

   Introduction <learning/introduction>
   Calico <learning/calico>
   ISTIO <learning/istio>


.. toctree::
   :hidden:
   :caption: Chapter 2 - set up BGP

   Introduction <BGP/introduction>
   Calico - BGP <BGP/calico-bgp>
   F5 BigIP - BGP <BGP/bigip-bgp>
   BGP - Verification <BGP/bgp-verify>


.. toctree::
   :hidden:
   :caption: Chapter 3 - Ingress Service

   Introduction <k8s-ingress/introduction>
   Container Ingress Service <k8s-ingress/cis>
   Basic Ingress <k8s-ingress/basic-ingress>
   Basic Ingress - TLS <k8s-ingress/basic-ingress-tls>
   Basic Ingress - L7 Routing <k8s-ingress/basic-ingress-l7-route>

.. toctree::
   :hidden:
   :caption: Chapter 4 - AS3 / Config-Map

   Introduction <as3/introduction>
   Config Map <as3/config-map>

.. toctree::
   :hidden:
   :caption: Chapter 5 - Custom Ressource Definition

   Introduction <crd/introduction>
   New CIS Instance <crd/crd-cis>
   Import CRD Definition <crd/crd-crd>
   Create CRD Services <crd/crd-deploy>

.. toctree::
   :hidden:
   :caption: Chapter 6 - istio
   
   Introduction <istio/introduction>