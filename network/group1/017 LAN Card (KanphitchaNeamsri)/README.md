
# LAN Card
## LAN Card หรือ Network Interface Card [NIC]
    LAN Card: ย่อมาจาก Local Area Network Card : หมายถึง การ์ดเครือข่ายที่ใช้เทคโนโลยีอีเธอร์เน็ต (Ethernet ในการเชื่อมต่อกับเครือข่ายท้องถิ่น (LAN)) 
LAN Card เป็นประเภทหนึ่งของ NIC

    Network Interface Card (NIC) : หมายถึง การ์ดใดๆ ที่ทำหน้าที่เชื่อมต่อคอมพิวเตอร์กับเครือข่าย โดยไม่จำเป็นต้องระบุเทคโนโลยีที่ใช้ 
NIC เป็นคำศัพท์ทั่วไป หมายถึง การ์ดเครือข่ายทุกประเภท

    Ethernet Network Card : หมายถึง การ์ดเครือข่ายที่ใช้เทคโนโลยีอีเธอร์เน็ตในการเชื่อมต่อกับเครือข่าย ซึ่งเป็นเทคโนโลยีที่ใช้กันแพร่หลายที่สุดในปัจจุบัน

Ethernet Network Card = Network Interface Card (ที่ใช้เทคโนโลยีอีเธอร์เน็ต)

Network Interface Card ≠ Ethernet Network Card (NIC อาจใช้เทคโนโลยีอื่น เช่น Wi-Fi, Bluetooth)

## What is network interface card (NIC)?

Network Interface Card **ตัวกลางในการเชื่อมต่อระหว่างคอมพิวเตอร์ที่ใช้ Linux กับเครือข่ายข้อมูล ช่วยให้คอมพิวเตอร์สามารถระบุตัวตนและติดต่อสื่อสารกับอุปกรณ์อื่นๆ บนเครือข่ายได้** เป็นฮาร์ดแวร์ที่จำเป็นสำหรับคอมพิวเตอร์ในการเชื่อมต่อกับเครือข่าย เปรียบเสมือนบัตรประชาชนดิจิทัลที่ช่วยให้คอมพิวเตอร์สามารถระบุตัวตนและติดต่อสื่อสารกับอุปกรณ์อื่นๆ บนเครือข่ายได้ NIC มักถูกเรียกว่า Network Interface Controller (NIC), Network Adapter หรือ LAN Adapter


มีวัตถุประสงค์หลัก 2 ประการ:

1. รองรับการสื่อสารทั้งแบบมีสายและไร้สาย:

    - มีสาย: เชื่อมต่อผ่านสาย RJ-45 เข้ากับเครือข่าย LAN (Local Area Network) ภายในอาคาร
    - ไร้สาย: เชื่อมต่อผ่านสัญญาณวิทยุตามมาตรฐาน Wi-Fi (802.11b/g/n/ac)

1. อำนวยความสะดวกในการติดต่อสื่อสารระหว่างคอมพิวเตอร์บนเครือข่าย:
    - เชื่อมต่อคอมพิวเตอร์ภายใน LAN เพื่อแชร์ข้อมูลและทรัพยากร
    - เชื่อมต่อกับเครือข่ายอินเตอร์เน็ตโดยใช้โปรโตคอล IP (Internet Protocol)
    - ทำหน้าที่เป็นอุปกรณ์ชั้น Physical Layer และ Data Link Layer ในโมเดล OSI (Open Systems Interconnection) ช่วยแปลงสัญญาณข้อมูลและควบคุมการรับส่งระหว่างคอมพิวเตอร์กับอุปกรณ์อื่นๆ บนเครือข่าย

สรุปง่ายๆ คือ NIC ทำหน้าที่เป็นตัวกลางเชื่อมต่อคอมพิวเตอร์เข้ากับเครือข่าย ช่วยให้คอมพิวเตอร์สามารถสื่อสารและแชร์ข้อมูลกันได้ทั้งภายในเครือข่ายท้องถิ่นและอินเตอร์เน็ต

## Types of NIC Cards
1. **Internal Network Cards**
เมนบอร์ดจะมีช่องสำหรับเสียบการ์ดเครือข่าย โดยต้องใช้สายเคเบิลเครือข่ายเพื่อเชื่อมต่อเข้ากับเครือข่าย การ์ดเครือข่ายภายในแบ่งเป็น 2 ประเภทหลัก:

* **PCI** (Peripheral Component Interconnect): เป็นการ์ดรุ่นเก่ากว่า มีขนาดใหญ่กว่า และเชื่อมต่อกับสล็อต PCI บนเมนบอร์ด ปัจจุบันไม่ค่อยนิยมใช้แล้ว
* **ISA** (Industry Standard Architecture): เป็นการ์ดรุ่นเก่ามาก ไม่เหมาะกับใช้งานยุคใหม่ ไม่นิยมใช้แล้วเช่นกัน
**หมายเหตุ:** ไม่ต้องเสียบเข้าช่องบนเมนบอร์ด: การ์ดเครือข่ายภายในโดยทั่วไปมักจะฝังอยู่บนเมนบอร์ดโดยตรง ไม่ต้องเสียบ ไม่ได้ใช้สล็อต PCI หรือ ISA ซึ่งเป็นเทคโนโลยีเก่าที่เลิกใช้แล้ว ปัจจุบันนิยมใช้ PCIe หรือรุ่นใหม่กว่าอย่าง M.2
![Internal Network Cards](https://www.shutterstock.com/shutterstock/photos/2019663176/display_1500/stock-photo-computer-network-card-on-white-isolated-background-2019663176.jpg)


source : [https://www.shutterstock.com/th/image-photo/computer-network-card-on-white-isolated-2019663176](https://www.shutterstock.com/th/image-photo/computer-network-card-on-white-isolated-2019663176).

2. **External Network Cards**
* ไม่ต้องเสียบการ์ดเครือข่ายไร้สายเข้าเมนบอร์ด: การ์ดเครือข่ายไร้สาย ทั้งแบบภายในและภายนอก เป็นอุปกรณ์อิสระ ไม่ต้องเสียบเข้าเมนบอร์ด พวกมันเชื่อมต่อผ่านพอร์ต USB หรือใช้สล็อตภายในเฉพาะ (เช่น M.2 ในบางรุ่นของแล็ปท็อป)
* ไม่ต้องใช้สายเครือข่าย: ถูกต้องสำหรับการ์ดเครือข่ายไร้สาย เพราะใช้คลื่นวิทยุแทนสาย
* เหมาะสำหรับการเดินทางและเชื่อมต่อสัญญาณไร้สาย: ใช้งานได้ แต่ไม่ใช่จุดประสงค์เดียว ทั้งการ์ดเครือข่ายไร้สายภายในและภายนอก ช่วยให้เชื่อมต่อเครือข่ายไร้สายได้ โดยไม่คำนึงว่าเดินทางหรือไม่

**- ประเภทของ External Network Cards -**
1. แบบ **USB**: ขนาดเล็ก พกพาสะดวก เชื่อมต่อกับพอร์ต USB บนคอมพิวเตอร์เพื่อเข้าถึงเครือข่ายอีเทอร์เน็ตแบบมีสาย
1. แบบ **PCIe** (อะแดปเตอร์ภายนอก): เชื่อมต่อกับสล็อต PCIe ภายนอก (มักพบในเดสก์ท็อป) ประสิทธิภาพสูงกว่าแบบ USB

![External Network Cards](https://www.shutterstock.com/shutterstock/photos/2331271007/display_1500/stock-photo-wireless-card-wifi-mini-pci-e-express-to-pci-e-adapter-with-antenna-external-for-pc-2331271007.jpg)


source : [https://www.shutterstock.com/th/image-photo/wireless-card-wifi-mini-pcie-express-2331271007](https://www.shutterstock.com/th/image-photo/wireless-card-wifi-mini-pcie-express-2331271007).


## คำอื่นๆ ที่ใช้เรียก Network Interface Card ได้แก่

* LAN Adapter

* Physical Network Interface

* Network Controller



![NIC.](https://www.shutterstock.com/shutterstock/photos/472460401/display_1500/stock-photo-network-lan-card-for-computer-isolated-on-white-background-clipping-path-for-use-472460401.jpg)


source : [https://www.shutterstock.com/th/image-photo/network-lan-card-computer-isolated-on-472460401](https://www.shutterstock.com/th/image-photo/network-lan-card-computer-isolated-on-472460401).

## หน้าที่หลักของ NIC:

* แปลงข้อมูลจากคอมพิวเตอร์ให้เป็นสัญญาณดิจิทัลที่สามารถส่งผ่านเครือข่ายได้
* ควบคุมการรับส่งข้อมูลระหว่างคอมพิวเตอร์กับอุปกรณ์อื่นๆ บนเครือข่าย
* จัดการกับ Media Access Control (MAC) address ซึ่งเป็นที่อยู่เฉพาะของ NIC แต่ละตัว

## บทบาทหรือหน้าที่บน Linux  ของ NIC
เชื่อมต่อคอมพิวเตอร์เข้ากับเครือข่าย ทำหน้าที่ส่งและรับข้อมูลผ่านสายเคเบิลหรือสัญญาณไร้สาย 
1. **การสื่อสารเครือข่าย: NIC** จัดการการส่งและรับข้อมูลระหว่างคอมพิวเตอร์กับอุปกรณ์อื่นๆ บนเครือข่าย ทำหน้าที่เป็นจุดเชื่อมต่อทางกายภาพระหว่างคอมพิวเตอร์กับสื่อส่งข้อมูล เช่น สายเคเบิลอีเทอร์เน็ตหรือสัญญาณ Wi-Fi

2. **การเข้าถึงข้อมูล: NIC** ช่วยให้คอมพิวเตอร์สามารถเข้าถึงทรัพยากรที่แชร์บนเครือข่าย เช่น ไฟล์ เครื่องพิมพ์ และเว็บเซิร์ฟเวอร์

3. **การสื่อสารระยะไกล: NIC** ช่วยให้คอมพิวเตอร์สามารถสื่อสารกับคอมพิวเตอร์เครื่องอื่นผ่านเครือข่ายระยะไกล เช่น อินเทอร์เน็ต

4. **การรองรับโปรโตคอลเครือข่าย: NIC** รองรับโปรโตคอลเครือข่ายต่างๆ เช่น TCP/IP, UDP และ ARP โปรโตคอลเหล่านี้กำหนดวิธีการส่งและรับข้อมูลบนเครือข่าย

5. **การจัดการแบนด์วิดท์: NIC** ช่วยให้ระบบปฏิบัติการ Linux จัดการแบนด์วิดท์เครือข่ายได้ ช่วยให้มั่นใจว่าแอปพลิเคชันต่างๆ ได้รับทรัพยากรเครือข่ายที่เพียงพอ

6. **การแก้ไขข้อผิดพลาด: NIC** ตรวจสอบและแก้ไขข้อผิดพลาดที่เกิดขึ้นระหว่างการส่งข้อมูลบนเครือข่าย

7. **การรักษาความปลอดภัย: NIC** รองรับฟีเจอร์ความปลอดภัยต่างๆ เช่น การเข้ารหัสข้อมูลและไฟร์วอลล์ เพื่อปกป้องข้อมูลจากการถูกดักฟังหรือโจมตี

8. **การติดตามและการวิเคราะห์: NIC** สามารถให้ข้อมูลเกี่ยวกับการใช้งานเครือข่าย เช่น สถิติการส่งและรับข้อมูล ข้อมูลนี้สามารถใช้เพื่อติดตามประสิทธิภาพของเครือข่ายและระบุปัญหา

9. **การกำหนดค่า: NIC** สามารถกำหนดค่าได้ผ่านซอฟต์แวร์ Linux ช่วยให้ผู้ใช้สามารถปรับแต่งการตั้งค่าต่างๆ เช่น ความเร็วเครือข่าย ที่อยู่ IP และโหมดการทำงาน

10. **การอัปเดต: ไดรเวอร์ NIC** สามารถอัปเดตได้เพื่อปรับปรุงประสิทธิภาพและความปลอดภัย

## NIC components

* **Speed** :  หน่วยวัดเป็นเมกะบิตต่อวินาที (Mbps) กำหนดประสิทธิภาพของการ์ดเครือข่ายภายในเครือข่าย ยิ่งความเร็วของสัญญาณเครือข่ายต่ำกว่าความเร็วของการ์ด หรือมีคอมพิวเตอร์หลายเครื่องเชื่อมต่อกับตัวควบคุมเดียวกัน ยิ่งส่งผลให้ความเร็วจริงลดลง ปกติแล้วการ์ดเครือข่ายอีเทอร์เน็ตทั่วไปจะมีความเร็วตั้งแต่ 10 Mbps, 100 Mbps, 1000 Mbps และ 1 กิกะบิตต่อวินาที
* **Driver** : ซอฟต์แวร์ที่จำเป็นในการส่งข้อมูลระหว่างระบบปฏิบัติการของคอมพิวเตอร์กับการ์ดเครือข่าย เมื่อติดตั้งการ์ดเครือข่ายบนคอมพิวเตอร์ ระบบจะดาวน์โหลดไดร์เวอร์ที่ตรงกันมาด้วย ไดร์เวอร์จำเป็นต้องได้รับการอัปเดตและใช้งานได้อย่างถูกต้องเพื่อประสิทธิภาพที่ดีที่สุดของการ์ดเครือข่าย
* **MAC address** : ที่อยู่ควบคุมการเข้าถึงสื่อ (Media Access Control Address) หรือที่เรียกว่าที่อยู่เครือข่ายทางกายภาพ เป็นเลขประจำตัวที่ไม่สามารถเปลี่ยนแปลงได้และกำหนดให้กับการ์ดเครือข่าย ที่อยู่ MAC ทำหน้าที่ส่งแพ็คเก็ตข้อมูลอีเทอร์เน็ตไปยังคอมพิวเตอร์
* **LED indicator** :การ์ดเครือข่ายส่วนใหญ่มีไฟแสดงสถานะ LED อยู่ที่ตัวเชื่อมต่อ เพื่อแจ้งผู้ใช้เมื่อเชื่อมต่อกับเครือข่ายและมีการส่งข้อมูล
* **Router** : บางครั้งจำเป็นต้องใช้เราเตอร์เพื่อให้คอมพิวเตอร์สามารถสื่อสารกับอุปกรณ์อื่นๆ ได้ ในกรณีนี้ การ์ดเครือข่ายจะเชื่อมต่อกับเราเตอร์ ซึ่งเชื่อมต่อกับอินเทอร์เน็ต

## ข้อดีของการใช้ NIC:
* เพิ่มความเร็วในการรับส่งข้อมูล
* เพิ่มความเสถียรของการเชื่อมต่อ
* รองรับการเชื่อมต่อกับอุปกรณ์หลากหลายประเภท
* ช่วยให้สามารถเข้าถึงทรัพยากรบนเครือข่ายได้ เช่น ไฟล์ ปริ้นเตอร์ และเครื่องพิมพ์

## ข้อเสียของการใช้ NIC:
* เพิ่มค่าใช้จ่ายในการติดตั้ง
* เพิ่มความซับซ้อนในการตั้งค่า
* อาจเกิดปัญหาเกี่ยวกับความเข้ากันได้กับอุปกรณ์บางประเภท

## หลักการทำงานของ NIC
**รับข้อมูล** : รับข้อมูลจากคอมพิวเตอร์ในรูปแบบของแพ็กเก็ตข้อมูล แพ็กเก็ตข้อมูลประกอบด้วยข้อมูลปลายทาง ข้อมูลต้นทาง และข้อมูลอื่นๆ ที่จำเป็นสำหรับการส่งข้อมูล

**แปลงข้อมูล** : แปลงแพ็กเก็ตข้อมูลจากรูปแบบของคอมพิวเตอร์ให้เป็นรูปแบบที่เหมาะกับสื่อส่งข้อมูล เช่น สัญญาณไฟฟ้าบนสายเคเบิลอีเทอร์เน็ตหรือคลื่นวิทยุสำหรับ Wi-Fi

**ส่งข้อมูล** : ส่งข้อมูลผ่านสื่อส่งข้อมูลไปยังอุปกรณ์ปลายทางบนเครือข่าย

**รับข้อมูล** : รับข้อมูลจากอุปกรณ์ปลายทางบนเครือข่าย

**แปลงข้อมูล** : แปลงข้อมูลจากรูปแบบของสื่อส่งข้อมูลให้เป็นรูปแบบของคอมพิวเตอร์

**ส่งข้อมูล** : ส่งข้อมูลไปยังคอมพิวเตอร์

## ความเร็วของ NIC
* **10 Mbps** : เหมาะสำหรับการใช้งานทั่วไป
* **100 Mbps** : เหมาะสำหรับการใช้งานที่ต้องการความเร็วสูงขึ้น เช่น การดาวน์โหลดไฟล์ขนาดใหญ่
* **1000 Mbps (1 Gbps)**: เหมาะสำหรับการใช้งานที่ต้องการความเร็วสูงสุด เช่น การเล่นเกมออนไลน์

## NIC ใน Linux Networking
โดยทั่วไปแล้ว การ์ดเครือข่ายอีเธอร์เน็ต (Ethernet network interface) จะถูกติดตั้งไว้ภายในเมนบอร์ดของคอมพิวเตอร์รุ่นใหม่ส่วนใหญ่ โดยเฉพาะอย่างยิ่งสำหรับระบบเซิร์ฟเวอร์ ซึ่งมักจะมีการ์ดเครือข่ายติดตั้งอยู่ภายในเมนบอร์ดจำนวนสองอัน นอกจากนี้ ยังสามารถติดตั้งการ์ดเครือข่ายเพิ่มเติมลงในสล็อตเสริม PCI ได้อีกด้วย

ลองใช้คำสั่ง `lspci -vv` เพื่อดูว่าฮาร์ดแวร์ถูกตรวจจับอย่างถูกต้องหรือไม่ และโมดูลเคอร์เนลใด (ถ้ามี) กำลังถูกกำหนด:

    01:00.0 Ethernet controller: Broadcom Corporation NetXtreme BCM5764M Gigabit Ethernet PCIe (rev 10)
        Subsystem: Hewlett-Packard Company Device 1309
        Control: I/O- Mem+ BusMaster+ SpecCycle- MemWINV- VGASnoop- ParErr- Stepping- SERR- FastB2B- DisINTx+
        Status: Cap+ 66MHz- UDF- FastB2B- ParErr- DEVSEL=fast >TAbort- <TAbort- <MAbort- >SERR- <PERR- INTx-
        Latency: 0, Cache Line Size: 64 bytes
        Interrupt: pin A routed to IRQ 52
        Region 0: Memory at f7000000 (64-bit, non-prefetchable) [size=64K]
        Capabilities: <access denied>
        Kernel driver in use: tg3
        Kernel modules: tg3

วิธีการอ่านผลลัพธ์:

    00:00.0: หมายเลขบัส อุปกรณ์ และฟังก์ชัน
    Host bridge: ประเภทอุปกรณ์
    Intel Corporation Xeon E5-2600/3600 v3/4th Gen Core Processor PCIe Express Root Port 1: ชื่ออุปกรณ์
    rev 06: เวอร์ชันอุปกรณ์
    Flags: คุณสมบัติอุปกรณ์
    Device: รหัส PCI ของอุปกรณ์
    Kernel driver in use: โมดูลเคอร์เนลที่ใช้อยู่

ลองใช้คำสั่ง `lspci -vv | grep Ethernet` เพื่อให้ได้ผลลัพธ์ที่ specifically มากขึ้น
ได้ผลลัพธ์

    1:00.0 Ethernet controller: Broadcom Corporation NetXtreme BCM5764M Gigabit Ethernet PCIe (rev 10)
    37:09.0 Ethernet controller: Broadcom Corporation NetXtreme BCM5782 Gigabit Ethernet (rev 03)

คุณสมบัติอุปกรณ์ : 
* bus master: อุปกรณ์สามารถเข้าถึงหน่วยความจำหลักโดยตรง
* fast devsel: อุปกรณ์รองรับการเข้าถึง DMA ที่รวดเร็ว
* latency 0: อุปกรณ์มีความหน่วงเวลาต่ำ
* cap_list: อุปกรณ์รองรับ PCI Capabilities List
* 64bit: อุปกรณ์รองรับ PCI 64-bit
* pci_exp: อุปกรณ์เป็นอุปกรณ์ PCIe
* msi: อุปกรณ์รองรับ MSI (Message Signaled Interrupts)
* pciexpress: อุปกรณ์เป็นอุปกรณ์ PCIe Express
* vga_arbiter: อุปกรณ์รองรับ VGA arbiter
* rom_bar: อุปกรณ์มี ROM BAR (Base Address Register)
* netdev: อุปกรณ์เป็นอุปกรณ์เครือข่าย

### เครื่องมือสำหรับการกำหนดค่าเครือข่ายและไฟล์กำหนดค่าเครือข่ายนั้นแตกต่างกันไปตามระบบปฏิบัติการที่ใช้ โดยแบ่งเป็นสองกลุ่มใหญ่ๆ คือ:
**1. ระบบปฏิบัติการแบบ Debian/Ubuntu:**
* เครื่องมือ: นิยมใช้ `netplan` เป็นหลัก ซึ่งเป็นเครื่องมือจัดการคอนฟิกเครือข่ายแบบ declarative โดยกำหนดค่าเป็น YAML นอกจากนี้ ยังมีตัวเลือกอื่นๆ เช่น `ifupdown `และ `NetworkManager`
* ไฟล์กำหนดค่า: มักเก็บอยู่ในไดเร็กทอรี่ `/etc/netplan` สำหรับไฟล์ YAML ของ netplan และ `/etc/network/interfaces` สำหรับไฟล์ของ ifupdown
**เน้นความยืดหยุ่นและกำหนดค่าด้วยตนเอง ผ่านไฟล์ YAML ใน netplan

**2. ระบบปฏิบัติการแบบ Red Hat/Fedora:**
* เครื่องมือ: ส่วนใหญ่ใช้ `systemd-networkd` ซึ่งเป็นบริการที่มาพร้อมกับ systemd สำหรับการจัดการเครือข่าย หรือ `NetworkManager`
* ไฟล์กำหนดค่า: ไฟล์หลักมักเก็บอยู่ในไดเร็กทอรี่ `/etc/systemd/network` สำหรับ systemd-networkd และ `/etc/NetworkManager/conf.d` สำหรับ NetworkManager
**เน้นความสะดวกและการจัดการอัตโนมัติ ผ่าน systemd-networkd

## Linux configuration for a new card (การกำหนดค่า Linux สำหรับการ์ดใหม่) :
start network :

    sudo /etc/init.d/networking start
stop network : 

    sudo /etc/init.d/networking stop
restart network : 

    sudo /etc/init.d/networking restart

## Ubuntu network configuration:
โดยดั้งเดิม Ubuntu มีเครื่องมือ GUI สำหรับการกำหนดค่าเครือข่ายชื่อว่า **gnome-nettool** ซึ่งสามารถติดตั้งได้ด้วยคำสั่ง `apt-get install gnome-nettool`

**gnome-nettool ถูกยกเลิกการใช้งานใน Ubuntu 17.10 (Artful Aardvark) **และถูกลบออกจากที่เก็บอย่างสมบูรณ์ใน Ubuntu 18.04 (Bionic Beaver). ดังนั้น หากคุณใช้ Ubuntu เวอร์ชันใดที่ใหม่กว่า 17.10 คุณจะไม่สามารถติดตั้งหรือใช้ gnome-nettool ได้อีกต่อไป

***การกำหนดค่าเครือข่ายใน Ubuntu เวอร์ชันใหม่**
* **Netplan**: เครื่องมือหลักที่แนะนำสำหรับการกำหนดค่าเครือข่ายใน Ubuntu เวอร์ชันใหม่กว่า 17.10 ใช้ไฟล์ YAML แบบ declarative ทำให้กำหนดค่าได้ง่ายและยืดหยุ่น

จุดเด่น:

    - ใช้งานง่าย

    - กำหนดค่าได้ละเอียด

    - รองรับการเชื่อมต่อเครือข่ายหลากหลาย

    - ทำงานร่วมกับ NetworkManager ได้

ข้อจำกัด:

    - อาจจะยากสำหรับผู้ใช้ใหม่

    - ต้องการความรู้เกี่ยวกับ YAML

* **NetworkManager**: เครื่องมือ GUI ยอดนิยมสำหรับการจัดการเครือข่าย สามารถติดตั้งได้ด้วยคำสั่ง sudo apt install network-manager-gnome

จุดเด่น:

    - ใช้งานง่าย

    - อินเทอร์เฟซผู้ใช้ที่ใช้งานง่าย

    - รองรับการเชื่อมต่อเครือข่ายหลากหลาย

ข้อจำกัด:

    - ตัวเลือกการกำหนดค่าอาจจำกัดสำหรับผู้ใช้ขั้นสูง
    
    - อาจจะไม่เสถียรเท่า Netplan

* **nmtui**: เครื่องมือบรรทัดคำสั่งสำหรับ NetworkManager ใช้งานง่าย เหมาะสำหรับผู้ใช้ขั้นสูง

จุดเด่น:

    - ใช้งานง่าย

    - กำหนดค่าได้ละเอียด

    - ทำงานร่วมกับ NetworkManager ได้

ข้อจำกัด:

    - ไม่เหมาะสำหรับผู้ใช้ทั่วไป
    
    - อาจจะยากสำหรับผู้ใช้ใหม่

* **การแก้ไขไฟล์กำหนดค่าเครือข่ายด้วยตนเอง**: วิธีนี้เหมาะสำหรับผู้ใช้ขั้นสูงเท่านั้น โดยไฟล์กำหนดค่าหลักของ Netplan อยู่ในไดเร็กทอรี่ /etc/netplan

จุดเด่น:

    - กำหนดค่าได้ละเอียด

    - ควบคุมการทำงานของเครือข่ายได้เต็มที่

ข้อจำกัด:

    - ยากและซับซ้อน
    
    - อาจจะทำให้ระบบทำงานผิดพลาดได้

### - Example How to Configure Networking on Ubuntu with Netplan
1. ขั้นแรก ค้นหาชื่อของอินเทอร์เฟซเครือข่ายที่ใช้งานอยู่ที่คุณต้องการกำหนดค่า โดยให้รันคำสั่งต่อไปนี้:

        $ ip a

1. ไฟล์การกำหนดค่าเริ่มต้นของ Netplan อยู่ภายใต้ไดเร็กทอรี/etc/netplanคุณจะพบว่าใช้คำสั่งต่อไปนี้:

        $ ls /etc/netplan/

1. หากต้องการดูเนื้อหาของไฟล์การกำหนดค่าเครือข่าย Netplan ให้รันคำสั่งต่อไปนี้:

        $ cat /etc/netplan/*.yaml

1. เปิดไฟล์การ configuration file ในที่นี้ใช้ Nano เพื่อแก้ไขไฟล์การกำหนดค่า ดังนั้นจึงเรียกใช้:

        $ sudo nano /etc/netplan/*.yaml

1.  อัปเดตไฟล์การกำหนดค่าตามความต้องการด้านเครือข่าย สำหรับการกำหนดที่อยู่ IP แบบ static เพิ่มที่อยู่ IP, Gateway, DNS ในขณะที่แบบ dinamic ม่จำเป็นต้องเพิ่มข้อมูลนี้เนื่องจากจะได้รับข้อมูลนี้จากเซิร์ฟเวอร์ DHCP โดยให้รันคำสั่งต่อไปนี้:

        network:
            Version: 2
            Renderer: NetworkManager/ networkd
            ethernets:
            DEVICE_NAME:
                Dhcp4: yes/no
                Addresses: [IP_ADDRESS/NETMASK]
                Gateway: GATEWAY
                Nameservers:
                    Addresses: [NAMESERVER_1, NAMESERVER_2]

โดยที่
* DEVICE_NAME: ชื่อ interface.
* Dhcp4: "yes" or "no" ขึ้นอยู่กับการกำหนดที่อยู่ IP แบบ dynamic or static
* Addresses: IP address ในรูป prefix notation. อย่าใช้ netmask.
* Gateway: ที่อยู่ IP ของ Gateway เพื่อเชื่อมต่อกับเครือข่ายภายนอก
* Nameservers: ที่อยู่ของ DNS name servers

-ข้อควรระวัง-
**YAML ค่อนข้างเข้มงวดในการเยื้อง ใช้ช่องว่างในการเยื้อง ไม่ใช่แท็บ มิฉะนั้นคุณจะพบข้อผิดพลาด**


## How to Enable (UP)/Disable (DOWN) Network Interface Port (NIC) in Linux?

ip command : แสดงข้อมูลการ์ดอินเทอร์เฟซเครือข่ายที่มีอยู่ในระบบ Linux

    # ip a
    1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
        link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
        inet 127.0.0.1/8 scope host lo
        valid_lft forever preferred_lft forever
        inet6 ::1/128 scope host 
        valid_lft forever preferred_lft forever
    2: enp0s3: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
        link/ether 08:00:27:c2:e4:e8 brd ff:ff:ff:ff:ff:ff
        inet 192.168.1.4/24 brd 192.168.1.255 scope global dynamic noprefixroute enp0s3
        valid_lft 86049sec preferred_lft 86049sec
        inet6 fe80::3899:270f:ae38:b433/64 scope link noprefixroute 
        valid_lft forever preferred_lft forever
    3: enp0s8: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
        link/ether 08:00:27:30:5d:52 brd ff:ff:ff:ff:ff:ff
        inet 192.168.1.3/24 brd 192.168.1.255 scope global dynamic noprefixroute enp0s8
        valid_lft 86049sec preferred_lft 86049sec
        inet6 fe80::32b7:8727:bdf2:2f3/64 scope link noprefixroute 
        valid_lft forever preferred_lft forever

## 1) Bring UP/Down Network Interface, using ifconfig command
`ifconfig` ทำงานใน boot time เพื่อตั้งค่าอินเทอร์เฟซเครือข่ายและให้ข้อมูลเกี่ยวกับ NIC

Common Syntax for ifconfig:

    # ifconfig [NIC_NAME] Down/Up

Example : **down** "enp0s3"

    ifconfig enp0s3 down

output

    # ip a sh dev enp0s3
    2: enp0s3: <BROADCAST,MULTICAST> mtu 1500 qdisc fq_codel state DOWN group default qlen 1000
        link/ether 08:00:27:c2:e4:e8 brd ff:ff:ff:ff:ff:ff

Example : **up** "enp0s3"

    # ifconfig enp0s3 up

output

    # ip a sh dev enp0s3
    2: enp0s3: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
        link/ether 08:00:27:c2:e4:e8 brd ff:ff:ff:ff:ff:ff
        inet 192.168.1.4/24 brd 192.168.1.255 scope global dynamic noprefixroute enp0s3
        valid_lft 86294sec preferred_lft 86294sec
        inet6 fe80::3899:270f:ae38:b433/64 scope link noprefixroute 
        valid_lft forever preferred_lft forever

## 2) How to enable and disable Network Interface using ifdown/ifup command?

คำสั่ง `ifdown` จะทำให้ Network interface down ในขณะที่คำสั่ง `ifup` 
จะทำให้ Network interface up

Common Syntax for ifdown/ifup:

    # ifdown [NIC_NAME]

    # ifup [NIC_NAME]

Example : **down** and **up** "enp0s3"

    # ifdown eth1

    # ifup eth1

output

    "down"
    # ip a sh dev eth1
    3: eth1: <BROADCAST,MULTICAST> mtu 1500 qdisc pfifo_fast state DOWN qlen 1000
        link/ether 08:00:27:d5:a0:18 brd ff:ff:ff:ff:ff:ff

    "up"
    # ip a sh dev eth1
    3: eth1: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc pfifo_fast state UP qlen 1000
        link/ether 08:00:27:d5:a0:18 brd ff:ff:ff:ff:ff:ff
        inet 192.168.1.7/24 brd 192.168.1.255 scope global eth1
        inet6 fe80::a00:27ff:fed5:a018/64 scope link tentative dadfailed 
        valid_lft forever preferred_lft forever

**ifup และ ifdown ไม่รองรับอุปกรณ์อินเทอร์เฟซล่าสุดที่มีชื่อเช่น `enpXXX`**

## 3) Bringing UP/Down Network Interface using ip command?

Common Syntax for ip:

    # ip link set  Down/Up

Example : **down** and **up** "enp0s3"

    # ip link set enp0s3 down

    # ip link set enp0s3 up

output

    # ip a sh dev enp0s3
    2: enp0s3: <BROADCAST,MULTICAST> mtu 1500 qdisc fq_codel state DOWN group default qlen 1000
        link/ether 08:00:27:c2:e4:e8 brd ff:ff:ff:ff:ff:ff

    # ip a sh dev enp0s3
    2: enp0s3: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
        link/ether 08:00:27:c2:e4:e8 brd ff:ff:ff:ff:ff:ff
        inet 192.168.1.4/24 brd 192.168.1.255 scope global dynamic noprefixroute enp0s3
        valid_lft 86294sec preferred_lft 86294sec
        inet6 fe80::3899:270f:ae38:b433/64 scope link noprefixroute 
        valid_lft forever preferred_lft forever

## 4) How to enable & disable Network Interface using nmcli command?

คำสั่ง `nmcli` สามารถใช้แทน `nm-applet` ได้ nmcli ใช้เพื่อสร้าง แสดง แก้ไข ลบ เปิดใช้งานและปิดใช้งานการเชื่อมต่อเครือข่าย รวมถึงควบคุมและแสดงสถานะอุปกรณ์เครือข่าย

คำสั่ง nmcli ดำเนินงานส่วนใหญ่โดยใช้ `profile name` แทน `device name` รันคำสั่งต่อไปนี้เพื่อระบุชื่ออินเทอร์เฟซ

    # nmcli con show
    NAME                UUID                                  TYPE      DEVICE 
    Wired connection 1  3d5afa0a-419a-3d1a-93e6-889ce9c6a18c  ethernet  enp0s3 
    Wired connection 2  a22154b7-4cc4-3756-9d8d-da5a4318e146  ethernet  enp0s8 

Common Syntax for nmcli:

    # nmcli con  Down/Up

เริ่มจากการใส่ `profile name` แทนการใส่ `device name` เพื่อ down interface และ up interface 

    # nmcli con down 'Wired connection 1'
    Connection 'Wired connection 1' successfully deactivated (D-Bus active path: /org/freedesktop/NetworkManager/ActiveConnection/6)


    # nmcli con up 'Wired connection 1'
    Connection successfully activated (D-Bus active path: /org/freedesktop/NetworkManager/ActiveConnection/7)

output

    # nmcli dev status
    DEVICE  TYPE      STATE         CONNECTION         
    enp0s8  ethernet  connected     Wired connection 2 
    enp0s3  ethernet  disconnected  --                 
    lo      loopback  unmanaged     --  


    # nmcli dev status
    DEVICE  TYPE      STATE      CONNECTION         
    enp0s8  ethernet  connected  Wired connection 2 
    enp0s3  ethernet  connected  Wired connection 1 
    lo      loopback  unmanaged  --  

## 5) Bringing UP/Down Network Interface using systemctl command?

คำ สั่ง `systemctl` สามารถใช้เพื่อใช้การกำหนดค่าใหม่สำหรับบริการเครือข่ายซึ่งจะ brings down and brings up >> Network Interface Cards (NIC) ทั้งหมดขึ้นมาเพื่อโหลดการกำหนดค่าใหม่

    # systemctl restart network

    # systemctl restart network.service

## 6) Bringing UP/Down Network Interface using nmtui tool?

`nmtui` เป็นแอปพลิเคชัน TUI ใช้สำหรับการโต้ตอบกับ Network Manager ช่วยให้เราสามารถกำหนดค่าอินเทอร์เฟซเครือข่ายบนระบบ Linux โดยใช้ GUI ได้อย่างง่ายดาย
รันคำสั่ง `# nmtui` เพื่อเรียกใช้   interface nmtui 
- เลือก “Activate a connection”
- กด “OK”
- เลือก interface ที่ต้องการ 
- กด “Deactivate”
- สำหรับการเปิดใช้งาน ทำตามขั้นตอนเดียวกับข้างต้นได้เลย แต่เป็นกด “Activate”

## ข้อควรระวังในการใช้งาน NIC
* **การอัปเดตไดรเวอร์** : ควรอัปเดตไดรเวอร์ NIC อยู่เสมอเพื่อให้แน่ใจว่าใช้งานได้อย่างมีประสิทธิภาพและปลอดภัย ไดรเวอร์เวอร์ชันใหม่สามารถแก้ไขข้อบกพร่อง ปรับปรุงประสิทธิภาพ และเพิ่มฟีเจอร์ใหม่ๆ
* **การป้องกันไฟฟ้าสถิต** : ไฟฟ้าสถิตสามารถสร้างความเสียหายให้กับ NIC ได้ ควรระมัดระวังเมื่อถอดหรือเสียบ NIC เข้ากับคอมพิวเตอร์
* **การระบายความร้อน** : NIC บางรุ่นอาจร้อนขึ้นเมื่อใช้งาน ควรติดตั้ง NIC ในที่ที่มีการระบายความร้อนที่ดี
* **การตั้งค่าเครือข่าย**: ควรตั้งค่าเครือข่ายของ NIC ให้ถูกต้องเพื่อให้สามารถเชื่อมต่อกับเครือข่ายได้
* **การรักษาความปลอดภัย**: ควรติดตั้งซอฟต์แวร์รักษาความปลอดภัยบนคอมพิวเตอร์เพื่อป้องกัน NIC จากการโจมตีทางไซเบอร์







## เพิ่มเติม
* Network Interface Card (NIC) : หมายถึง การ์ดใดๆ ที่ทำหน้าที่เชื่อมต่อคอมพิวเตอร์กับเครือข่าย โดยไม่จำเป็นต้องระบุเทคโนโลยีที่ใช้
* PCIe (Peripheral Component Interconnect Express) เป็นมาตรฐานส่วนขยายสำหรับการเชื่อมต่ออุปกรณ์ความเร็วสูงกับคอมพิวเตอร์ พัฒนาขึ้นเพื่อแทนที่สล็อต PCI ดั้งเดิม PCIe นำเสนอความเร็วในการรับส่งข้อมูลที่สูงขึ้นและประสิทธิภาพที่ดีขึ้น

* M.2 เป็นมาตรฐานใหม่สำหรับการเชื่อมต่ออุปกรณ์ SSD กับคอมพิวเตอร์ มันใช้รูปแบบแฟคเตอร์ขนาดเล็กที่สามารถเสียบเข้ากับสล็อต M.2 บนเมนบอร์ดได้ M.2 รองรับทั้ง PCIe และ SATA SSDs

* M.2 นั้นเร็วกว่า SATA SSDs แบบดั้งเดิม เนื่องจากสามารถใช้ประโยชน์จากความเร็ว PCIe ได้ สิ่งนี้ทำให้เหมาะอย่างยิ่งสำหรับการใช้งานที่ต้องการประสิทธิภาพสูง เช่น การเล่นเกมและการแก้ไขวิดีโอ

## Command ต่างๆ
หากมีการเปลี่ยนแปลงใด ๆ ใน NIC เนื่องจากอินเทอร์เฟซไม่ทำงาน อินเทอร์เฟซนั้นสามารถดึงขึ้นมาได้หลายวิธี 

**คำสั่งดังต่อไปนี้:**

* `ifconfig` : ใช้เพื่อกำหนดค่าอินเทอร์เฟซเครือข่าย ให้ข้อมูลมากมายเกี่ยวกับ NIC
* `ifdown/ifup` :  ifdown ทำให้อินเทอร์เฟซเครือข่ายลดลง ในขณะที่ ifup จะทำให้อินเทอร์เฟซเครือข่ายขึ้น
* `ip` : ใช้เพื่อจัดการ NIC เป็นการแทนที่คำสั่ง ifconfig เก่าและเลิกใช้แล้ว คล้ายกับคำสั่ง ifconfig แต่มีคุณสมบัติที่มีประสิทธิภาพมากมายซึ่งไม่มีในคำสั่ง ifconfig
* `nmcli` : nmcli เป็นเครื่องมือบรรทัดคำสั่งสำหรับควบคุม Network Manager และรายงานสถานะเครือข่าย
* `systemctl` : เป็นเครื่องมือที่รับผิดชอบในการควบคุมระบบ systemd และตัวจัดการบริการ
* `nmtui` : เป็นแอปพลิเคชัน TUI ที่ใช้คำสาปสำหรับการโต้ตอบกับ Network Manager

## Source เนื้อหา
* http://www.yolinux.com/TUTORIALS/LinuxTutorialNetworking-Add_NIC.html
* https://vitux.com/how-to-configure-networking-with-netplan-on-ubuntu/
* https://www.2daygeek.comenable-disable-up-down-nic-network-interface-port-linux/
* https://www.techtarget.com/searchnetworking/definition/network-interface-card
* https://il.mahidol.ac.th/e-media/computer/network/net_hardware5.htm
* https://makcheeze.blogspot.com/p/lan-card.html

