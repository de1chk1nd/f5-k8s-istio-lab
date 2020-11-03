Calico BGP Set Up
=================

Login to kube-master and change to folder: **/home/ubuntu/k8s/calico/calicoctl**

You need to apply the BGP config from *BGPConfiguration* and also *BGPPeer* to set up the BGP config in k8s::

   #change folder to /home/ubuntu/k8s/calico/calicoctl
   imish

   #Switch to enable mode
   enable

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