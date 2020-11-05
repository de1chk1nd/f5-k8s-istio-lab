Welcome
=======

Welcome the the first chapter *learning & pre reading*

The following sections provide generic information about the lab and different technologies used.

The lab set up in the beginning is very basic. Different components (like calico, services, ...) need to be deplyoed.

Everything important is stored on github:  `github repo <https://github.com/de1chk1nd/f5-k8s-istio-lab>`_

Lab related content is stored in the **lab-setup** folder. Detailed explanation will be provided in the labs later on.


F5 BigIP
--------

F5 BigIP is more or less in default set up. VLANs and VLAN Network IPs were assigned. Current Supported AS3 version is installed.

Current installed license supports:

* LTM
* Routing Bundle
* APM
* aWAF

**kubernetes partition was added - this one is requried by the CIS controller**


Kubernetes Master & Worker Nodes
--------------------------------

Kubernetes Nodes were installed with ubuntu 18.04 server. 

Packet repository and disstribution packages were updated.

Finally current supported docker & kubernetes packages were installed a basic kubernetes cluster was set up.



Windows Jumphost
----------------

Windows 10 basic OS with Google Chrome.


Windows Client
--------------

Windows 10 basic OS with Google Chrome.

**When CIS Services are deployed, the tests to access the service can be done from this jump host. Please test manually, and on a case by case base, if requreds


.. toctree::
   :hidden:
   :maxdepth: 1
   :caption: Chapter 1 - Information

   Introduction <learning/introduction>
   Calico <learning/calico>
   ISTIO <learning/istio>