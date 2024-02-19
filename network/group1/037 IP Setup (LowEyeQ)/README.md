# IP Setup
IP Setup บน Linux เป็นเครื่องมือสำคัญสำหรับการกำหนดค่าเครือข่าย ช่วยให้ผู้ใช้สามารถกำหนดค่า IP address, subnet mask, gateway, DNS server และค่าอื่นๆ ที่จำเป็นสำหรับการเชื่อมต่อกับเครือข่าย
## Syntax:
The basic syntax of the IP command is as follows:
```bash
$ ip a or ip addr
```
Options:
The IP command supports the following command-line options:
| Command   | Description |
| ---|--- |
| **-V or -Version:**| ใช้เพื่อแสดงเวอร์ชันของ IP command|
| **-h, -human, -human-readable:**| ใช้เพื่อแสดงสถิติในรูปแบบของค่าที่มนุษย์สามารถอ่านได้ |
|**-b, -batch <FILENAME>** | ใช้เพื่ออ่านและเรียกใช้คำสั่งจากไฟล์หรืออินพุตที่กำหนด ตัวเลือก '-force' จะไม่ยอมให้ IP เมื่อมีข้อผิดพลาดในโหมดแบตช์ หากมีข้อผิดพลาดใดๆ ในระหว่างการดำเนินการ โค้ดส่งคืนจะไม่ใช่ศูนย์ |
| **-s, -stats, -statistics**| ใช้เพื่อแสดงข้อมูลเพิ่มเติม เช่น สถิติหรือค่าเวลา |
| **-d, -details**| ใช้เพื่อแสดงผลแบบละเอียด |
| **-h, -human, -human-readable**| ใช้เพื่อแสดงสถิติในรูปแบบของค่าที่มนุษย์สามารถอ่านได้ |
| **-l, -loops <COUNT>**| ใช้เพื่อระบุจำนวนลูปสูงสุด |
| **-f, -family <FAMILY>**| ใช้เพื่อกำหนดตระกูลโปรโตคอล ตัวระบุตระกูลโปรโตคอลเหล่านี้อาจเป็น inet, inet6, bridge, ipx, dnet, mpls หรือ link ทางลัดต่อไปนี้ใช้สำหรับตระกูลโปรโตคอล ใช้เพื่อกำหนดตระกูลโปรโตคอล |
|                  | ตัวระบุโปรโตคอลเหล่านี้อาจเป็น:    |
|                  | -4: ใช้สำหรับ inet                   |
|                  | -6: ใช้สำหรับ inet6                  |
|                  | -B: ใช้สำหรับบริดจ์               |
|                  | -D: ใช้สำหรับ decnet               |
|                  | -I: ใช้สำหรับ ipx                  |
|                  | -M: ใช้สำหรับ mpls                    |
|                  | -0: ใช้สำหรับลิงก์                  |
| **-o, -oneline**| ใช้เพื่อแสดงแต่ละระเบียนในบรรทัดเดียว โดยจะแทนที่ช่องบรรทัดด้วยอักขระแบ็กสแลช '\' มันมีประโยชน์สำหรับการนับบันทึกด้วยคำสั่ง wc และ grep |
| **-r, -resolve**| มันถูกระบุเมื่อเราต้องการใช้ตัวแก้ไขชื่อของระบบเพื่อพิมพ์ชื่อ DNS แทนที่จะเป็นที่อยู่โฮสต์|
| **-n, -netns <NETNS>**| ใช้เพื่อสลับ IP เป็น NETNS ที่ระบุ (เนมสเปซเครือข่าย) |
| **-a หรือ -all**| ใช้เพื่อดำเนินการคำสั่งที่กำหนดกับวัตถุทั้งหมด |
| **-c, -color**| ใช้เพื่อแสดงเอาต์พุตสี |
| **-t, -timestamp**| ใช้เพื่อแสดงเวลาปัจจุบัน |
| **-rc, -rcvbuf<SIZE>**| ใช้เพื่อตั้งค่าซ็อกเก็ต Netlink เพื่อรับขนาดบัฟเฟอร์ ค่าเริ่มต้นคือ 1MB |
| **-iec**| ใช้เพื่อแสดงอัตราที่มนุษย์อ่านได้ในหน่วย IEC (เช่น 1Ki = 1,024) |
| **-br,-brief**| ใช้เพื่อแสดงเฉพาะข้อมูลที่จำเป็นในรูปแบบตารางเพื่อให้อ่านง่ายขึ้น |

## IP Command in Linux Basic

### Permanently Configure Static IP Address
เพื่อกำหนดที่อยู่ IP แบบคงที่ในระบบที่ใช้งานเบื้องต้นของ Debian-based distributions เช่น Debian, Ubuntu, และ Mint 
จะต้องแก้ไขหรืออัปเดตไฟล์การกำหนดค่าอินเตอร์เฟซเครือข่ายที่ /etc/network/interfaces เพื่อทำการเปลี่ยนแปลงอย่างถาวรตามตัวอย่างด้านล่าง:
```bash
$ sudo nano /etc/netplan/00-installer-config.yaml [On Ubuntu Linux]
```
ในไฟล์ netplan configuration, จะเห็นการกำหนดค่าของอินเตอร์เฟซเครือข่าย ซึ่งอาจมีลักษณะเป็นประมาณนี้:
```bash
  network:
    version: 2
  ethernets:
    ens33:
      dhcp4: true
      optional: true
```
>
เพื่อกำหนดที่อยู่ IP แบบคงที่, ต้องเปลี่ยน dhcp4 เป็น false และระบุที่อยู่ IP และnetmaskด้วย โดยมีรูปแบบเช่นนี้:
```bash
network:
  version: 2
  ethernets:
    ens33:
      dhcp4: false
      addresses: [Your ip addr /netmask]
      gateway4: 192.168.1.1
      nameservers:
        addresses: [8.8.8.8, 8.8.4.4]
```
ใช้คำสั่งต่อไปนี้เพื่อเปิดใช้งานการกำหนดค่าเครือข่ายใหม่
```bash
$ sudo netplan apply
```
> ชื่อและโครงสร้างที่แตกต่างกัน ใน Ubuntu, ไฟล์การกำหนดค่าเครือข่ายอยู่ใน /etc/netplan/ และมักจะมีชื่อเป็น 01-netcfg.yaml หรือ 50-cloud-init.yaml หรือชื่ออื่น ๆ ขึ้นอยู่กับการติดตั้งและการกำหนดค่าของระบบ
สำหรับการกำหนดที่อยู่ IP แบบคงที่ใน Ubuntu คุณสามารถสร้างไฟล์ .yaml ใหม่ใน /etc/netplan/ โดยใช้ชื่ออะไรก็ได้ตามความเหมาะสม เช่น my-network-config.yaml หรืออื่น ๆ แล้วนำเข้ารูปแบบการกำหนดค่าเครือข่ายลงไปในไฟล์นั้น

### Temporary Configure Static IP Address in Linux
สำหรับการกำหนดค่าเครือข่ายชั่วคราว (temporary network configurations) ใน Linux คุณสามารถใช้คำสั่ง ip เพื่อกำหนดที่อยู่ IP 
สำหรับอินเตอร์เฟซที่กำหนดให้ (เช่น eth1) ได้ทันที โดยไม่ต้องการการกำหนดค่าในไฟล์การกำหนดค่าเครือข่าย เช่นเดียวกับตัวอย่างคำสั่งด้านล่าง:
```bash
$ sudo ip add add 172.19.1.10/24 dev eth1
```
or
```bash
$ sudo ip addr add 172.19.1.10/24 dev eth1
```
> การตั้งค่าทั้งหมดเหล่านี้จะหายไปหลังจากการรีสตาร์ทระบบ

### Display All Network Interfaces
ในคำสั่ง ip, อ็อบเจ็กต์ link แทนอินเตอร์เฟซเครือข่าย โดยเราสามารถใช้คำสั่ง show เพื่อแสดงอินเตอร์เฟซเครือข่ายทั้งหมด
จะแสดงอินเตอร์เฟซเครือข่ายทั้งหมดโดยใช้คำสั่งต่อไปนี้:
```bash
ip link show
```
ตัวอย่างของผลลัพธ์ที่อาจจะได้รับเมื่อใช้คำสั่ง ```ip link show ```
```bash
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN mode DEFAULT group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
2: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP mode DEFAULT group default qlen 1000
    link/ether 52:54:00:12:34:56 brd ff:ff:ff:ff:ff:ff
3: wlan0: <BROADCAST,MULTICAST> mtu 1500 qdisc noop state DOWN mode DEFAULT group default qlen 1000
    link/ether 52:54:00:12:34:57 brd ff:ff:ff:ff:ff:ff
```

###  Check an IP Address of a Specific Network Interface
เพื่อให้ได้ข้อมูลละเอียดของอินเตอร์เฟซเครือข่ายแต่ละตัวใ ใช้คำสั่งต่อไปนี้:
```bash
$ ip link show Your interface name
```
เราใช้อ็อบเจ็กต์ link เพื่อแสดงข้อมูลinterfaceอย่างละเอียด แต่มันไม่แสดงที่อยู่ IP ที่เชื่อมโยงกับอินเตอร์เฟซเครือข่าย 
ในการแก้ไขปัญหานี้ เราสามารถใช้อ็อบเจ็กต์ addr ร่วมกับคำสั่ง ip เพื่อแสดงข้อมูลที่อยู่ IP ของinterfaceได้ สามารถใช้คำสั่งนี้:
```bash
$ ip addr show
```
ตัวอย่างของผลลัพธ์ที่อาจจะได้รับเมื่อใช้คำสั่ง ```ip addr show ```

```bash
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host 
       valid_lft forever preferred_lft forever
2: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 52:54:00:12:34:56 brd ff:ff:ff:ff:ff:ff
    inet 192.168.1.100/24 brd 192.168.1.255 scope global eth0
       valid_lft forever preferred_lft forever
    inet6 fe80::5054:ff:fe12:3456/64 scope link 
       valid_lft forever preferred_lft forever
```

เห็นได้ว่าผลลัพธ์ที่แสดงอย่างต่อเนื่องตอนนี้แสดงที่อยู่ IP ของทุกinterfaceพร้อมกับรายละเอียดอื่น ๆ อีกด้วย
ในการแสดงที่อยู่ IP ของแต่ละinterface แค่ต้องระบุชื่ออินเตอร์เฟซเครือข่ายเป็นargumentให้กับคำสั่งเท่านั้น
```bash
$ ip addr show Your interface name
```

### Display IP Address in Colored Output
สามารถเปิดใช้งานการแสดงผลที่เป็นสีได้ ตัวเลือกนี้จะเน้นข้อมูลสำคัญในสีที่แตกต่างกัน
ให้ใช้ตัวเลือก -c ของคำสั่งเพื่อแสดงผลลัพธ์ในสีต่าง ๆ:
```bash
$ ip -c addr show
```

### Remove an IP Address From the Network Interface
เราใช้คำสั่ง "add" เพื่อกำหนดที่อยู่ IP ในการใช้งาน เราสามารถใช้คำสั่งย่อย "del" เพื่อลบที่อยู่ IP ที่ระบุออกได้
คำสั่งต่อไปนี้จะลบที่อยู่ IP ที่กำหนดไว้จากอินเตอร์เฟซที่ระบุ (eth2):
```bash
# ip addr del 172.19.1.10/24 dev eth2
OR
$ sudo ip addr del 172.19.1.10/24 dev eth2
```

### Enable the Network Interface
“up” พร้อมกับชื่ออินเตอร์เฟซ (เช่น eth2) เป็นการเปิดใช้งานอินเตอร์เฟซเครือข่าย 
ตัวอย่างเช่น คำสั่งต่อไปนี้จะเปิดใช้งานinterface eth2:
ip link set eth2 up
```bash
# ip link set eth2 up
OR
$ sudo ip link set dev eth2 up
```
check status ของ eth2

ตัวอย่างของผลลัพธ์ที่อาจจะได้รับเมื่อใช้คำสั่ง ```$ ip -j -p link show eth2 | grep operstate ```
```bash
"operstate": "up",
```
## Soruce/Reference
(https://www.tecmint.com/ip-command-examples/)

(https://www.cyberciti.biz/faq/linux-ip-command-examples-usage-syntax/)

([https://www.tecmint.com/ip-command-examples/](https://www.ibm.com/docs/en/power9/0009-ESS?topic=notebook-setting-ip-address-in-linux)https://www.ibm.com/docs/en/power9/0009-ESS?topic=notebook-setting-ip-address-in-linux)
(https://www.geeksforgeeks.org/ifconfig-command-in-linux-with-examples/)
(https://www.linode.com/docs/guides/how-to-use-the-linux-ip-command/)
(https://www.javatpoint.com/linux-ip)
