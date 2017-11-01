# Setting up source NAT in SRX

## Basics

1.  Create a NAT connection in VMware workstation – edit – Virtual Network Editor – Change settings
– choose NAT (remove the √ from the DHCP box if you have configured it in your virtual router)
2.  Make a subnet IP, then go into NAT settings and make a Gateway IP
3.  Go into settings on the SRX router – choose the NAT connection and network adapter you want to
use ie. VMnet15 - Network adapter 4 (interface ge0/0/3)

## Configuration step by step in cli mode
1. Make an interface for the NAT connection
    ```
    [edit]
    root@vSRX1# edit interfaces
    [edit interfaces]
    root@vSRX1# set ge-0/0/3 unit 0 family inet address 192.168.222.2/24
    [edit interfaces]
    root@vSRX1# commit
    commit complete
    [edit interfaces]
    root@vSRX1# exit
    ```

2. Set interface used for the NAT connection in the untrust zone in your security zones, set it to “all”
– as seen below. Then you can make sure it works, and we can go more into detail later
    ```
    [edit]
    root@vSRX1# edit security zones
    [edit security zones]
    root@vSRX1# set security-zone untrust interfaces ge-0/0/3 host-inbound-
    traffic system-services all
    [edit security zones]
    root@vSRX1# commit
    commit completeNow your security zones for ge-0/0/3 should look like this (highlighted):
    [edit security zones]
    root# show
    security-zone trust {
      tcp-rst;
      interfaces {
        ge-0/0/1.0 {
          host-inbound-traffic {
            system-services {
              ping;
              dhcp;
              all;
            }
          }
        }
      }
    }
    security-zone untrust {
      interfaces {
        ge-0/0/3.0 {
          host-inbound-traffic {
            system-services {
              ping;
            }
          }
        }
      }
    }
    [edit security zones]
    root# exit
    ```

3. Create a static route to the NAT default gateway in the routing table:
    ```
    [edit]
    root@vSRX1# edit routing-options
    [edit routing-options]
    root@vSRX1# set static route 0.0.0.0/0 next-hop 192.168.222.1
    [edit routing-options]
    root@vSRX1# commit
    commit complete
    Now you should be able to see the static route you’ve made in the routing-options:
    [edit routing-options]
    root@vSRX1# show
    static {
      route 0.0.0.0/0 next-hop 192.168.222.1;
    }
    [edit routing-options]
    root@vSRX1# exit
    ```

    And you should also be able to see it in your routing table:
    ```
    [edit]
    root@vSRX1# run show route terse
    A Destination   P Prf   Metric 1  Metric 2  Next hop            AS
    Path
    * 0.0.0.0/0     S   5                       >192.168.222.1
    ```

4. Now you need to set up the NAT security source, first by creating a source NAT rule set, then you
configure a security policy that allows traffic from the trust zone to the untrust zone:
    ```
    [edit]
    root@vSRX1# edit security nat source
    [edit security nat source]
    root@vSRX1# set rule-set rs1 from zone trust
    [edit security nat source]
    root@vSRX1# set rule-set rs1 to zone untrust
    [edit security nat source]root@vSRX1# set rule-set rs1 rule r1 match source-address 0.0.0.0/0
    [edit security nat source]
    root@vSRX1# set rule-set rs1 rule r1 match destination-address 0.0.0.0/0
    [edit security nat source]
    root@vSRX1# set rule-set rs1 rule r1 then source-nat interface
    [edit security nat source]
    root@vSRX1# commit
    commit complete
    [edit security nat source]
    root@vSRX1# exit
    [edit]
    root@vSRX1# edit security policies from-zone trust to-zone untrust
    [edit security policies from-zone trust to-zone untrust]
    root@vSRX1# set policy internet-access match source-address any
    destination-address any application any
    [edit security policies from-zone trust to-zone untrust]
    root@vSRX1# set policy internet-access then permit
    [edit security policies from-zone trust to-zone untrust]
    root@vSRX1# commit
    commit complete
    [edit security policies from-zone trust to-zone untrust]
    root@vSRX1# exit
    Now your security NAT should look like this:
    [edit]
    root# show security nat
    source {
      rule-set rs1 {
        from zone trust;
        to zone untrust;
        rule r1 {
          match {
            source-address 0.0.0.0/0;
            destination-address 0.0.0.0/0;
          }
          then {
            source-nat {
              interface;
          }
    ```

## Test
Now you should be able to ping 8.8.8.8 from your vSRX router, and any hosts you have working on your
network. 

Remember If you have several routers interconnected, you must use `set static route
0.0.0.0/0 next-hop <ip address>` to the router with the NAT service.
