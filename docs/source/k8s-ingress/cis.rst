Container Ingress Service
=========================

Before we starting and creating services, we need to set up the CIS controller.

For later use, I'll post the login info, which is required on the controller to be able to login to the bigip.

========  ========  ==========
 Device   Username   Password
========  ========  ==========
 bigip     admin    f5twister!
========  ========  ==========

**From kubernetes master (10.1.20.20)**

First, and foremost, **update local github repository** (if not already done in a previous chapter)::

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


* change folder to k8s/calico/CIS/::

   cd k8s/calico/CIS/


Now we create the login of the BigIP. 
Since we do not want to store this sensible information in a raw config file, we add the login to a secret.
To get  to know more about k8s secrets, please go :ref:`here <https://kubernetes.io/docs/concepts/configuration/secret/>`.


* Create BigIP Login::
   
   kubectl create secret generic bigip-login -n kube-system --from-literal=username=admin --from-literal=password=f5twister!


|
|
Once this is done, we set up the RBAC. 
Basically we create a role and bind the role to the controller.
First we create the Service Account - second we apply a RBAC file, to define what is allowed and what is not allowed.

* Create a service account for deploying CIS::

   kubectl create serviceaccount bigip-ctlr -n kube-system

* Create a Cluster Role and Cluster Role Binding on the Kubernetes Cluster using the examples below::

   kubectl apply -f  k8s_rbac.yaml

|

Now it is time to start configuring and deplyoing the CIS controller.
From the CIS yaml file, the main changes are done within the *args* section::

          args: [
            # See the k8s-bigip-ctlr documentation for information about
            # all config options
            # https://clouddocs.f5.com/products/connectors/k8s-bigip-ctlr/latest
            "--bigip-username=$(BIGIP_USERNAME)",
            "--bigip-password=$(BIGIP_PASSWORD)",
            "--bigip-url=10.1.20.5",
            "--bigip-partition=kubernetes",
            "--pool-member-type=cluster",
            "--insecure",


When using another CIS template as provided here, please change *bigip-url*, *bigip-partition* and, depending the deployment, *pool-member-type*.
|
Other options might be added - like *default-ingress-ip*.
|
For an overview, please check clouddocs :ref:`here <https://clouddocs.f5.com/products/connectors/k8s-bigip-ctlr/v1.11/#controller-configuration-parameters>`.
|
|
Finally apply the CIS controller.

* Create a CIS deployment using cis_deploy.yaml as shown below::

   kubectl apply -f  cis_deploy.yaml
|
|
Finally check, if the controller is **running**::

      ubuntu@kube-master:~$ kubectl get pods -n kube-system
      NAME                                        READY   STATUS    RESTARTS   AGE
      calico-kube-controllers-7567d8d9dd-x7dz9    1/1     Running   2          12h
      calico-node-2mdp2                           1/1     Running   2          12h
      calico-node-gmhbl                           1/1     Running   2          12h
      calico-node-zp9jh                           1/1     Running   2          12h
      coredns-66bff467f8-fdxkf                    1/1     Running   3          12h
      coredns-66bff467f8-s54hj                    1/1     Running   3          12h
      etcd-kube-master                            1/1     Running   3          12h
      k8s-bigip-ctlr-deployment-b8649597f-76xr5   1/1     Running   3          8h
      kube-apiserver-kube-master                  1/1     Running   3          12h
      kube-controller-manager-kube-master         1/1     Running   3          12h
      kube-proxy-dwzxh                            1/1     Running   3          12h
      kube-proxy-wc5wz                            1/1     Running   2          12h
      kube-proxy-x8kp8                            1/1     Running   2          12h
      kube-scheduler-kube-master                  1/1     Running   3          12h


You should see **k8s-bigip-ctlr-deployment**-<POD-ID>.

To check the config files online, please go :download:`github repo <https://github.com/de1chk1nd/F5k8sCalicoLab/blob/main/k8s/cis/002_setup_cis_bigip.yaml>`


.. toctree::
   :numbered:
   :hidden:
   :caption: Chapter 3 - Ingress Service

   Introduction <k8s-ingress/introduction>
   Container Ingress Service <k8s-ingress/cis>
   Basic Ingress <k8s-ingress/basic-ingress>
   Basic Ingress - TLS <k8s-ingress/basic-ingress-tls>
   Basic Ingress - L7 Routing <k8s-ingress/basic-ingress-l7-route>