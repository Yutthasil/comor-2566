# Routing
Routing คือกระบวนการของการเลือกเส้นทางในเครือข่ายต่างๆ เพื่อส่งข้อมูลจากแหล่งต้นทางไปยังปลายทาง
## หลักการทำงานของ Routing
เมื่อคอมพิวเตอร์ของเราส่ง IP packet ที่มีข้อมูลไปยัง Gateway และ Gateway จะส่งต่อ packet นี้ไปยัง Gateway/ Router อื่น กระบวนการนี้จะเกิดขึ้นจนกระทั่งมาถึงเครื่องปลายทาง ซึ่งกระบวนการทั้งหมดที่เกี่ยวข้องใช้ protocol ประเภทต่างๆ เช่น FTP, IRC, HTTP และอื่นๆ อีกมากมาย
บน Linux IP Packet ที่มีข้อมูลจะถูกจัดเก็บไว้ในประเภทของโครงสร้าง kernel ซึ่งเรียกว่า routing table เราสามารถเปลี่ยนตารางนี้ได้ในขณะที่กำหนดค่าคอมพิวเตอร์ของเราเพื่อสื่อสารกับคอมพิวเตอร์เครื่องอื่นผ่านเครือข่าย

## ประเภทของ Routing
1.	**Static Routing :** เป็นกระบวนการที่เราต้องเพิ่มเส้นทางด้วยตนเองใน routing table เป็นกระบวนการที่ได้รับความนิยมน้อย 
2.	**Dynamic Routing :** ในการเพิ่มเส้นทางโดยอัตโนมัติตามสถานะปัจจุบันของเส้นทางที่มีอยู่ใน routing table การกำหนดเส้นทางแบบ Dynamic ใช้ Protocol ที่แตกต่างกันในการค้นหาปลายทางของเครือข่าย และ path/route เพื่อไปยังปลายทาง
มี Routing Information Protocol (RIP) และ Open Shortest Path First (OSPF) เป็น Protocol การกำหนดเส้นทางแบบ Dynamic ที่ดีที่สุด
3.	**Default Routing :** ใน Router ได้รับการกำหนดค่าให้ส่ง Packet ทั้งหมดไปยัง Gateway/Router เดียว และดำเนินต่อไปจนถึงการ hop ครั้งถัดไป Packet จะถูกส่งต่อไปยัง Router ซึ่งได้รับการกำหนดค่าสำหรับการกำหนดเส้นทางเริ่มต้นโดยไม่คำนึงถึง Packet เครือข่ายใดๆ Router ดังกล่าวเรียกอีกอย่างว่า stub router


## Routing table
อุปกรณ์เครือข่ายทั้งหมด ไม่ว่าจะเป็น Host, Router หรือโหนดเครือข่ายประเภทอื่นๆ จำเป็นต้องมีตัดสินใจเกี่ยวกับตำแหน่งที่จะกำหนดเส้นทาง TCP/IP data packets ซึ่ง Routing table จะให้ข้อมูลการกำหนดค่าที่จำเป็นในการตัดสินใจเหล่านั้น ใช้เพื่อกำหนดเส้นทางเดียวที่พร้อมใช้งานสำหรับ typical local host และเพื่อพิจารณาว่าจะส่ง Packet ไปยัง default gateway router หรือไม่
คำสั่ง **route -n** แสดงรายการ Routing table; -n option จะแสดงผลลัพธ์เป็นที่อยู่ IP เท่านั้น และจะไม่ค้นหา DNS ซึ่งจะแทนที่ที่อยู่ IP ด้วยชื่อ Host  และถ้าหากเราใช้คำสั่ง netstat -rn ก็จะได้ผลลัพธ์ที่คล้ายกัน

``` bash
[root@host1 ~]# route -n
Kernel IP routing table
Destination     Gateway         Genmask         Flags Metric Ref    Use Iface
0.0.0.0         192.168.0.254   0.0.0.0         UG    100    0        0 eno1
192.168.0.0     0.0.0.0         255.255.255.0   U     100    0        0 eno1
```
_ตัวอย่างที่ 1_

Default gateway จะแสดง destination 0.0.0.0 เสมอเมื่อใช้ -n option หากไม่ได้ใช้ -n คำว่า "Default" จะปรากฏในคอลัมน์ Destination ของ Output ที่อยู่ IP ในคอลัมน์ Gateway คือที่อยู่ของ outbound gateway router และ netmask 0.0.0.0 สำหรับ Default gateway หมายความว่า Packet ใดๆ ที่ไม่ได้ระบุถึง local network หรือ outbound router อื่นโดยรายการเพิ่มเติมในRouting table จะถูกส่งไปยัง Gateway เริ่มต้นโดยไม่คำนึงถึง network class

คอลัมน์ Iface (Interface) ใน _ตัวอย่างที่ 1_ คือชื่อของ outbound NIC ในกรณีนี้คือ eno1 สำหรับ Host ที่ทำหน้าที่เป็น Router อาจมี NIC อย่างน้อยสองตัวหรือมากกว่านั้น ซึ่ง NIC แต่ละตัวที่ใช้เป็นเส้นทางจะเชื่อมต่อกับ physical and logical network ที่แตกต่างกัน ส่วนคอลัมน์ flags จะระบุว่าเส้นทางเป็นขึ้น (U) และซึ่งเป็น default gateway (G) อาจมี flag อื่น ๆ อยู่ด้วย

การตัดสินใจกำหนดเส้นทางของ Host ส่วนใหญ่:
* หาก destination host อยู่บน local network ให้ส่งข้อมูลไปยัง destination host โดยตรง
* destination host อยู่บน remote network  ที่สามารถเข้าถึงได้ผ่าน Gateway ภายในเครื่องที่แสดงอยู่ใน Routing table ให้ส่งไปยัง Gateway ที่กำหนดไว้อย่างชัดเจน
* หาก destination host อยู่บน remote network และไม่มีรายการอื่นที่กำหนดเส้นทางไปยัง Host นั้น ให้ส่งข้อมูลไปยัง default gateway

ก็คือหากสิ่งอื่นทั้งหมดล้มเหลวเนื่องจากไม่มีข้อที่ตรงกัน ให้ส่ง Packet ไปยัง default gateway

Routing table ใน _ตัวอย่างที่ 2_ จะมีความซับซ้อนกว่าเล็กน้อยเนื่องจากเป็นของ Linux Host ที่ทำหน้าที่เป็นเราเตอร์ที่เชื่อมต่อกับเครือข่ายสามเครือข่าย ซึ่งเครือข่ายหนึ่งนำไปสู่อินเทอร์เน็ต 
local class C networks ภายใน 192.168.0.0/24 บน interface eth1, 192.168.25.0/24 บน eth2 แต่ละรายการมีรายการในตาราง เช่นเดียวกับ default route ที่นำไปสู่ส่วนที่เหลือ the world on eth0


``` bash
[root@host2 ~]# route -n
Kernel IP routing table
Destination     Gateway         Genmask         Flags Metric Ref    Use Iface
192.168.1.24    0.0.0.0         255.255.255.252 U     0      0        0 eth0
192.168.0.0     0.0.0.0         255.255.255.0   U     0      0        0 eth1
192.168.25.0    0.0.0.0         255.255.255.0   U     0      0        0 eth2
0.0.0.0         192.168.1.25    0.0.0.0         UG    0      0        0 eth0
```
_ตัวอย่างที่ 2_

## Routing configuration 
การกำหนดค่าให้กับ routing table สำหรับ Host ที่เชื่อมต่อกับเครือข่ายโดยใช้ DHCP เซิร์ฟเวอร์ DHCP จะให้ข้อมูลการกำหนดค่าสำหรับ default route พร้อมกับ DNS ที่อยู่ IP ของ Host และข้อมูลอื่น ๆ เช่น ที่อยู่ IP สำหรับเซิร์ฟเวอร์ NTP สำหรับการกำหนดค่าแบบคงที่(static configurations) โดยทั่วไปจะเป็นเรื่องง่าย แต่บางครั้งอาจซับซ้อนกว่าเล็กน้อย
ในกรณีส่วนใหญ่ การเพิ่ม default route ให้กับไฟล์ /etc/sysconfig/network จะทำให้เครือข่ายกำหนดค่าเส้นทางเริ่มต้นใน routing table  รายการนั้นเช่นเดียวกับ _ตัวอย่างที่ 3_

``` bash
GATEWAY=192.168.0.1
```
_ตัวอย่างที่ 3_

เฉพาะ default gateway เท่านั้นที่สามารถกำหนดค่าโดยใช้ network file ได้

อีกวิธีในการกำหนดค่า default gateway ใน environment  ที่กำหนดค่าแบบคงที่คือการเพิ่มลงในไฟล์การกำหนดค่า interface ที่เหมาะสมใน directory /etc/sysconfig/network-scripts หากต้องการเพิ่ม Gateway ให้กับไฟล์การกำหนดค่า interface สำหรับ interface eth0 เราจะต้องเพิ่มบรรทัดตาม _ตัวอย่างที่ 3_ ลงในไฟล์ ifcfg-eth0 ซึ่งหากเราทำเช่นนั้น เราก็ควรจะลบรายการนั้นออกจาก network file ด้วย

ใน environment ที่ซับซ้อนมากขึ้น เช่น เมื่อhost computer เชื่อมต่อกับหลายเครือข่ายโดยใช้ NIC หลายตัว และเมื่อมีเส้นทางอย่างน้อยสองเส้นทางหรืออาจมากกว่านั้นที่ต้องป้อนลงใน routing table เราควรจะใช้ route file ใน /etc/sysconfig/network-scripts. สำหรับ NIC enp7s1 ไฟล์นั้นจะเป็น Route-enp7s1 และจะมีรายการที่แสดงใน _ตัวอย่างที่ 4_

``` bash
default via 192.168.0.1 dev enp7s1
```
_ตัวอย่างที่ 4_
การตั้งค่า Default gateway ใน route-interface files จะแทนที่การตั้งค่าใดๆ ที่อาจแสดงอยู่ใน network file

และเราสามารถเพิ่ม route จาก command line ได้โดยใช้ route command   ดังแสดงใน _ตัวอย่างที่ 5_

``` bash
route del default
route add default gw 192.168.0.1
```
_ตัวอย่างที่ 5_

## Commands of Linux Route

Command:
``` bash
route
```

Output:
``` bash
Kernel IP routing table
Destination     Gateway         Genmask         Flags Metric Ref    Use Iface
default         192.168.10.2    0.0.0.0         UG    1024   0        0 eth0
192.168.10.0       *         255.255.255.0      U     0      0        0 eth1
```

Command:
``` bash
route Options
```
Options:
* **-A family** : ใช้สำหรับตระกูลที่อยู่ที่ระบุ
* **-F** : ทำงานบน Forwarding Information Base (FIB) Routing table แบบ kernel-based ซึ่งเป็นค่าเริ่มต้น
* **-C** : ทำงานบน kernel routing cache
* **-v** : ดำเนินการแบบละเอียด
* **-n** : ใช้สำหรับ IP address ที่เป็นตัวเลขแทน hostname เพื่อทำความเข้าใจเมื่อเส้นทางไปยัง nameserver ที่หายไป
* **-e** : แสดง Routing table ในรูปแบบ netstat
* **del** : ลบ route
* **add** : เพิ่ม route ในตาราง
* **-net** : กำหนดว่าเป้าหมายเป็นnetwork
* **-host** : เมื่อเป้าหมายเป็น Host
* **netmask NM** : เมื่อเราต้องการเพิ่ม network route แล้ว netmask จะถูกใช้งาน
* **gw Gw** : ตัวเลือกนี้จะกำหนดเส้นทาง Packet ผ่าน Gateway 
_หมายเหตุ:_ ต้องเข้าถึง Gateway ก่อน ซึ่งหมายความว่าเราจำเป็นต้องกำหนดเส้นทางแบบคงที่ไปยัง Gateway ก่อน
* **metric M** : ใช้เพื่อตั้งค่าฟิลด์เมตริกใน Routing table เป็น M

Command:
``` bash
netstat -r
```
แสดงการเชื่อมต่อเครือข่ายเป็น Transmission Control Protocol, Printers, LAN, Routing tables, interfaces multicasts, etc.

Output:
``` bash
Kernel IP routing table
Destination     Gateway         Genmask         Flags Metric Ref    Use Iface
default         192.168.10.2    0.0.0.0         UG    1024   0        0 eth0
192.168.11.0       *         255.255.254.0      UG    1026   0        0 eth1
```

Command:
``` bash
ip route show or ip route list
```

Output:
``` bash
10.144.207.98/27 dev eth1 proto kernel scope link src 10.144.216.121
172.26.31.0/22 dev eth0 proto kernel scope link src 172.26.31.43
10.192.192.0/18 via 10.144.216.98 dev eth1
default via 172.26.31.1 dev eth0 proto static
```
Command:
``` bash
route add default gw 192.167.1.254 eth1
```
It will route all the traffic via 192.168.1.254 gateway connected through eth1 network interface.

Command:
``` bash
ip route add 192.167.1.0/25 dev eth1
```
กำหนดเส้นทางการรับส่งข้อมูลทั้งหมดผ่าน gateway 192.168.1.254 ที่เชื่อมต่อผ่าน network interface eth1

Command:
``` bash
route -Cn
```
Kernel กำลังรักษาข้อมูล route cache information เพื่อกำหนดเส้นทาง Packet อย่างรวดเร็วโดยใช้ตัวเลือก -C

Output:
``` bash
Kernel IP routing cache
#Source       #Destination     #Gateway     #Flags #Metric #Ref  #Use #Iface
192.169.1.157 192.162.2.51    192.168.9.51    0     0       1     0   eth0
192.169.1.157 74.125.237.69   192.168.4.10    0     0       1     0   eth1
```

Command:
``` bash
route add -host 192.167.2.52 reject
```
เมื่อเราต้องการปฏิเสธ Host หรือ network เพื่อรับ packets เราจะใช้เพื่อปฏิเสธ command หลังจากนั้นเราต้องตรวจสอบว่า host/network นั้นเข้าถึงได้หรือไม่ :

Command:
``` bash
ping 192.168.1.51
```
Output: Network is unreachable

Command:
``` bash
Make 192.167.3.* Accessible from 192.167.1.*
```
เราต้องเพิ่มข้อมูล routing เพื่อให้เราสามารถเข้าถึง 192.168.3 ได้อย่างเต็มที่ ชุดของที่อยู่ IP จาก 192.167.1 

Command:
``` bash
route add default gw 192.167.1.10
```
เมื่อ 192.167.1.1 ping 192.167.3.1 จะเปลี่ยนเส้นทางไปยัง GATEWAY ผ่าน 192.168.1.10 ใน GATEWAY เราจำเป็นต้องเพิ่มรายการ routing

Command:
``` bash
route add -net 192.167.3.0  netmask  255.255.254.0  gw  192.167.3.10
```
packet ทั้งหมดถูกส่งไปยังเครือข่าย 192.167.3.* จะถูกส่งผ่าน gateway interface 192.167.3.10 ซึ่งจะส่ง packet ไปยัง destination

## Reference 
* https://opensource.com/sites/default/files/gated-content/osdc_cheatsheet-networking-2021.4.8.pdf
* https://opensource.com/business/16/8/introduction-linux-network-routing
* https://www.educba.com/linux-route-command/
