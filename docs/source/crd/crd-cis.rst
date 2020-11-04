CRD - New CIS instance
======================

Best is to start with a warning ;)

.. warning::
   CRDs are, as of 11/04/2020, EA - and are for testing only.

.. warning::
   CRDs require the controller to run in "CRD" mode - so we'll delete the old instance and create a new CIS controller.

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

Check that we do not have any ingress service running - or any config map applied::

    ubuntu@kube-master:~/k8s/config-map$ kubectl get ingress
    No resources found in default namespace.

    ubuntu@kube-master:~/k8s/config-map$ kubectl get configmap
    No resources found in default namespace.



Double check on the BigIP, if config artefacte do still exist.


.. admonition:: Running CIS Instance

    We assume, that CIS controller from Chapter 3 / Container Ingress Service is still deployed!


* Change directory to /home/ubuntu/k8s/calico/CIS::

    cd /home/ubuntu/k8s/calico/CIS


* Delete the controller::

    ubuntu@kube-master:~/k8s/calico/CIS$ kubectl delete -f cis_deploy.yaml
    deployment.apps "k8s-bigip-ctlr-deployment" deleted

* Check if the controller POD is stopped::

    ubuntu@kube-master:~/k8s/calico/CIS$ kubectl get pods -n kube-system
    NAME                                       READY   STATUS    RESTARTS   AGE
    calico-kube-controllers-7567d8d9dd-x7dz9   1/1     Running   2          16h
    calico-node-2mdp2                          1/1     Running   2          16h
    calico-node-gmhbl                          1/1     Running   2          16h
    calico-node-zp9jh                          1/1     Running   2          16h
    coredns-66bff467f8-fdxkf                   1/1     Running   3          16h
    coredns-66bff467f8-s54hj                   1/1     Running   3          16h
    etcd-kube-master                           1/1     Running   3          16h
    kube-apiserver-kube-master                 1/1     Running   3          16h
    kube-controller-manager-kube-master        1/1     Running   3          16h
    kube-proxy-dwzxh                           1/1     Running   3          16h
    kube-proxy-wc5wz                           1/1     Running   2          16h
    kube-proxy-x8kp8                           1/1     Running   2          16h
    kube-scheduler-kube-master                 1/1     Running   3          16h


Now we can prepare the CRD config.

As said before - we need to deploy the controller with **--custom-resource-mode=true** argument.


* Change folder to /home/ubuntu/k8s/crd/CIS::

   cd /home/ubuntu/k8s/crd/CIS


* Deploy new CIS Controller::

   ubuntu@kube-master:~/k8s/crd/CIS$ kubectl apply -f cis_deploy.yaml
   deployment.apps/k8s-bigip-ctlr-deployment created

* Verify, that the controller is running::

   ubuntu@kube-master:~/k8s/crd/CIS$ kubectl get pods -n kube-system
   NAME                                         READY   STATUS    RESTARTS   AGE
   calico-kube-controllers-7567d8d9dd-x7dz9     1/1     Running   2          16h
   calico-node-2mdp2                            1/1     Running   2          16h
   calico-node-gmhbl                            1/1     Running   2          16h
   calico-node-zp9jh                            1/1     Running   2          16h
   coredns-66bff467f8-fdxkf                     1/1     Running   3          17h
   coredns-66bff467f8-s54hj                     1/1     Running   3          17h
   etcd-kube-master                             1/1     Running   3          17h
   k8s-bigip-ctlr-deployment-7f7c6bc7d8-jwgjl   1/1     Running   0          9s
   kube-apiserver-kube-master                   1/1     Running   3          17h
   kube-controller-manager-kube-master          1/1     Running   3          17h
   kube-proxy-dwzxh                             1/1     Running   3          17h
   kube-proxy-wc5wz                             1/1     Running   2          16h
   kube-proxy-x8kp8                             1/1     Running   2          16h
   kube-scheduler-kube-master   



.. toctree::
   :hidden:
   :caption: Chapter 5 - Custom Ressource Definition

   Introduction <crd/introduction>
   New CIS Instance <crd/crd-cis>
   Import CRD Definition <crd/crd-crd>
   Create Services <crd/crd-deploy>