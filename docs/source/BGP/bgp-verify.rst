.. raw:: html

   <style> .red {color:red}; font-weight:bold </style>

.. role:: red


.. raw:: html

   <style> .blue {color:blue}; font-weight:bold </style>

.. role:: blue


Verify BGP Configuration
========================

Now we are going to verify, that the routes are up

on kubernetes
+++++++++++++

**From kubernetes master (10.1.20.20)**

Login to :blue:`kubernetes master (10.1.20.20)` and issue *calicoctl get bgpPeer*::

      # Check BGP Peers via calicoctl 
      calicoctl get bgpPeer
      

The output should be similar to this::     
      
      NAME                    PEERIP      NODE       ASN
      bgppeer-global-bigip1   10.1.20.5   (global)   64512


BGP Peer F5 is available.


on bigip
++++++++

**From bigip CLI (10.1.20.5)**::

    # login to imish
    imish

    # show bgp peerings (state)
    show ip bgp neighbors


Check for :red:`BGP state = Established` in the output for each member in the response::

      bigip-1.lab.cloud[0]#sh ip bgp neighbors
      BGP neighbor is 10.1.20.20, remote AS 64512, local AS 64512, internal link
       Member of peer-group calico-k8s for session parameters
        BGP version 4, remote router ID 10.1.20.20
        BGP state = Established, up for 00:00:16
        Last read 00:00:16, hold time is 90, keepalive interval is 30 seconds


Also check if routes are announced (also in imish shell)::

      sh ip route bgp
      
Check announced routes and compare it to the k8s master/node IPs::
      
      B       192.168.127.0/26 [200/0] via 10.1.20.22, internal, 00:00:23
      B       192.168.180.0/26 [200/0] via 10.1.20.21, internal, 00:00:23
      B       192.168.221.192/26 [200/0] via 10.1.20.20, internal, 00:00:23

      Gateway of last resort is not set

|

Interpretation of bgp Routes
++++++++++++++++++++++++++++

Please remember the BGP Route output::

      sh ip route bgp
      
      B       192.168.127.0/26 [200/0] via 10.1.20.22, internal, 00:00:23
      B       192.168.180.0/26 [200/0] via 10.1.20.21, internal, 00:00:23
      B       192.168.221.192/26 [200/0] via 10.1.20.20, internal, 00:00:23

We can see 3 routes announced via BGP:

* 192.168.221.192/26 via 10.1.20.20 :red:`(kubernetes master)`

* 192.168.180.0/26 via 10.1.20.21 :red:`(kubernetes worker I)`

* 192.168.127.0/26 via 10.1.20.22 :red:`(kubernetes worker II)`

Each k8s node is running a certain amount of pods - these pods have an 192.168.*.* IP/subnet assigned.

|

**Calico SDN**


.. admonition:: IMPORTANT!

   If you skipped the tigera video about the calico installation - and might miss something in the part below.
   I recommend to check the video again, as this explains the architecture very well and is helpfull.


Calico SDN is based on routing - more or less.

1. Calico creates tunnel interfaces to *"link"* PODs to the Host Network

2. Within the POD - each PODs has a default route pointing to their (tunnel)interface

3. On host level - to be able to route traffic to specific PODs, local routes are Created

4. To route to PODs on *external* nodes (e.g. worker-I to worker-II), hosts needs to have a route pointing to the nexthop

5. To automate "4", BGP is used (dynamic update of *"external"* routes)

**From kubernetes-master (10.1.20.20)**

Let's check running PODs to show this for one example::

      # kubectl get pods to show running PODs - and use "--all-namespaces" to show PODs on all namespaces
      kubectl get pods --all-namespaces
            
      NAMESPACE     NAME                                       READY   STATUS    RESTARTS   AGE
      kube-system   calico-kube-controllers-7567d8d9dd-x7dz9   1/1     Running   1          179m
      kube-system   calico-node-2mdp2                          1/1     Running   1          178m
      kube-system   calico-node-gmhbl                          1/1     Running   1          178m
      kube-system   calico-node-zp9jh                          1/1     Running   1          179m
      kube-system   coredns-66bff467f8-fdxkf                   1/1     Running   2          3h11m
      kube-system   coredns-66bff467f8-s54hj                   1/1     Running   2          3h11m
      kube-system   etcd-kube-master                           1/1     Running   2          3h11m
      kube-system   kube-apiserver-kube-master                 1/1     Running   2          3h11m
      kube-system   kube-controller-manager-kube-master        1/1     Running   2          3h11m
      kube-system   kube-proxy-dwzxh                           1/1     Running   2          3h11m
      kube-system   kube-proxy-wc5wz                           1/1     Running   1          178m
      kube-system   kube-proxy-x8kp8                           1/1     Running   1          178m
      kube-system   kube-scheduler-kube-master                 1/1     Running   2          3h11m


Let us take the calico controller as example (since we do not have any apps deployed, yet)::

      # get detailed info for POD 'calico-kube-controllers-7567d8d9dd-x7dz9'
      kubectl describe pod calico-kube-controllers-7567d8d9dd-x7dz9 -n kube-system
      
      Name:                 calico-kube-controllers-7567d8d9dd-x7dz9
      Namespace:            kube-system
      Priority:             2000000000
      Priority Class Name:  system-cluster-critical
      Node:                 kube-master/10.1.20.20
      Start Time:           Tue, 03 Nov 2020 20:45:29 +0000
      Labels:               k8s-app=calico-kube-controllers
                           pod-template-hash=7567d8d9dd
      Annotations:          cni.projectcalico.org/podIP: 192.168.221.198/32
                           cni.projectcalico.org/podIPs: 192.168.221.198/32
      Status:               Running
      IP:                   192.168.221.198

| The Controller hast IP :red:`192.168.221.198`
| According to the BGP Routing, :red:`192.168.221.198` is hosted on kube-master (10.1.20.20).

.. warning::
   
   Check IP Address accordingly. It might change!! Adjust as required in the following commands!


Login to kube-master (10.1.20.20) and check routing table::

      # show local routes via 'netstat'
      netstat -rn | grep 192.168.221.198
      
      
      192.168.221.198 0.0.0.0         255.255.255.255 UH        0 0          0 cali430463d79fe

Remember - calico creates tunnel interfaces - and routes POD IPs to that Tunnel interface::

      # show interface info from tunnel interface 'cali430463d79fe'
      ifconfig cali430463d79fe
      
      cali430463d79fe: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1440
            inet6 fe80::ecee:eeff:feee:eeee  prefixlen 64  scopeid 0x20<link>
            ether ee:ee:ee:ee:ee:ee  txqueuelen 0  (Ethernet)
            RX packets 1429  bytes 128030 (128.0 KB)
            RX errors 0  dropped 0  overruns 0  frame 0
            TX packets 1552  bytes 867320 (867.3 KB)
            TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0


Now let's test this.

**From bigip TMUI (10.1.20.5)**

Issue a ping from bigip to one POD IP::

      # From F5 BigIP PING POD IP
      ping 192.168.221.198
            
      PING 192.168.221.198 (192.168.221.198) 56(84) bytes of data.
      64 bytes from 192.168.221.198: icmp_seq=1 ttl=63 time=0.885 ms
      64 bytes from 192.168.221.198: icmp_seq=2 ttl=63 time=0.805 ms
      64 bytes from 192.168.221.198: icmp_seq=3 ttl=63 time=1.15 ms
      64 bytes from 192.168.221.198: icmp_seq=4 ttl=63 time=0.718 ms
      ^C


Summary
+++++++

To sum this up (what happens with that ping):

1. ping to 192.168.221.198
2. :red:`bigip` looks up routing table and finds the announced bgp route to :blue:`kube-master`
3. :blue:`kube-master` receives traffic from the f5 - and finds a route to local tunnel interface
4. return traffic leaving the POD (through tunnel interface), will be sent back to f5 (either because of SNAT on :red:`bigip` or via default route)


.. toctree::
   :numbered:
   :hidden:
   :caption: Chapter 2 - set up BGP

   Introduction <BGP/introduction>
   Calico - BGP <BGP/calico-bgp>
   F5 BigIP - BGP <BGP/bigip-bgp>
   BGP - Verification <BGP/bgp-verify>