# ucpe-ietf

YANG data model for uCPE management

https://datatracker.ietf.org/doc/draft-shytyi-opsawg-vysm/

   The uCPE as harware with x86
   capabilities that is generally running Linux distibution with
   additinal virtualisation layer.  Virtualization layer provides
   virtual compute, virtual storage and virtual network resources.  Each
   VNF runnning in the uCPE requires the amount of virtual resources
   (for example: 4 vCPUs, 4GB RAM, 40GB storege, 4 vPorts).  VNFs MAY be
   interconnected between each other and physical ports via Virtual
   Networks.  Topology construction and VM lifecycle management is
   allowed via high level interface (Configuration can be done in the
   same transaction).  The figure below presents the uCPE architecture.

         ----------------------------------------|--------------
         VNF1            VNF2            VNF3    |
         ----------------------------------------|
         Virtual         Virtual         Virtual | uCPE software
         Compute         Storage         Networks|
         ----------------------------------------|---------------
         PHY x86         RAM+PHY         PHYsical| uCPE Hardware
         processor       storage         ports   |



 uCPE purpose

   o  uCPE replaces multiple types of equipment (Node#1 - Node#5) with 1
      unit by virtualizing them as Virtual Network Functions on the top
      of NFVIs:

     :      NODE #1     :   NODE #2 :  NODE #3  :NODE #4: NODE #5  :
     :    +-----------+ :  +------+ :  +------+ :  +--+ :  +-----+ :
  ...-----|Aggregation|----|CE-L2 |----| CE-L3|----|FW|----|SDWAN|---LAN
     :    |  switch   | :  |      | :  |      | :  |  | :  |     | :
     :    +-----------+ :  +------+ :  +------+ :  +--+ :  +-----+ :

    :      NODE #1   :           NODE #2                           :
    :                : +.........................................+ :
    :  +-----------+ : |  +------+    +------+    +--+   +-----+ | :
 ...---|Aggregation|---|--|CE-L2 |----| CE-L3|----|FW|---|SDWAN|-|---LAN
    :  |  switch   | : |  |      |    |      |    |  |   |     | | :
    :  +-----------+ : |  +------+    +------+    +--+   +-----+ | :
    :                : |  universal Customer-Premises Equipment  | :
    :                : +-----------------------------------------+ :

   o  uCPE falicitates the interconnection between the Network Funtions
      (NF) as interconnection between NF is performed via virtual
      links(that is part of the uCPE management).  That meens that no
      need to hire technichian to cable the equipment, it could be done
      via orchestrator.

   o  uCPE falicitates the 0day configuration of the VNFs as its 0day
      configuration can be putted remotely.


uCPE VNF ecosystem example

   uCPE supports a Virtual Network Funcitons of different type:

   o  SD-WAN

   o  vRouter

   o  vFirewall

   o  vLB(vLoad Balancer)

   o  vCGNAT(vCarrier Grade NAT)

   o  virtual WAN Optimistaion

   o  vWireless LAN controller

   o  Other...
   
Internal uCPE service example

   The VNF in the uCPE could be a vRouter or vFirewall or an SD-WAN that
   is not a default part of virtual network resources of the uCPE.
   Multiple VNFs MAY be instantiated in the uCPE.  With support of links
   and swithes, VNFs MAY participate a service chains.  Example of
   service chains (Note that virtual switch "vs(WAN)" connected to LAN
   ports and vSW(WAN) is connected to WAN ports):

   o  vSW(WAN)-l1-vRouter-l2-vSW(LAN).

   o  vSW(WAN)-l1-vRouter-l2-vSW(Service)-l3-vFirewall-l4-vSW(LAN).

   o  vSW(WAN)-l1-vRouter-l2-vSW(Service1)-l3-vFirewall-l4-
      vSW(Service2)-l5-SD-WAN-l6-vSW(LAN).

   o  vSW(WAN)-l1-SDWAN-l2-vSW(Service)-l3-vFirewall-l4-vSW(LAN).

   o

         vSW(WAN1)--vRouter--+
                             +--vLoadBalance  vFirewall--vSW(LAN)
         vSW(WAN2)--vRouter--+     |              |
                                   +-vSW(Service1)+

   o

      vSW(WAN1)--vRouter(ISP1)--+
                                +--SD-WAN        vFirewall--vSW(LAN)
      vSW(WAN2)--vRouter(ISP2)--+     |              |
                                      +-vSW(Service1)+
