Calico
======

This chapter provides some additional information about calico itself


Calico SDN
----------

To better understand the Calico SDN, I recommend to have a look into the video below - it was created by one of the developers from tigera and does a pretty good job in explaining the calico SDN. Basically everything is based on routing - so if you are, like me, a more network focused guy, you'll find this very easy, once the video is over.

.. raw:: html

   <p><a href="https://www.tigera.io/video/tigera-calico-fundamentals?wvideo=1h2w5xt3sv"><img src="https://embed-fastly.wistia.com/deliveries/311b99bce1acb570911fb5b82dc839b8.jpg?image_play_button_size=2x&amp;image_crop_resized=960x540&amp;image_play_button=1&amp;image_play_button_color=54bbffe0" style="width: 400px; height: 225px;" width="400" height="225"></a></p><p><a href="https://www.tigera.io/video/tigera-calico-fundamentals?wvideo=1h2w5xt3sv">Tigera Calico - Architecture &amp; Networking Fundamentals Video | Tigera</a></p>

.. admonition:: INFO

   00:52 - ~20:00 is the most important part
   

   Use this whiteboard to show your peers how calico works - from my experience, it is very well received (as the story is very well structured).



Check if all required services are running
------------------------------------------

Once basic installation ist done, calico default file is installed::

   kubectl apply -f https://docs.projectcalico.org/manifests/calico.yaml

.. admonition:: Calico already installed

   In preperation for this lab, calico is already installed. No need to install this packet, now!


Check Nodes
-----------

**From kubernetes master (10.1.20.20)**

Check if the nodes are up & ready::

   ubuntu@kube-master:~$ kubectl get nodes
   NAME            STATUS   ROLES    AGE   VERSION
   kube-master     Ready    master   13m   v1.18.10
   kube-worker-1   Ready    <none>   36s   v1.18.10
   kube-worker-2   Ready    <none>   22s   v1.18.10


You should see 3 nodes - the master node and two worker nodes. Status must be "Ready"

Check runnung PODs::

   ubuntu@kube-master:~$ kubectl get pods --all-namespaces
   NAMESPACE     NAME                                       READY   STATUS    RESTARTS   AGE
   kube-system   calico-kube-controllers-7567d8d9dd-x7dz9   1/1     Running   0          2m10s
   kube-system   calico-node-2mdp2                          1/1     Running   0          66s
   kube-system   calico-node-gmhbl                          1/1     Running   0          80s
   kube-system   calico-node-zp9jh                          1/1     Running   0          2m10s
   kube-system   coredns-66bff467f8-fdxkf                   1/1     Running   1          13m
   kube-system   coredns-66bff467f8-s54hj                   1/1     Running   1          13m
   kube-system   etcd-kube-master                           1/1     Running   1          14m
   kube-system   kube-apiserver-kube-master                 1/1     Running   1          14m
   kube-system   kube-controller-manager-kube-master        1/1     Running   1          14m
   kube-system   kube-proxy-dwzxh                           1/1     Running   1          13m
   kube-system   kube-proxy-wc5wz                           1/1     Running   0          66s
   kube-system   kube-proxy-x8kp8                           1/1     Running   0          80s
   kube-system   kube-scheduler-kube-master                 1/1     Running   1          14m

You should see clico PODs up & running, kube-proxy (one for each node) and DNS Services up & running.



.. toctree::
   :hidden:
   :maxdepth: 1
   :caption: Chapter 1 - Information

   Introduction <learning/introduction>
   Calico <learning/calico>
   ISTIO <learning/istio>