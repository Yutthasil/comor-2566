
# ・✦ʚ DNS ɞ✦・
 

## บทบาทหน้าที่

ในระบบ Linux DNS มีบทบาทสำคัญในการช่วยให้network system ทำงานได้อย่างมีประสิทธิภาพและเป็นระบบ นี่คือบทบาทหลัก ๆ ของ DNS ในระบบ Linux:

1. **การแปลงชื่อ domain  (Name Resolution):** แปลงชื่อ domain  (Domain Name) เป็น IP address  (Internet Protocol) ซึ่งเป็นตัวระบุที่ใช้ในการติดต่อกับเครื่องคอมพิวเตอร์ใน network  เมื่อผู้ใช้พิมพ์ URL ใน web browser  DNS จะช่วยแปลง URL นั้นเป็น IP address  เพื่อให้สามารถเข้าถึงเว็บไซต์ได้

2. **การแก้ไขความล่าช้า (Caching):** DNS บน Linux มีระบบ caching ที่ช่วยลดความล่าช้าในการตอบสนอง เมื่อระบบได้ทำการแปลงชื่อ domain เป็น IP address  แล้ว ข้อมูลนี้จะถูกเก็บไว้ในแคช (cache) เพื่อให้การเข้าถึง domain นั้นๆ ในครั้งถัดไปเป็นไปอย่างรวดเร็ว

3. **การจัดการ domain  (Domain Management):** DNS ใน Linux ให้บริการในการจัดการ domain  ซึ่งรวมถึงการกำหนดค่า DNS records เพื่อกำหนดความเชื่อถือและการทำงานของ domain นั้น ๆ นอกจากนี้ มันยังเป็นส่วนสำคัญในการดำเนินการการลงทะเบียน domain  (domain registration)

4. **การทำงานเป็น DNS Server:** บน Linux BIND เป็นโปรแกรมที่ใช้เป็น DNS server และมีบทบาทในการให้บริการตอบสนองต่อคำถาม DNS จากเครื่องลูกของ network 

5. **การปรับแต่งความปลอดภัย:** DNS มีบทบาทในการควบคุมความเข้าถึงและความปลอดภัยของระบบ การตั้งค่า DNS Security Extensions (DNSSEC) สามารถช่วยป้องกันการโจมตีแบบ DNS spoofing และ DNS cache poisoning

ดังนั้น การทำหน้าที่ของ DNS ในระบบ Linux ไม่เพียงแค่การแปลงชื่อ domain แต่ยังเกี่ยวข้องกับการจัดการ domain การทำงานเป็น DNS server และการปรับแต่งความปลอดภัยของระบบ

## พื้นฐานและหลักการทำงาน
DNS (Domain Name System) เป็นระบบที่ใช้แปลงชื่อ domain เป็น IP address  และมีบทบาทสำคัญในการทำงานของ network นี่คือพื้นฐานและหลักการทำงานของ DNS ในระบบ Linux:

### 1. พื้นฐาน DNS:

#### 1.1 โครงสร้างชื่อ domain :
   - **Top-Level Domain (TLD):** ส่วนท้ายของชื่อ domain  เช่น .com, .org, .net
   - **Second-Level Domain (SLD):** ชื่อหลักของ domain  เช่น example
   - **Subdomain:** ชื่อที่ถูกเพิ่มเข้าไปเทียบกับ SLD เพื่อสร้างโครงสร้างหลายระดับ เช่น www.example.com

#### 1.2 DNS Records:
   - **A (Address) Record:** ระบุ IP address  สำหรับ domain หรือ subdomain
   - **CNAME (Canonical Name) Record:** สร้างชื่อทางอิเล็กทรอนิกส์ทาง domain 
   - **MX (Mail Exchange) Record:** ระบุเซิร์ฟเวอร์ที่รับอีเมลสำหรับ domain 
   - **NS (Name Server) Record:** ระบุชื่อเซิร์ฟเวอร์ DNS ที่ให้บริการสำหรับ domain 
   - **PTR (Pointer) Record:** ใช้สำหรับการแปลง IP address  เป็นชื่อ domain 

### 2. หลักการทำงาน DNS:

#### 2.1 การแปลงชื่อ domain :
   - เมื่อคำขอการแปลงชื่อ domain ถูกส่งมายัง DNS resolver (หรือ DNS client), resolver จะทำการสืบค้นข้อมูลจาก local cache ก่อนเพื่อดูว่ามีข้อมูลนี้อยู่แล้วหรือไม่
   - หากไม่พบข้อมูลใน local cache, resolver จะทำการสอบถาม root DNS server เพื่อหาข้อมูลเกี่ยวกับ TLD

#### 2.2 การสืบค้นแบบต่อเนื่อง:
   - Root DNS server จะตอบกลับด้วยข้อมูลเกี่ยวกับ TLD DNS server (e.g., .com DNS server)
   - Resolver จะสอบถาม TLD DNS server เพื่อหาข้อมูลเกี่ยวกับ SLD
   - กระบวนการนี้จะทำให้ resolver ไปสอบถาม authoritative DNS server ของ domain นั้นๆ

#### 2.3 การแก้ไขความล่าช้า:
   - เมื่อ resolver ได้ข้อมูลจาก authoritative DNS server ข้อมูลนี้จะถูกเก็บไว้ใน local cache เพื่อให้การสืบค้นในครั้งถัดไปเป็นไปอย่างรวดเร็ว

#### 2.4 DNS Server:
   - บนระบบ Linux, BIND (Berkeley Internet Name Domain) เป็นโปรแกรมที่ใช้เป็น DNS server
   - BIND มีหน้าที่รับคำขอและตอบสนองต่อการแปลงชื่อ domain 

#### 2.5 DNSSEC:
   - DNS Security Extensions (DNSSEC) เป็นโปรโตคอลที่ใช้เพิ่มความปลอดภัยในการสื่อสารระหว่าง resolver และ authoritative DNS server โดยเพิ่มลายเซ็นในข้อมูล DNS

การทำงานของ DNS ใน Linux มีกระบวนการทำงานเหล่านี้เพื่อให้ network system สามารถใช้งานได้ดี และเพื่อลดความล่าช้าในการสืบค้นข้อมูล


## DNS ทำงานยังไง

เมื่อไคลเอ็นต์ (เช่น  web browser ) ต้องการข้อมูลจาก name server  มันจะเชื่อมต่อกับ port  53 จากนั้น name server จะทำการแปลชื่อที่ร้องขอ (เช่น ชื่อ domain ) ให้เป็นข้อมูลที่ต้องการ

นึกภาพง่ายๆ ว่าชื่อ domain เหมือนชื่อเล่นของเว็บไซต์ ส่วนข้อมูลที่ต้องการอาจจะเป็น IP address  หรือข้อมูลอื่นๆ ของเว็บไซต์นั้น  web browser ไม่สามารถเข้าถึงข้อมูลโดยตรงด้วยชื่อเล่น มันต้องรู้ข้อมูลที่ถูกต้องก่อน จึงจะสามารถเชื่อมต่อและแสดงเว็บไซต์ให้ได้

เมื่อพิมพ์ชื่อ domain ลงใน web browser   web browser จะติดต่อกับ name server  (เหมือนกับสมุดโทรศัพท์ของอินเตอร์เน็ต) โดยใช้ port  53  name server จะค้นหาข้อมูลที่เกี่ยวข้องกับชื่อ domain นั้น และส่งกลับไปให้ web browser

ดังนั้น  port  53 จึงเป็นส่วนสำคัญที่ทำให้สามารถท่องเว็บไซต์ต่างๆ ได้อย่างสะดวกโดยไม่ต้องจำข้อมูลที่ซับซ้อน


![alt text](https://www.redhat.com/sysadmin/sites/default/files/styles/embed_large/public/2021-08/Screen%20Shot%202021-08-10%20at%203.30.51%20PM.png?itok=JajROO06)
source : https://www.redhat.com/

1. การส่งคำขอจากไคลเอ็นต์ DNS ไปยังเซิร์ฟเวอร์ DNS เรียกว่า **คำขอค้นหา (lookup request)**
2. การได้รับการตอบกลับจากเซิร์ฟเวอร์ DNS ไปยังไคลเอ็นต์ DNS เรียกว่า **การตอบสนองค้นหา (lookup response)**
3. ระบบที่กำหนดค่าบริการ DNS เรียกว่า **DNS server**
4. ระบบที่เข้าถึงเซิร์ฟเวอร์ DNS เรียกว่า **DNS client**

## DNS เอา ip address มาจากที่ไหน

กระบวนการทำงานของ DNS อธิบายวิธีการสื่อสารภายใน DNS และวิธีการแก้ไขที่อยู่เหล่านี้
![alt text](https://www.redhat.com/sysadmin/sites/default/files/styles/embed_large/public/2021-08/Screen%20Shot%202021-08-10%20at%203.31.08%20PM.png?itok=mVw21968)

source : https://www.redhat.com/


* เมื่อ client ค้นหา domain  www.example.com คำขอจะส่งไปยังตัวแก้ปัญหาของผู้ให้บริการอินเตอร์เน็ต (ISP) เป็นขั้นแรก ตัวแก้ปัญหาจะตอบสนองต่อคำขอของผู้ใช้ในการแปลชื่อ domain 

* หากไม่พบ IP address ใน resolver คำขอจะถูกส่งต่อไปยังเซิร์ฟเวอร์ DNS ราก (root DNS server) และต่อมาไปยังเซิร์ฟเวอร์ domain ระดับบนสุด (TLD)

* เซิร์ฟเวอร์ TLD จัดเก็บข้อมูลสำหรับ domain ระดับบนสุด เช่น .com หรือ .net

* คำขอจะถูกส่งต่อมายัง name server  ซึ่งทราบข้อมูลโดยละเอียดเกี่ยวกับ domain และ IP address

* name server ตอบกลับไปยังตัวแก้ปัญหาของ ISP จากนั้นตัวแก้ปัญหาตอบกลับไปยังไคลเอ็นต์ด้วย IP ที่ร้องขอ

* เมื่อตัวแก้ปัญหาไม่ทราบ IP มันจะเก็บ IP และ domain นั้นไว้ในแคชเพื่อรองรับการค้นหาในอนาคต

## Install and configure DNS
BIND คือบริการ name server ที่ทำหน้าที่แปลงชื่อ domain เป็น IP address บนเซิร์ฟเวอร์ DNS ที่ใช้ระบบ Linux โดยทั่วไป BIND เป็นซอฟต์แวร์ฟรีและโอเพนซอร์สที่ได้รับความนิยมสูง มีการใช้งานอย่างแพร่หลาย เนื่องจากมีความเสถียรภาพ ปลอดภัย และมีชุมชนผู้ใช้งานขนาดใหญ่ที่คอยสนับสนุน

```
[root@servera ~] # yum install bind
```
แพคเกจ BIND มอบ named service ซึ่งจะอ่านการกำหนดค่าจากไฟล์ /etc/named และ /etc/named.conf  หลังจากติดตั้งแพคเกจนี้ สามารถเริ่มกำหนดค่า DNS ได้เลย

## Configure the /etc/named.conf file
ก่อนอื่นให้เพิ่มหรือแก้ไขค่าสองอย่างใน options field หนึ่งคือ DNS server address และอีกหนึ่งคือการกำหนดค่า allow-query เป็น any (อนุญาตให้สอบถามจากทุกที่)

```
[root@servera ~] # vim /etc/named.conf
listen-on port 53 { 127.0.0.1; 192.168.25.132; };
allow-query { localhost; any; };
```

นี่คือค่าจากไฟล์ด้านบน:

* 192.168.25.132 - ที่อยู่เซิร์ฟเวอร์ DNS
* any - ตรงกับทุก IP address 

## Define the forward and reverse zones
กำหนดโซนการส่งต่อ (forward) และโซนการส่งกลับ (reverse) ในไฟล์ /etc/named.conf หรือ /etc/named.rfc1912.zones ในตัวอย่างนี้, กำลังเพิ่มรายละเอียดการกำหนดโซนลงในไฟล์ /etc/named.rfc1912.zones
```
[root@servera ~] # vim /etc/named.rfc1912.zones
  zone "example.com" IN { type master;
  file "example.forward.zone";
  allow-update { none; };
};

  zone "25.168.192.in-addr.arpa" IN { 
   type master;
   file "example.reverse.zone";
   allow-update { none; };
};
```
## Create forward and reverse zone files
การสร้างไฟล์โซนการส่งต่อ (forward) และการส่งกลับ (reverse) นั้นเป็นกระบวนการการกำหนดค่าเพื่อให้เซิร์ฟเวอร์ DNS ทราบถึงข้อมูลที่เกี่ยวข้องกับโซนนั้น ๆ บนระบบ
```
[root@servera ~] # vim /var/named/example.forward.zone
```
```
[root@servera ~] # vim /var/named/example.reverse.zone
```
## Add the nameserver IP to /etc/resolv.conf
การเพิ่ม IP address ของ name server  (nameserver) ลงในไฟล์ /etc/resolv.conf เป็นขั้นตอนที่สำคัญเพื่อกำหนด **DNS resolver** ที่จะใช้ในระบบ

ก่อนอื่นต้องปิดการประมวลผล DNS ที่ถูกทำโดย NetworkManager เนื่องจากมันจะอัปเดตไฟล์ /etc/resolv.conf โดยอัตโนมัติด้วยการตั้งค่า DNS จากโปรไฟล์การเชื่อมต่อที่ใช้งานอยู่ เพื่อปิดการใช้งานนี้และอนุญาตให้ทำการแก้ไข /etc/resolv.conf ด้วยวิธีด้วยตนเอง ต้องสร้างไฟล์ (เช่น 90-dns-none.conf) ในไดเรกทอรี /etc/NetworkManager/conf.d/ ที่มีเนื้อหาต่อไปนี้:
```
[main]
dns=none
```
save และ reload

```
# systemctl reload NetworkManager
```

หลังจาก reload NetworkManager, มันจะไม่อัพเดต /etc/resolv.conf. Now, สามารถ manually เพิ่ม nameserver's IP address to the /etc/resolv.conf file
```
[root@servera ~] # vim /etc/resolv.conf
# Generated by NetworkManager 
search localdomain example.com 
nameserver 192.168.25.132
```

## Start/restart and enable the named service
```
[root@servera ~] # systemctl status named.service
```
```
[root@servera ~] # systemctl start named.service
```
```
[root@servera ~] # systemctl enable named.service
```
```
[root@servera ~] # systemctl restart named.service
```

## ตรวจสอบค่า ip DNS ยังไง 

ip DNS สามารถตรวจสอบได้ด้วย command `cat /etc/resolv.conf` 

![alt text](https://github.com/LowEyeQ/Network-1/blob/main/088%20DNS%20Purin%20((%E2%80%A2%CB%8B%20_%20%CB%8A%E2%80%A2))/catetcresolv.conf.png?raw=true)

ip DNS จะอยู่ที่ **nameserver**

หรือ ใช้ command `nslookup` ตามด้วยชื่อ website

![alt text](https://github.com/LowEyeQ/Network-1/blob/main/088%20DNS%20Purin%20((%E2%80%A2%CB%8B%20_%20%CB%8A%E2%80%A2))/nslookup.png?raw=true)

ip DNS จะอยู่ที่ **server**

## การตรวจสอบว่า DNS ทำงานได้ไหม

สามารถทดสอบด้วยการ ping หรือ traceroute ไปที่ website

![alt text](https://github.com/LowEyeQ/Network-1/blob/main/088%20DNS%20Purin%20((%E2%80%A2%CB%8B%20_%20%CB%8A%E2%80%A2))/ping.png?raw=true)

จากรูปคือการ ping ไปที่ตัวเอง ถ้าเกิด ping สำเร็จ จะแปลงจากชื่อ domain name เป็น ip address ได้

## การตรวจสอบค่า hostname

ตรวจสอบ Hostname โดยใช้ command `hostname`
![alt text](https://github.com/LowEyeQ/Network-1/blob/main/088%20DNS%20Purin%20((%E2%80%A2%CB%8B%20_%20%CB%8A%E2%80%A2))/hostname..png?raw=true)
## ข้อควรระวัง
การแก้ไขการตั้งค่า DNS อาจต้องใช้สิทธิ์ root หรือสิทธิ์แอดมิน ดังนั้นควรระมัดระวังในการทำเพื่อป้องกันไม่ให้เกิดความผิดพลาดที่ไม่พึงประสงค์
## Reference

redhat

https://www.jodoi.com/book/network-command_3.pdf

แปลภาษาและข้อมูลเพิ่มเติม : chatGPT
