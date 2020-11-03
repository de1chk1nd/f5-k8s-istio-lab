Calico BGP Set Up
=================

Login to kube-master via ssh.

First and foremost update to current github repository::

  ubuntu@kube-master:~$ /home/ubuntu/update_repo.sh
  A    k8s
  A    k8s/apps
  A    k8s/apps/README.md
  A    k8s/calico
  A    k8s/calico/README.md
  A    k8s/calico/calicoctl
  A    k8s/calico/calicoctl/BGPConfiguration
  A    k8s/calico/calicoctl/BGPPeer
  A    k8s/istio
  A    k8s/istio/README.md
  Exported revision 54.


The lenght of the list may vary, depending on the amout of scripts/files downloaded.

You need to apply the BGP config from *BGPConfiguration* and also *BGPPeer* to set up the BGP config in k8s::

   #change folder to /home/ubuntu/k8s/calico/calicoctl
   cd /home/ubuntu/k8s/calico/calicoctl

   #copy & paste the config from BGPConfiguration into the CLI
   cat BGPConfiguration
   
   #copy & paste the config from BGPPeer into the CLI
   cat BGPPeer

See :download:`Example Code on github <https://github.com/de1chk1nd/f5-k8s-istio-lab/tree/main/lab-setup/calico/calicoctl>`


The output should be similar to this::

  ubuntu@kube-master:~$ cat << EOF | calicoctl create -f -
  >  apiVersion: projectcalico.org/v3
  >  kind: BGPConfiguration
  >  metadata:
  >    name: default
  >  spec:
  >    logSeverityScreen: Info
  >    nodeToNodeMeshEnabled: true
  >    asNumber: 64512
  > EOF
  Successfully created 1 'BGPConfiguration' resource(s)

  ubuntu@kube-master:~$ cat << EOF | calicoctl create -f -
  > apiVersion: projectcalico.org/v3
  > kind: BGPPeer
  > metadata:
  >   name: bgppeer-global-bigip1
  > spec:
  >   peerIP: 10.1.20.5
  >   asNumber: 64512
  > EOF
  Successfully created 1 'BGPPeer' resource(s)






.. toctree::
   :numbered:
   :hidden:
   :caption: Chapter 2 - kubernetes ingress

   Introduction <k8s-ingress/introduction>
   Calico - BGP <k8s-ingress/calico-bgp>
   F5 BigIP - BGP <k8s-ingress/bigip-bgp>
   BGP - Verification <k8s-ingress/bgp-verify>