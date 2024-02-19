# Wireless Adapter
## Wireless Adapter คืออะไร
Wireless Adapter หรือ Wireless USB Adapter คืออุปกรณ์ที่ใช้สำหรับเชื่อมต่อกับเครือข่ายคอมพิวเตอร์แบบไร้สาย หรือเรียกง่าย ๆ ว่า ตัวรับสัญญาณไวไฟ จำเป็นต้องใช้งานกับจุดที่มีเราท์เตอร์ปล่อยสัญญาณไวไฟ เน้นใช้งานร่วมกับคอมพิวเตอร์ โดยวิธีการใช้งานเพียงแค่เชื่อมต่อผ่านพอร์ต USB ก็สามารถรับสัญญาณไวไฟได้ทันที ไม่สามารถปล่อยสัญญาณไปให้อุปกรณ์อื่น ๆ เป็นอุปกรณ์ที่มีขนาดเล็ก ใช้งานง่ายสำหรับพีซี แล็ปท็อป และอุปกรณ์อัจฉริยะต่าง ๆ เช่น ทีวี เครื่องควบคุมอุณหภูมิแบบตั้งโปรแกรมได้ กล้องวงจรปิด และอุปกรณ์ที่คล้ายกัน โดยจะประกอบด้วยเครื่องส่งสัญญาณไวไฟ หรือสัญญาณวิทยุ เมื่อทำการเชื่อมต่อแล้ว จะช่วยให้อุปกรณ์สามารถเชื่อมต่อแบบไร้สายกับอุปกรณ์อื่นหรืออินเทอร์เน็ตได้
  ______
Wireless USB Adapter สำหรับพีซีและอุปกรณ์ที่คล้ายกันเป็นอุปกรณ์ Plug-and-Play ที่เพียงแค่เสียบเข้ากับพอร์ตก็สามารถใช้งานได้ทั้ง Windows และ macOS ในเวอร์ชันปัจจุบันจะโหลดไดรเวอร์ที่จำเป็นอัตโนมัติ อุปกรณ์ USB ทั้งหมดนั้นเป็นแบบ Hot-swappable หมายความว่าสามารถเชื่อมต่อและยกเลิกการเชื่อมต่อได้โดยไม่ต้องรีบูตอุปกรณ์โฮสต์

![image](https://www.dlink.co.th/wp-content/uploads/2021/07/DWA-185-2.jpg) ![image](https://res.cloudinary.com/itcity-production/image/upload/f_jpg,q_80/v1651032195/product/product-master/cku9huiny6siibse8xm0.jpg)

(source : https://www.tp-link.com/ae/blog/378/what-is-a-wifi-adapter-and-how-to-pick-the-best-one-for-you-/#:~:text=A%20WiFi%20adapter%20allows%20your,to%20the%20latest%20WiFi%20generation.)

## Wireless Adapter เหมาะกับใคร
- **ใช้คอมพิวเตอร์รุ่นเก่าหรือ PC ประกอบเอง** ไม่มีการ์ด wifi ทำให้ไม่สามารถเชื่อมต่ออินเทอร์เน็ตได้ 
- **สัญญาณไวไฟค่อนข้างช้า** หากคอมพิวเตอร์เชื่อมต่อสัญญาณได้ แต่รู้สึกว่าสัญญาณช้ากว่าที่ควรจะเป็น อาจเป็นไปได้ว่าการ์ด wifi มีปัญหาหรืออยู่ห่างจากจุดปล่อยสัญญาณมากเกินไป อุปกรณ์นี้ช่วยให้การดึงสัญญาณไวไฟทำได้ดีขึ้น

## การตั้งค่า Wireless adapter บน Linux
   โดยการตั้งค่า Wireless adapter บน Linux จะเกี่ยวข้องกับหลายขั้นตอน โดยจะมีขั้นตอนการติดตั้งไดรเวอร์ การกำหนดการตั้งค่าเครือข่าย และการเชื่อมต่อกับเครือข่ายไร้สาย 
   1. **ระบุ Wireless Adapter** : จะใช้คำสั่ง **lspci** เพื่อแสดงรายการอุปกรณ์ PCI (Peripheral Component Interconnect) ทั้งหมดที่มีการเชื่อมต่อกับระบบ โดยรวมถึงอุปกรณ์ต่าง ๆ เช่น network adapters, graphics cards, sound cards, USB controllers และอื่นๆ 


ตัวอย่างผลลัพธ์ของ `lspci` :
```00:00.0 Host bridge: Intel Corporation Xeon E3-1200 v6/7th Gen Core Processor Host Bridge/DRAM Registers (rev 02)
00:02.0 VGA compatible controller: Intel Corporation HD Graphics 620 (rev 02)
00:14.0 USB controller: Intel Corporation Sunrise Point-LP USB 3.0 xHCI Controller (rev 21)
00:16.0 Communication controller: Intel Corporation Sunrise Point-LP CSME HECI #1 (rev 21)
00:1c.0 PCI bridge: Intel Corporation Sunrise Point-LP PCI Express Root Port #1 (rev f1)
...
```

หรือใช้คำสั่ง **lsusb** เพื่อแสดงรายการอุปกรณ์ USB ทั้งหมดที่เชื่อมต่อกับระบบ พร้อมด้วยรายละเอียด รวมถึง ID ผู้จำหน่าย ID ผลิตภัณฑ์ และข้อมูลอื่น ๆ ซึ่งจะมีประโยชน์ในการระบุอุปกรณ์ USB ที่เชื่อมต่อ การแก้ไขปัญหาที่เกี่ยวข้องกับ USB หรือการพิจารณาความเข้ากันได้ของอุปกรณ์

ตัวอย่างผลลัพธ์ของ `lsusb` :
```Bus 002 Device 001: ID 1d6b:0003 Linux Foundation 3.0 root hub
Bus 001 Device 005: ID 0bda:0129 Realtek Semiconductor Corp. RTS5129 Card Reader Controller
Bus 001 Device 004: ID 0cf3:e009 Qualcomm Atheros Communications 
Bus 001 Device 003: ID 0bda:568b Realtek Semiconductor Corp. Integrated_Webcam_HD
Bus 001 Device 002: ID 046d:c52b Logitech, Inc. Unifying Receiver
Bus 001 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub
```

   2. **ขั้นตอนติดตั้งไดรเวอร์**: Linux รุ่นใหม่ส่วนใหญ่มาพร้อมกับไดรเวอร์ที่หลากหลาย รวมถึงไดรเวอร์สำหรับ Wireless adapter ด้วย อย่างไรก็ตาม หากต้องใช้ไดรเวอร์ที่เป็นกรรมสิทธิ์ หรือหากไดรเวอร์เริ่มต้นทำงานได้ไม่ดี อาจจะต้องดาวน์โหลดหรือติดตั้งไดรเวอร์เพิ่มเติม
   3. **ขั้นตอนโหลดโมดูลไดรเวอร์**: เมื่อติดตั้งไดรเวอร์ที่เหมาะสมแล้ว อาจต้องโหลดโมดูลไดรเวอร์ลงในเคอร์เนล สามารถทำได้โดยใช้คำสั่ง `modprobe`
   ตัวอย่างเช่น: ```sudo modprobe <driver_module_name>```
   4. **ขั้นตอนตรวจสอบสถานะของอแด็ปเตอร์**: ใช้คำสั่ง **ip** หรือ **ifconfig** เพื่อตรวจสอบว่าอแด็ปเตอร์ไร้สายของคุณได้รับการยอมรับจากระบบหรือไม่ และใช้งานได้หรือไม่
   ตัวอย่างเช่น:

-- คำสั่ง **ip link show** ใช้เพื่อแสดงข้อมูลเกี่ยวกับอินเทอร์เฟซเครือข่าย โดยจะให้รายละเอียดเกี่ยวกับสถานะปัจจุบันและการกำหนดค่าของอินเทอร์เฟซเครือข่ายทั้งหมดในระบบ

ตัวอย่างผลลัพธ์ของ `ip link show` :
```
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN mode DEFAULT group default qlen 1000
   link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
2: enp0s25: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP mode DEFAULT group default qlen 1000
   link/ether f0:de:f1:9c:56:74 brd ff:ff:ff:ff:ff:ff
3: wlp3s0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc mq state UP mode DORMANT group default qlen 1000
   link/ether 48:5d:60:2a:ab:10 brd ff:ff:ff:ff:ff:ff
```

 `lo` คือ อินเทอร์เฟซแบบ loopback, `enp0s25` คือ อินเทอร์เฟซ Ethernet, `wlp3s0` คือ อินเทอร์เฟซ wireless

-- คำสั่ง **ifconfig** ใช้เพื่อกำหนดค่าและแสดงข้อมูลเกี่ยวกับอินเทอร์เฟซของเครือข่ายในระบบปฏิบัติการแบบ Unix , **-a** ใช้เพื่อแสดงข้อมูลเกี่ยวกับอินเทอร์เฟซทั้งหมด รวมถึงอินเทอร์เฟซที่ใช้งานไม่ได้ในปัจจุบัน
 
 ตัวอย่างผลลัพธ์ของ `ifconfig -a` :
```
enp0s3: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet 192.168.1.10  netmask 255.255.255.0  broadcast 192.168.1.255
        inet6 fe80::a00:27ff:fe74:8ca2  prefixlen 64  scopeid 0x20<link>
        ether 08:00:27:74:8c:a2  txqueuelen 1000  (Ethernet)
        RX packets 208332  bytes 279812907 (279.8 MB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 99644  bytes 7753682 (7.7 MB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

lo: flags=73<UP,LOOPBACK,RUNNING>  mtu 65536
        inet 127.0.0.1  netmask 255.0.0.0
        inet6 ::1  prefixlen 128  scopeid 0x10<host>
        loop  txqueuelen 1000  (Local Loopback)
        RX packets 17369  bytes 1428921 (1.4 MB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 17369  bytes 1428921 (1.4 MB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

```

ในตัวอย่างนี้ `enp0s3` อินเทอร์เฟซ Ethernet และ `lo` อินเทอร์เฟซแบบ loopback 

เอาต์พุตประกอบด้วยข้อมูล เช่น อินเทอร์เฟซ flag, ที่อยู่ IP (ทั้ง IPv4 และ IPv6), ที่อยู่ MAC, MTU (Maximum Transmission Unit) และ packet statistics.

   5. **ขั้นตอนกำหนดการตั้งค่าเครือข่าย**: สามารถกำหนดการตั้งค่าเครือข่ายได้ โดยใช้คำสั่ง เช่น `iw` หรือ `nmcli` เพื่อกำหนดการตั้งค่าเครือข่ายไร้สาย เช่น SSID และรายละเอียดการตรวจสอบสิทธิ์

   -- คำสั่ง **nmcli** เป็น command-line interface คำสั่งสำหรับ NetworkManager ซึ่งเป็นการจัดการการเชื่อมต่อเครือข่ายใน Linux `nmcli` ใช้เพื่อเชื่อมต่อกับเครือข่าย WiFi

สามารถใช้เพื่อเชื่อมต่อกับเครือข่าย Wi-Fi ด้วย SSID และรหัสผ่านที่ระบุได้ดังนี้:
   
```nmcli device wifi connect <SSID> password <password>```

แทนที่ <SSID> ด้วยชื่อ (SSID) ของเครือข่าย WiFi ที่ต้องการเชื่อมต่อ และ <password> ด้วยรหัสผ่านสำหรับเครือข่าย
คำสั่งนี้จะบอก NetworkManager ให้เชื่อมต่อกับเครือข่าย Wi-Fi ที่ระบุโดยใช้ SSID และรหัสผ่านที่ให้มา

-- คำสั่ง **iw** ใช้สำหรับการกำหนดค่าและการโต้ตอบกับอินเทอร์เฟซเครือข่ายไร้สาย ช่วยให้ผู้ใช้สามารถดำเนินการต่าง ๆ ได้ เช่น การสแกนหาเครือข่าย Wi-Fi ในบริเวณใกล้เคียง การกำหนดการตั้งค่าไร้สาย และตรวจสอบการเชื่อมต่อไร้สาย

ตัวอย่างผลลัพธ์ของ `iw` :

```
Wiphy phy0
        max # scan SSIDs: 4
        max scan IEs length: 2257 bytes
        max # sched scan SSIDs: 0
        max # match sets: 0
        max # scan plans: 1
        max scan plan interval: -1
        max scan plan iterations: 0
        Retry short limit: 7
        Retry long limit: 4
        Coverage class: 0 (up to 0m)
```

เอาต์พุตนี้ให้ข้อมูลเกี่ยวกับความสามารถของอุปกรณ์ไร้สาย phy0 เช่น จำนวน SSID สูงสุดที่สามารถสแกนได้ ความยาวสูงสุดขององค์ประกอบข้อมูล (IE) ในคำขอสแกน ขีดจำกัดการลองใหม่ และอื่น ๆ

หากต้องการใช้ `iw` อย่างมีประสิทธิภาพ จะต้องระบุคำสั่งย่อยและตัวเลือกตามงานเฉพาะที่ต้องการดำเนินการ เช่น การสแกนหาเครือข่าย (`iw dev wlan0 scan`) การกำหนดค่าพารามิเตอร์ไร้สาย (`iw dev wlan0 set ...`) หรือการมอนิเตอร์ การเชื่อมต่อไร้สาย (`iw dev wlan0 station dump`)
      
   6. **ขั้นตอนตรวจสอบการเชื่อมต่อ**: หลังจากกำหนดการตั้งค่าเครือข่ายแล้ว ให้ตรวจสอบว่าสามารถเชื่อมต่อกับเครือข่ายไร้สายได้หรือไม่ โดยสามารถใช้เครื่องมือ เช่น ping เพื่อทดสอบการเชื่อมต่อกับอุปกรณ์หรือเว็บไซต์อื่นๆ

      ตัวอย่างผลลัพธ์ของ `ping 8.8.8.8` :

```
PING 8.8.8.8 (8.8.8.8) 56(84) bytes of data.
64 bytes from 8.8.8.8: icmp_seq=1 ttl=117 time=11.1 ms
64 bytes from 8.8.8.8: icmp_seq=2 ttl=117 time=10.9 ms
64 bytes from 8.8.8.8: icmp_seq=3 ttl=117 time=11.0 ms
64 bytes from 8.8.8.8: icmp_seq=4 ttl=117 time=11.0 ms
```
      
   7. **ขั้นตอนการเชื่อมต่ออัตโนมัติ**: หากต้องการเชื่อมต่อกับเครือข่ายไร้สายโดยอัตโนมัติขณะบู๊ตเครื่อง สามารถกำหนดค่าตัวจัดการเครือข่ายให้บันทึกรายละเอียดการเชื่อมต่อได้ โดยวิธีนี้จะทำให้ระบบของเชื่อมต่อกับเครือข่ายไร้สายโดยอัตโนมัติเมื่อเริ่มทำงาน


   ใช้คำสั่ง `iw dev` ตรวจสอบชื่ออุปกรณ์เครือข่าย คำสั่งนี้จะให้ข้อมูลเกี่ยวกับอินเทอร์เฟซเครือข่ายไร้สายและสถานะปัจจุบัน โดยคำสั่งนี้จะใช้เพื่อแสดงรายละเอียดเกี่ยวกับอุปกรณ์ไร้สาย เช่น ชื่อ ที่อยู่ MAC โหมดไร้สายที่รองรับ และสถานะการเชื่อมต่อ
      ตัวอย่างผลลัพธ์ของ `iw dev` :

```
phy#0
	Interface wlan0
		ifindex 3
		wdev 0x1
		addr 12:34:56:78:9a:bc
		type managed
		channel 1 (2412 MHz), width: 20 MHz (no HT), center1: 2412 MHz
		txpower 20.00 dBm
```

`phy#0` คือ ฮาร์ดแวร์ไร้สาย (เลเยอร์ PHY)
`Interface wlan0` คือ อินเทอร์เฟซไร้สาย
`ifindex` คือ ดัชนีอินเทอร์เฟซ
`wdev` คือ ตัวระบุอุปกรณ์ไร้สาย
`addr` คือ ที่อยู่ MAC ของอินเทอร์เฟซ
`type` ระบุโหมดของอินเทอร์เฟซ (เช่น จัดการ มอนิเตอร์)
`channel` ระบุช่องการทำงานและความถี่
`txpower` คือ กำลังส่งของอินเทอร์เฟซ
  ______
หากต้องการแสกนหา Access Point ถ้า Access Point ที่เราจะเอา USB Wireless LAN ไปต่อนั้นมีการเข้ารหัสแบบ WPA/WPA2 เราจะต้องติดตั้ง wpa_supplicant เพิ่มเติมด้วย เพื่อทำหน้าที่เป็น WPA Client จะได้รองรับ WPA-PSK (WPA Personal) และ WPA2-PSK (WPA2 Personal) นอกจากนั้น wpa_supplicant ยังรองรับ WPA-EAP (IEEE 802.1X) ด้วย
ติดตั้ง wpa_supplicant รันคำสั่ง `apt-get install wpasupplicant` 

  ______
References:
* <a href="https://th.linux-console.net/?p=342" />https://th.linux-console.net/?p=342</a>
* <a href="https://www.tp-link.com/ae/blog/378/what-is-a-wifi-adapter-and-how-to-pick-the-best-one-for-you-/#:~:text=A%20WiFi%20adapter%20allows%20your,to%20the%20latest%20WiFi%20generation." />https://www.tp-link.com/ae/blog/378/</a>
* <a href="https://unix.stackexchange.com/questions/92799/connecting-to-wifi-network-through-command-line" />https://unix.stackexchange.com/questions/92799/</a>
* <a href="http://voip4share.com/topic3592.html" />http://voip4share.com/topic3592.html</a>





