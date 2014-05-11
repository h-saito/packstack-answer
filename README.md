packstack-answer
================

RDOを利用してOpenStack環境を手軽に構築するためのpackstackのanswer-fileです。
このanswer-fileを利用することにより、packstackで簡単にOpenStackのAll-in-One環境を構築することができます。
事前準備
=======
VirtualBox環境で以下の構成のネットワークと仮想マシンを用意します。

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
3. インストール手順 [http://www.slideshare.net/h-saito/openstack-quickstart-icehouse]

a) All-In-One環境
=========================
1台の仮想マシンに、RDOが提供するコンポーネント全てをインストールしてOpenStack環境を構築します。同時にNagiosの環境も構築します。

all-in-one.conf
---------------
 <pre>
                                        vboxnet0
-------+---------------------------+--- 192.168.0.0/24
       |                           |.240
       |.1                         |
+------+------+                    |
|     RDO     |                    |
|  CentOS64   |                    |
+---+-----+---+                    |
    |     |.1                      |
    |     |                        |    vboxnet1
    |   --+-------------------+----|--- 172.16.0.0/24
    |                         |.240|
    |                         |    |    NAT(DHCP)
----+--------------------+----|----|--- 10.0.4.0/24
                         |.2  |    |
                         |    |    |
                         |    |    |
                         |    |    |
                     +---+----+----+---+
                     |      HostOS     |
                     |  OSX,Win,Linux  |
                     +-----------------+

 [インストール対象コンポーネント]
   MySQL
   MongoDB
   RabbitMQ or ApacheQPID ※OpenStackのリリースバージョンによりどちらかがインストールされる
   Nagios
   OpenStack
       Ceilometer
       Cinder
       Glance
       Heat
       Keystone
       Neutron
       Nova
       Swift
       Tempest
       OSClient
 </pre>
 
2) 最小構成All-In-One環境
=======================
1台の仮想マシンに、RDOが提供するコンポーネントの中から必要最小限のOpenStack環境を構築します。

minimal.conf
------------
 <pre>
                                        vboxnet0
-------+---------------------------+--- 192.168.0.0/24
       |                           |.240
       |.1                         |
+------+------+                    |
|     RDO     |                    |
|  CentOS64   |                    |
+---+-----+---+                    |
    |     |.1                      |
    |     |                        |    vboxnet1
    |   --+-------------------+----|--- 172.16.0.0/24
    |                         |.240|
    |                         |    |    NAT(DHCP)
----+--------------------+----|----|--- 10.0.4.0/24
                         |.2  |    |
                         |    |    |
                         |    |    |
                         |    |    |
                     +---+----+----+---+
                     |      HostOS     |
                     |  OSX,Win,Linux  |
                     +-----------------+

 [インストール対象コンポーネント]
  MySQL
  ApacheQPID
  OpenStack
      Cinder
      Glance
      Keystone
      Neutron
      Nova
      OSClient
 </pre>

3) コントローラ1台 + Computeノード複数台
====================================

multi-node.conf
---------------

[TBD]
