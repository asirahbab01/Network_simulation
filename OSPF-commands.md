Router0#

en

conf t

int s0/3/0

ip addr 192.168.20.1 255.255.255.0

clock rate 1200

no shut

ex

int f0/0

ip addr 192.168.10.1 255.255.255.0

no shut

ex

ip dhcp pool cse

network 192.168.10.0 255.255.255.0

default-route 192.168.10.1

ex

route ospf 1

router-id 1.1.1.1

network 192.168.10.0 0.0.0.255 area 0

network 192.168.20.0 0.0.0.255 area 1

area 1 virtual-link 3.3.3.3   /\*Virtual-link created\*/

ex

do show ip route





Router1#

en

conf t

int s0/3/0

ip addr 192.168.20.2 255.255.255.0

no shut

ex

en

conf t

int s0/3/1

ip addr 192.168.30.1 255.255.255.0

clock rate 1200

no shut

ex

route ospf 1

router-id 2.2.2.2

network 192.168.20.0 0.0.0.255 area 1

network 192.168.30.0 0.0.0.255 area 1

ex

do show ip route





Router2#

en

conf t

int s0/3/0

ip addr 192.168.30.2 255.255.255.0

no shut

ex

int f0/0

ip addr 192.168.40.1 255.255.255.0

no shut

ex

ip dhcp pool eee

network 192.168.40.0 255.255.255.0

default-route 192.168.40.1

ex

route ospf 1

router-id 3.3.3.3

network 192.168.30.0 0.0.0.255 area 1

network 192.168.40.0 0.0.0.255 area 2

area 1 virtual-link 1.1.1.1   /\*Virtual-link created\*/

ex

do show ip route







**Note:** All the areas need to be connected with area 0/backbone area so that data communication can be done in the topology where OSPF routing is enabled.



\*\*Now what if all the areas are not connected to the area 0/ backbone area?



=> In that case we have to create a virtual link(VL). Thus a virtual link is created in the area1 due to which a virtual connection between area 0 and area 2 is successfully established for data communication. Without this link, Area 0 and Area 2 remain isolated from each other.





