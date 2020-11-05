Getting started with BGP
========================

The following labs describe how to set up BGP in Calico and also how to use the imish to set up BGP in f5 tmos/imish.

This set up is **mandatory** to continue adding services (this *"adds"* the f5 to the SDN of the kubernetes cluster).

Another option might be the implementation via NodePort (not part of this lab - as this set up is not as *sophisticated* as Cluster IP set up, and maybe as often seen in prod environments).
Future releases will allow ServiceType *LoadBalancer* - but again - this is not part of this lab.

To get more info about integrating f5 bigip with kubernetes, please have a look into our deployment guide on :ref:`clouddocs <https://clouddocs.f5.com/containers/latest/userguide/what-is.html>` and check the deployment options.


.. toctree::
   :numbered:
   :hidden:
   :caption: Chapter 2 - set up BGP

   Introduction <BGP/introduction>
   Calico - BGP <BGP/calico-bgp>
   F5 BigIP - BGP <BGP/bigip-bgp>
   BGP - Verification <BGP/bgp-verify>