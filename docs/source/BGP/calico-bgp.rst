.. raw:: html

   <style> .red {color:red}; font-weight:bold </style>

.. role:: red


.. raw:: html

   <style> .blue {color:blue}; font-weight:bold </style>

.. role:: blue


Calico BGP Set Up
=================

Preparation
+++++++++++

**From kubernetes master (10.1.20.20)**

First and foremost update to current github repository. 
Within the the *root* folder of the current user ("ubuntu"), I stored a script to download the current repo from git

Please run the "update_repo" script::

  /home/ubuntu/update_repo.sh

| 
| Output will look like:

ubuntu@kube-master:~$ :red:`/home/ubuntu/update_repo.sh`
:blue:`A    k8s
| A    k8s/apps
| A    k8s/apps/README.md
| A    k8s/calico
| A    k8s/calico/README.md
| A    k8s/calico/calicoctl
| A    k8s/calico/calicoctl/BGPConfiguration
| A    k8s/calico/calicoctl/BGPPeer
| A    k8s/istio
| A    k8s/istio/README.md
| Exported revision 54.`

The lenght of the list may vary, depending on the amout of scripts/files downloaded.


Start BGP Set Up
++++++++++++++++

You need to apply the BGP config from *BGPConfiguration* and also *BGPPeer* to set up the BGP config in k8s::

  # change folder to /home/ubuntu/k8s/calico/calicoctl::
  cd /home/ubuntu/k8s/calico/calicoctl

You can check the local config files via "ls" and "cat".
When finished, deplyo the BGP configuration::

  # Deploy BGP Config
  calicoctl create -f /home/ubuntu/k8s/calico/calicoctl/BGPConfiguration
   
  # Deploy BGP- :red:`Peer Configuration`
  calicoctl create -f /home/ubuntu/k8s/calico/calicoctl/BGPPeer

See :download:`Example Code on github <https://github.com/de1chk1nd/f5-k8s-istio-lab/tree/main/lab-setup/calico/calicoctl>`


The output should be similar to this::

  ubuntu@kube-master:~/k8s/calico/calicoctl$ calicoctl create -f /home/ubuntu/k8s/calico/calicoctl/BGPConfiguration
  Successfully created 1 'BGPConfiguration' resource(s)

  ubuntu@kube-master:~/k8s/calico/calicoctl$ calicoctl create -f /home/ubuntu/k8s/calico/calicoctl/BGPPeer
  Successfully created 1 'BGPPeer' resource


.. toctree::
   :numbered:
   :hidden:
   :caption: Chapter 2 - set up BGP

   Introduction <BGP/introduction>
   Calico - BGP <BGP/calico-bgp>
   F5 BigIP - BGP <BGP/bigip-bgp>
   BGP - Verification <BGP/bgp-verify>