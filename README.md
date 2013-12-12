packstack-answer
================

RDOを利用してOpenStack環境を手軽に構築するためのpackstackのanswer-fileです。
このanswer-fileを利用することにより、packstackで簡単にOpenStackのAll-in-One環境を構築することができます。

a) All-In-One環境を構築する
=========================

all-in-one.conf
---------------
1. VirtualBoxにHostOnlyNetworkを2面作成する
 <pre>
 vboxnet0: 192.168.0.240/24, DHCP off, プロミスキャスモード(全て許可)
 vboxnet1: 172.16.0.240/24 , DHCP off, プロミスキャスモード(全て許可)
 </pre>
2. 仮想マシンのスペック
 <pre>
 SPEC: CPU x 2 / Mem 4GB / HDD 20GB
 OS: CentOS6.4 x86_64
 NETWORK:
   eth0: 192.168.0.1/24 , Adapter1(vboxnet0)
   eth1: 172.16.0.1/24  , Adapter2(vboxnet1)
   eth2: DHCP           , Adapter3(NAT)
 </pre>
3. インストール手順 [http://www.slideshare.net/h-saito/openstack-quickstart-havana]

4. 構成
 <pre>
                                           vboxnet0
 -------+-----------------------------+--- 192.168.0.0/24
        |                             |.240
        |.1                           |
 +------+------+                    |
 |     RDO     |                    |
 |  CentOS64   |                    |
 +---+-----+---+                    |
     |     |.1                        |
     |     |                          |    vboxnet1
     |   --+---------------------+----|--- 172.16.0.0/24
     |                           |.240|
     |                           |    |    NAT(DHCP)
 ----+--------------------+----|----|--- 10.0.4.0/24
                            |.2  |    |
                            |    |    |
                            |    |    |
                            |    |    |
                        +---+----+----+---+
                        |      HostOS     |
                        |  OSX,Win,Linux  |
                        +-----------------+
 </pre>

2) コントローラ1台 + Computeノード複数台
====================================

multi-node.conf
---------------

[TBD]