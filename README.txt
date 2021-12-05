HW-3 
Cloud Computing




Task 1: Defining custom topologies




Ans 1 :
mininet> nodes
available nodes are: 
c0 h1 h2 h3 h4 h5 h6 h7 h8 s1 s2 s3 s4 s5 s6 s7
mininet> net
h1 h1-eth0:s3-eth2
h2 h2-eth0:s3-eth3
h3 h3-eth0:s4-eth2
h4 h4-eth0:s4-eth3
h5 h5-eth0:s6-eth2
h6 h6-eth0:s6-eth3
h7 h7-eth0:s7-eth2
h8 h8-eth0:s7-eth3
s1 lo:  s1-eth1:s2-eth1 s1-eth2:s5-eth1
s2 lo:  s2-eth1:s1-eth1 s2-eth2:s3-eth1 s2-eth3:s4-eth1
s3 lo:  s3-eth1:s2-eth2 s3-eth2:h1-eth0 s3-eth3:h2-eth0
s4 lo:  s4-eth1:s2-eth3 s4-eth2:h3-eth0 s4-eth3:h4-eth0
s5 lo:  s5-eth1:s1-eth2 s5-eth2:s6-eth1 s5-eth3:s7-eth1
s6 lo:  s6-eth1:s5-eth2 s6-eth2:h5-eth0 s6-eth3:h6-eth0
s7 lo:  s7-eth1:s5-eth3 s7-eth2:h7-eth0 s7-eth3:h8-eth0
c0


Ans 2 : 

mininet> h7 ifconfig
h7-eth0: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet 10.0.0.7  netmask 255.0.0.0  broadcast 10.255.255.255
        inet6 fe80::40db:47ff:fe97:e981  prefixlen 64  scopeid 0x20<link>
        ether db:47:67:e9:81  txqueuelen 1000  (Ethernet)
        RX packets 56  bytes 4232 (4.2 KB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 10  bytes 796 (796.0 B)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0


lo: flags=73<UP,LOOPBACK,RUNNING>  mtu 65536
        inet 127.0.0.1  netmask 255.0.0.0
        inet6 ::1  prefixlen 128  scopeid 0x10<host>
        loop  txqueuelen 1000  (Local Loopback)
        RX packets 0  bytes 0 (0.0 B)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 0  bytes 0 (0.0 B)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0






Task 2: Analyze the “of_tutorial’ controller:


Ans 1 :


_handle_PacketIn() -> act_like_hub() -> resend_packet()


Ans 2 :


1. For h1 to h2, it takes 4.790ms on average.
           For h1 to h8, it takes 30.992ms on average.


2. for h1 to h2: min = 4.2, max = 51. ms
for h1 to h8 : min =  22.6, max =110 ms. 

3. The time cost by h1 to h8 is longer than h1 to h2.
Because h1 to h8 only needs s3 to forward packets, but h1 to h8 needs s3, s2, s1, s5, s7 to forward packets.

Ans 3 :


   1. Iperf is a tool for network performance measurement and tuning. Iperf has client and server functionality, and can create data streams to measure the throughput between the two ends in one or both directions.

   2. the throughput for h1 to h2 is 3.02 Mbits/sec, and from h2 to h1 is 2.72 Mbits/sec.
   3. The throughput from h1 to h2 is larger than h1 to h8 because from h1 to h8, there are more switches needed to forward packets.





Ans 4 : 


s3 observes traffic for iperf h1 h2
s3, s2, s1, s5, s7 observe traffic for iperf h1 h8





Task 3: MAC Learning Controller



Ans 1 : the code works by linking ports to source MACs


Ans 2 : 


      1. h1 to h2 took 2.3 ms
 h1 to h8 took 9.60 ms


      2. for h1 to h2 min=1.08, max = 6.6 ms
for h1 to h8, min=  5.9, max= 14.6 ms


      3. it takes less time compared to Task 2




And 3 :


b) between h1 and h2 there is a huge difference