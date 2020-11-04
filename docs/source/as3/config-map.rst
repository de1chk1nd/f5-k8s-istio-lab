AS3 -- Config Maps
==================

In the previous chapter, we looked at deploying *simple* ingress service (from a definition point of view).
Now we'll have a look into config maps / as3.

Using this method, we allow a lot of more flexibility, as we allow AS3 definitions. The drawback is an increase of config-complexity.

First and foremost update to current github repository (if not already done)::

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

* First change folder to  /home/ubuntu/k8s/apps::

   cd /home/ubuntu/k8s/apps



.. toctree::
   :hidden:
   :caption: Chapter 4 - AS3 / Config-Map

   Introduction <as3/introduction>
   Config Map <as3/config-map>