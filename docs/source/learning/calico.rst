Calico
======

This chapter provides some additional information about calico itself

Calico Lab
----------

To build an own lab, Nicola Mennant wrote a Dev Central post and explained how to set up this kind of lab in your own environment.
If you can not use UDF, and need a step-by-step introduction to get a basic lab up & running, I recommend to have a look into these posts:

* `F5 & Calico Part I <https://devcentral.f5.com/s/articles/CIS-and-Kubernetes-Part-1-Install-Kubernetes-and-Calico>`_
* `F5 & Calico Part II <https://devcentral.f5.com/s/articles/CIS-and-Kubernetes-Part-2-Install-F5-Container-ingress-services>`_


Calico SDN
++++++++++

To better understand the Calico SDN, I recommend to have a look into the video below - it was created by one of the developers from tigera and does a pretty good job in explaining the calico SDN. Basically everything is based on routing - so if you are, like me, a more network focused guy, you'll find this very easy, once the video is over.

.. raw:: html

   <p><a href="https://www.tigera.io/video/tigera-calico-fundamentals?wvideo=1h2w5xt3sv"><img src="https://embed-fastly.wistia.com/deliveries/311b99bce1acb570911fb5b82dc839b8.jpg?image_play_button_size=2x&amp;image_crop_resized=960x540&amp;image_play_button=1&amp;image_play_button_color=54bbffe0" style="width: 400px; height: 225px;" width="400" height="225"></a></p><p><a href="https://www.tigera.io/video/tigera-calico-fundamentals?wvideo=1h2w5xt3sv">Tigera Calico - Architecture &amp; Networking Fundamentals Video | Tigera</a></p>

.. admonition:: For the impatient ...

   00:52 - ~20:00 is the most important part


.. admonition:: pro tipp ...

      I used the general concept of this video session to "whiteboard" calico to my customers & partners ... usually it is well received, as the story unveils very good and is easy to follow and understand.



Check if all required services are running
------------------------------------------

Check Nodes
+++++++++++

**From kubernetes master (10.1.10.20)**

Check if the nodes are up & ready::

  ubuntu@ip-10-1-1-4:~/tmp$ kubectl get nodes
  NAME          STATUS   ROLES    AGE    VERSION
  ip-10-1-1-4   Ready    master   159d   v1.13.4
  ip-10-1-1-5   Ready    <none>   159d   v1.13.4
  ip-10-1-1-6   Ready    <none>   159d   v1.13.4


You should see 3 nodes - the master node and two worker nodes. Status must be :red:`"Ready"`

.. toctree::
   :maxdepth: 2