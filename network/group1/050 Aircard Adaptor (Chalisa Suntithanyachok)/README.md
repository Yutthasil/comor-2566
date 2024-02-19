# Aircard Adaptor
## Aircard Adaptor คืออะไร
   Aircard เป็นอุปกรณ์ประเภทโมเด็มอย่างหนึ่งที่ใช้เชื่อมคอมพิวเตอร์เข้ากับเครือข่ายอินเตอร์เน็ตแบบไร้สายด้วยความเร็วสูงผ่านโครงข่ายสัญญาณโทรศัพท์มือถือ เช่น 3G, 4G, 5G, LTE อุปกรณ์ชนิดนี้มักจะเป็นการ์ดโมเด็มที่สามารถเสียบเข้ากับพอร์ต USB ของคอมพิวเตอร์ และใช้สัญญาณเครือข่ายโทรศัพท์เคลื่อนที่เพื่อเชื่อมต่อกับอินเทอร์เน็ตได้ แต่ยังมีรูปแบบอื่น ๆ ของ Aircard ที่อาจมีรูปร่างหรือขนาดที่แตกต่างกันไป อาทิเช่น มินิรูเตอร์หรือรูเตอร์พกพาที่ใช้สำหรับการเชื่อมต่ออินเทอร์เน็ตผ่าน Aircard ด้วยฟังก์ชันการส่งสัญญาณไร้สาย (Wi-Fi) 

   โดยมักจะใช้ในสถานที่ที่ไม่สามารถใช้งานอินเทอร์เน็ตผ่านเครือข่ายคงที่ได้ เช่น ที่บ้านนอกเมืองหรือในสถานที่ที่มีสัญญาณอินเทอร์เน็ตไม่เสถียร ด้วยความสามารถในการเชื่อมต่อผ่านเครือข่ายโทรศัพท์เคลื่อนที่ Aircard ช่วยเพิ่มความสะดวกสบายในการเชื่อมต่ออินเทอร์เน็ตในสถานการณ์ที่มีข้อจำกัดด้านการเชื่อมต่ออินเทอร์เน็ตอื่น ๆ ไม่สามารถทำได้

![image](https://github.com/LowEyeQ/Network-1/assets/109953773/2a64e543-b186-4e60-90a2-91b838c6ba90)



## ชื่อเรียกอื่นๆ ของ Aircard adaptor
โดยเป็นชื่อที่ใช้กันแพร่หลายในคอมมูของ linux 
* USB mobile broadband modem
* USB cellular modem
* Dongle

## คุณสมบัติของ Aircard Adaptor
1. รองรับเครือข่ายมือถือทั้ง 3G, 4G, และ 5G:
   Aircard สามารถใช้งานกับเครือข่ายมือถือทั้งหมดที่รองรับบน Linux รวมถึง 3G, 4G, และ 5G เพื่อให้ผู้ใช้สามารถเชื่อมต่ออินเทอร์เน็ตได้อย่างมีประสิทธิภาพในทุกสถานที่ที่มีการรับสัญญาณมือถือ
2. การรองรับแพลตฟอร์ม Linux:
   Aircard มักมาพร้อมกับไดรเวอร์ที่สามารถทำงานบนระบบปฏิบัติการ Linux ได้อย่างมีประสิทธิภาพ ซึ่งช่วยให้ผู้ใช้ Linux สามารถใช้งาน Aircard ได้อย่างราบรื่นโดยไม่มีปัญหาในด้านเชื่อมต่อและใช้งานได้อย่างลื่นไหล
3. ความสะดวกในการใช้งาน:
   Aircard มักมาพร้อมกับตัวอินเตอร์เฟซที่ใช้งานง่าย ผู้ใช้สามารถเสียบ Aircard เข้ากับพอร์ต USB ของคอมพิวเตอร์และเริ่มต้นใช้งานได้ทันที โดยไม่ต้องมีการติดตั้งซอฟต์แวร์หรือการกำหนดค่าซับเซตพิเศษเพิ่มเติม
4. ความเสถียร:
   มักมีการออกแบบให้มีความมั่นคงและเสถียรภาพสูง เพื่อให้ผู้ใช้สามารถใช้งานในสถานการณ์ที่ต้องการความเชื่อมต่ออินเทอร์เน็ตได้อย่างมีความมั่นใจ


## Aircard Adaopter ทำงานยังไง ?
การทำงานหลักๆ ของ Aircard คือการรับส่งข้อมูลระหว่างเครื่องคอมพิวเตอร์และเครือข่ายมือถือ ผ่านพอร์ต USB  ซึ่งจะใช้โปรโตคอลที่เหมาะสมเพื่อการเชื่มต่อเครือข่ายมือถือ เมื่อเชื่อมต่อเรียบร้อยแล้ว Aircard จะทำหน้าที่เป็นตัวกลางในการเชื่อมอินเตอร์เน็ตให้กับเครื่องคอมพิวเตอร์ ทำให้ผู้ใช้สามารถใช้อินเตอร์เน็ตได้ผ่าน Aircard เลย โดยไม่ต้องผ่านการใช้ wifi

## วิธีการเพิ่ม Aircccard Adaptor ใน linux
1. เสียบ Aircard เข้ากับพอร์ต USB:
   เริ่มต้นโดยการเสียบ Aircard เข้ากับพอร์ต USB ของคอมพิวเตอร์
   
2. ตรวจสอบว่า linux หา Aircard เจอหรือไม่:
   เมื่อเสียบ Aircard เข้ากับคอมพิวเตอร์ ลองรันคำสั่ง `lsusb` ใน Terminal เพื่อดูว่าระบบ Linux สามารถรับรู้ว่ามี Aircard หรือไม่ คำสั่งนี้จะแสดงรายชื่อของอุปกรณ์ USB ทั้งหมดที่เชื่อมต่ออยู่

ตัวอย่างการรันคำสั่ง `lsusb`
   ```
Bus 002 Device 001: ID 1d6b:0003 Linux Foundation 3.0 root hub
Bus 001 Device 006: ID 0cf3:e009 Qualcomm Atheros Communications 
Bus 001 Device 005: ID 04f2:b571 Chicony Electronics Co., Ltd 
Bus 001 Device 004: ID 138a:0017 Validity Sensors, Inc. 
Bus 001 Device 003: ID 8087:0a2b Intel Corp. 
Bus 001 Device 002: ID 04f2:b56f Chicony Electronics Co., Ltd 
Bus 001 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub
```
* แต่ละบรรทัดแสดงข้อมูลของอุปกรณ์ที่เชื่อมต่อผ่านพอร์ต USB
* แต่ละบรรทัดมีรหัสที่แสดงสถานะของอุปกรณ์ เช่น "Bus" และ "Device"
* รหัส "ID" บอกถึง Vendor ID และ Product ID ของอุปกรณ์
* บางครั้งอาจมีคำอธิบายเพิ่มเติมเกี่ยวกับอุปกรณ์ เช่น รายละเอียดของอุปกรณ์หรือชื่อผู้ผลิต
* สามารถใช้ข้อมูลนี้เพื่อตรวจสอบว่า Aircard หรืออุปกรณ์ USB cellular modem ได้รับการรับรู้แล้วหรือไม่

3. ติดตั้งไดรเวอร์ (ถ้าจำเป็น):
โดยส่วนมากแล้ว driver จะถูกติดตั้งมาโดยอัตโนมัติอยู่แแล้ว แต่มีในบางกรณีอาจจะต้องติดตั้ง driver เสริมสำหรับ aircard โดยอาจจะต้องดาวโหลน์และติดตั้งแยกต่างหากจากเว็บไซต์ของผู้ผลิต

4. กำหนดค่าเครือข่าย (ถ้าจำเป็น):
หลังจากที่ระบบ Linux รับรู้ Aircard แล้วต้องกำหนดค่าเครือข่ายเพื่อให้ Aircard สามารถเชื่อมต่อกับอินเทอร์เน็ตได้ สำหรับบางระบบ Linux ระบบจะทำการตรวจจับและกำหนดค่าเครือข่ายโดยอัตโนมัติ ในขณะที่บางระบบอื่นอาจต้องทำการกำหนดค่าเครือข่ายด้วยตนเอง โดยใช้เครื่องมือเช่น Network Manager หรือการกำหนดค่าแบบ Command Line

ตัวอย่างโค้ดสำหรับการตั้งค่าเครือข่ายเอง
   ```
import subprocess

def configure_network(interface, ip_address, subnet_mask, gateway):
    try:
        # สร้างคำสั่งสำหรับกำหนด IP address, subnet mask, และ gateway ให้กับ interface
        command = f"sudo ifconfig {interface} {ip_address} netmask {subnet_mask} up"
        subprocess.run(command.split(), check=True)

        # กำหนด default gateway
        command = f"sudo route add default gw {gateway} {interface}"
        subprocess.run(command.split(), check=True)

        print("Network configuration successful!")
    except subprocess.CalledProcessError as e:
        print(f"Error: {e}")

# ตัวอย่างการใช้งานฟังก์ชัน configure_network
interface = "eth0"  # ชื่อของ interface (เช่น eth0, wlan0)
ip_address = "192.168.1.100"  # IP address ที่ต้องการกำหนด
subnet_mask = "255.255.255.0"  # Subnet mask
gateway = "192.168.1.1"  # Default gateway

configure_network(interface, ip_address, subnet_mask, gateway)
```
* รันโปรแกรมด้วยสิทธิ์ของผู้ใช้ root หรือผู้ใช้ที่มีสิทธิ์การใช้ sudo เพื่อทำการกำหนดค่าเครือข่าย
* แทนที่ค่าของ interface, ip_address, subnet_mask, และ gateway ด้วยค่าที่เหมาะสมสำหรับเครือข่ายของ
* การใช้ subprocess.run() ด้วย check=True จะทำให้โปรแกรมระงับการทำงานและแสดงข้อผิดพลาดหากคำสั่งไม่สำเร็จ

5. ทดสอบการเชื่อมต่อ:
ลองเปิดเบราว์เซอร์หรือทดสอบการเชื่อมต่ออินเทอร์เน็ตเพื่อตรวจสอบว่า Aircard ทำงานได้ถูกต้องหรือไม่

## คำสั่งต่างๆ ที่เกี่ยวข้องกับ Aircard Adaptor 
|**Argument**	 | **Description** | 
| :-------- | :------- | 
| **lsusb** | ใช้สำหรับแสดงรายการของอุปกรณ์ USB ที่เชื่อมต่อ |
|**ifconfig**|ใช้สำหรับแสดงข้อมูลอินเทอร์เฟซที่เกี่ยวข้องกับ Aircard adapter|
|**iwconfig**|กำหนดค่าและแสดงข้อมูลเกี่ยวกับอินเทอร์เฟซไร้สาย (Wireless) |
|**ifup / ifdown**|ใช้เปิดหรือปิดอินเทอร์เฟซเครือข่าย ซึ่งสามารถใช้กับ Aircard adapter ได้เช่นกัน|
|**ip:**|จัดการเครือข่าย IP ซึ่งสามารถใช้ในการกำหนดค่า IP address, subnet mask, gateway, และการเชื่อมต่อสื่อสารระหว่างเครื่องแม่ข่ายและอุปกรณ์อื่น ๆ|
|**modprobe / rmmod:**|ใช้ในการจัดการกับไดรเวอร์ Aircard adapter|
|**wvdial:**|เป็นการใช้งานในโหมด dial-up สามารถใช้ wvdial ในการกำหนดค่าและสร้างการเชื่อมต่อ.|


คำสั่งเหล่านี้จะช่วยให้จัดการ Aircard Adaptor ได้อย่างมีประสิทธิภาพและง่ายดายขึ้น โดยแนะนำให้ผู้ใช้ดูเอกสารคู่มือหรือคำสั่งช่วยเพิ่มเติมได้จากเว็บไซต์ของผู้จำหน่าย Aircard Adaptor 

อีกสิ่งที่ควรพิจารณาคือการใช้ NetworkManager หรือ netplan เพื่อกำหนดการเชื่อมต่อและการตั้งค่าเครือข่ายให้กับ Aircard adapter ใน Linux โดย NetworkManager เป็นเครื่องมือจัดการเครือข่ายแบบกราฟิกที่ใช้กันอย่างแพร่หลาย ส่วน netplan เป็นเครื่องมือที่ใช้กับระบบปฏิบัติการ Ubuntu เพื่อกำหนดค่าเครือข่ายในรูปแบบ YAML configuration files โดยการใช้เครื่องมือเหล่านี้จะช่วยให้กำหนดค่าเครือข่ายและการเชื่อมต่อ Aircard adaptor ได้อย่างง่ายดายและสะดวกมากขึ้น คำสั่งที่ใช้กันอย่างแพร่หลายเมื่อต้องการกำหนดค่าเครือข่ายเช่น ip หรือ ifconfig ก็ยังคงใช้งานได้ เฉพาะในบางกรณีที่ต้องการการกำหนดค่าและการจัดการระดับเสถียรมากขึ้นสามารถพิจารณาเลือกใช้ NetworkManager หรือ netplan ได้ตามความเหมาะสม


ตัวอย่าง Output ของคำสั่ง `ifconfig`
 ```
ifconfig
ifconfig eth0 up
ifconfig eth0 192.168.1.2 netmask 255.255.255.0
route add default gw 192.168.1.1
ifconfig eth0
```


ตัวอย่าง Output ของคำสั่ง `iwconfig` ที่แสดงข้อมูลเกี่ยวกับอินเทอร์เฟซ
 ```
iwconfig wlan0

##ตัวอย่าง Output
wlan0     IEEE 802.11  ESSID:"Your_Network_Name"
          Mode:Managed  Frequency:2.412 GHz  Access Point: 00:11:22:33:44:55
          Bit Rate=54 Mb/s   Tx-Power=20 dBm
          Retry short limit:7   RTS thr:off   Fragment thr:off
          Power Management:off
          Link Quality=50/70  Signal level=-60 dBm
          Rx invalid nwid:0  Rx invalid crypt:0  Rx invalid frag:0
          Tx excessive retries:0  Invalid misc:0   Missed beacon:0
```



ตัวอย่าง Output ของคำสั่ง `ip addr show` เพื่อดูข้อมูลเกี่ยวกับอินเทอร์เฟซทั้งหมด รวมทั้ง Aircard ด้วย
 ```
ip addr show

##ตัวอย่าง Output
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host 
       valid_lft forever preferred_lft forever
2: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc pfifo_fast state UP group default qlen 1000
    link/ether 00:00:00:00:00:00 brd ff:ff:ff:ff:ff:ff
    inet 192.168.1.2/24 brd 192.168.1.255 scope global dynamic eth0
       valid_lft 42555sec preferred_lft 42555sec
    inet6 fe80::223:4eff:fe7d:3b0c/64 scope link 
       valid_lft forever preferred_lft forever
3: wlan0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc mq state UP group default qlen 1000
    link/ether 00:00:00:00:00:00 brd ff:ff:ff:ff:ff:ff
    inet 192.168.1.3/24 brd 192.168.1.255 scope global dynamic wlan0
       valid_lft 42555sec preferred_lft 42555sec
    inet6 fe80::223:4eff:fe7d:3b0d/64 scope link 
       valid_lft forever preferred_lft forever
4: ppp0: <POINTOPOINT,MULTICAST,NOARP,UP,LOWER_UP> mtu 1500 qdisc pfifo_fast state UNKNOWN group default qlen 3
    link/ppp 
    inet 10.20.30.40 peer 50.60.70.80/32 scope global ppp0

```

![image](https://github.com/LowEyeQ/Network-1/assets/109953773/b2a3b77a-e342-46ec-bfad-32bcc0ec55dc)


## ตัวอย่าง modem ที่รองรับการทำงานร่วมกับ linux ของ netgear
|**Modem Type**	 | **CDMA** | **GSM/UMTS** | 
| :-------- | :------- | :------- | 
| **AirCards** | AirCard 580, AirCard 595, AirCard 597E, AirCard 402 | AirCard 501, AirCard 875, AirCard 88x, AirCard 88xE|
|**USB modems**| AirCard 595U, Compass 597, USB 598, AirCard 250U*| AirCard 875U, AirCard 88xU, Compass 885/888/889, USBconnect 881, Mercury |



## Networkmanager เกี่ยวข้องกับ aircard ยังไง?
NetworkManager เป็นเครื่องมือในระบบปฏิบัติการ Linux ที่ใช้ในการจัดการการเชื่อมต่อเครือข่าย โดย NetworkManager จะช่วยในการตรวจจับ Aircard และการตั้งค่าการเชื่อมต่อให้ตรงตามความเหมาะสม รวมทั้งสามารถตั้งค่าและจัดการการเชื่อมต่อเครือข่ายอื่น ๆ ได้อีกด้วย เช่น Wi-Fi หรือ Ethernet.

## คำสั่งของ Networkmanager

ดังนั้น NetworkManager เป็นเครื่องมือที่สำคัญสำหรับการใช้งาน Aircard และช่วยให้ผู้ใช้งานสามารถจัดการและเชื่อมต่อกับเครือข่าย mobile broadband ได้อย่างมีประสิทธิภาพและง่ายดาย.

|**Argument**	 | **Description** | 
| :-------- | :------- | 
| **nm-applet:** | แอปพลิเคชันกราฟิกสำหรับการจัดการเครือข่าย โดยสามารถใช้งานผ่าน GUI  สามารถใช้งานผ่านการคลิกขวาที่ไอคอน NetworkManager บนแถบเครื่องมือหรือแถบระบบของเครื่อง Linux เพื่อทำการเชื่อมต่อ Aircard |
|**nmcli:**|ใช้ในการจัดการกับไดรเวอร์ Aircard adapter|

ตัวอย่าง Output ของคำสั่ง `nmcli:` ที่เกี่ยวข้องกับการใช้งาน Aircard
 ```
DEVICE   TYPE      STATE         CONNECTION
eth0     ethernet  connected     Wired connection 1
wlan0    wifi      connected     My_WiFi_Network
wwan0    gsm       disconnected  --

```


## Reference
* https://www.aunbangpo.com/a_10806_7374_%E0%B9%81%E0%B8%AD%E0%B8%A3%E0%B9%8C%E0%B8%81%E0%B8%B2%E0%B8%A3%E0%B9%8C%E0%B8%94-%28Aircard%29-%E0%B8%84%E0%B8%B7%E0%B8%AD%E0%B8%AD%E0%B8%B0%E0%B9%84%E0%B8%A3%3F.htm
* https://kb.netgear.com/22827/Can-I-use-my-NETGEAR-AirCard-modem-on-a-Linux-operating-system-v-1-7-40
* https://wiki.archlinux.org/title/NetworkManager#Use_dispatcher_to_connect_to_a_VPN_after_a_network_connection_is_established
* https://kb.netgear.com/22869/Can-I-use-a-NETGEAR-AirCard-Modem-on-Linux-Machines-direct-IP-modems

