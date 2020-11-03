Kubernetes Training Lab
=======================

Welcome to my Lab Guide for integrating F5 Container Ingress Services with k8s and Calico as CNI.

The lab has following basic set up:

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

*Since MGMT IP is required by the lab by default, but not used in the lab, it will be ignored*

.. image:: images/overview.png
   :width: 400
   :alt: Lab Overview
   :align: center



WIP


.. toctree::
   :numbered:
   :maxdepth: 2
   :caption: Introduction & Pre-Reading
   Welcome <index>

.. toctree::
   :numbered:
   :maxdepth: 2
   :caption: Setting up the lab

.. toctree::
   :numbered:
   :maxdepth: 2
   :caption: Deploy Services