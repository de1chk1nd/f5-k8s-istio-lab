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







   #Enter configuration mode
   config terminal
   #Setup route bgp with AS Number 64512
   router bgp 64512

   #Create BGP Peer group
   neighbor calico-k8s peer-group

   #assign peer group as BGP neighbors
   neighbor calico-k8s remote-as 64512

   #we need to add all the peers: the other BIG-IP, our k8s components
   neighbor 10.1.20.20 peer-group calico-k8s
   neighbor 10.1.20.21 peer-group calico-k8s
   neighbor 10.1.20.22 peer-group calico-k8s

   #save configuration
   write

   #exit
   end




...on k8s
+++++++++

Login to :blue:`k8s master (10.1.20.20)`

Copy and paste the text below::

    cat << EOF | calicoctl create -f -
     apiVersion: projectcalico.org/v3
     kind: BGPConfiguration
     metadata:
       name: default
     spec:
       logSeverityScreen: Info
       nodeToNodeMeshEnabled: true
       asNumber: 64512
    EOF

    cat << EOF | calicoctl create -f -
    apiVersion: projectcalico.org/v3
    kind: BGPPeer
    metadata:
      name: bgppeer-global-bigip1
    spec:
      peerIP: 10.1.20.5
      asNumber: 64512
    EOF

See :download:`Example Code on github <https://github.com/de1chk1nd/F5k8sCalicoLab/blob/main/BGP/calico_bgp.txt>`



.. toctree::
   :numbered:
   :hidden:
   :caption: Chapter 2 - kubernetes ingress

   Introduction <k8s-ingress/introduction>
   Calico - BGP <k8s-ingress/calico-bgp>
   F5 BigIP - BGP <k8s-ingress/bigip-bgp>
   BGP - Verification <k8s-ingress/bgp-verify>