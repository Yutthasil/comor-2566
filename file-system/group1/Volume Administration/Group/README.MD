# Volume Group Administration

Volume Group (VG) เป็นกลุ่มของ Physical Volumes (PVs) ที่ถูกรวมกันเพื่อสร้างพื้นที่จัดเก็บข้อมูลในรูปแบบของ Logical Volumes (LVs) ในระบบ LVM

> [!NOTE]
> ภายใน Volume Group (VG) มีพื้นที่ว่างที่สามารถจัดสรรได้จะถูกแบ่งเป็น units ที่มีขนาดคงที่ที่เรียกว่า `extents`

การใช้ extents ใน LVM ช่วยให้ผู้ใช้สามารถจัดการพื้นที่จัดเก็บข้อมูลใน Volume Group (VG) ได้อย่างยืดหยุ่นและมีประสิทธิภาพ

---
## การสร้าง Volume Group

หากต้องการสร้าง Volume Group จาก Physical Volumes ให้ใช้คำสั่ง

```
vgcreate <volume_group_name> <physical_volume> [<physical_volume> ...]
```

**ตัวอย่างการใช้งาน:**

* สร้าง Volume Group ชื่อ "myvg" โดยใช้สอง Physical Volumes **/dev/sdb1** และ **/dev/sdc1** โดยใช้คำสั่ง

    `vgcreate myvg /dev/sdb1 /dev/sdc1`

* สามารถตรวจสอบว่า Volume Group ถูกสร้างเรียบร้อยด้วยคำสั่ง

    `vgdisplay myvg`

เมื่อใช้ Physical Volumes ในการสร้างแล้ว พื้นที่ดิสก์จะถูกแบ่งออกเป็น 4MB extents ตามค่าเริ่มต้น 

> [!NOTE]
> โดย extent นี้คือจำนวนขั้นต่ำที่ Logical Volume อาจเพิ่มหรือลดขนาดได้ 
ในส่วนขยายจำนวนมากจะไม่มีผลกระทบต่อประสิทธิภาพ I/O ของโลจิคัลวอลุ่ม

>[!TIP]
>- สามารถระบุขนาดขอบเขตด้วย option `-s` ให้กับคำสั่ง vgcreate หากขนาด default extent ไม่เหมาะสม 
>- สามารถกำหนดขีดจำกัดจำนวน physical หรือ logical volumes, the volume group ได้โดยใช้ option `-p` และ `-l` 


Volume group จะจัดสรร physical extents ตามกฎทั่วไป เช่น ไม่วางแถบขนาน (parallel stripes) บนวอลุ่มฟิสิคัลเดียวกัน นี่คือ นโยบายการจัดสรรพื้นที่แบบปกติ (normal allocation policy)

ใช้ตัวเลือก `--alloc` ของคำสั่ง `vgcreate` เพื่อระบุ นโยบายการจัดสรรพื้นที่  ซึ่งอาจจะเป็น `contiguous`, `anywhere`, หรือ `cling` โดยทั่วไปแล้ว ไม่จำเป็นต้องใช้นโยบายการจัดสรรพื้นที่อื่นนอกเหนือจาก `normal`   ยกเว้นกรณีพิเศษที่คุณต้องการกำหนดการจัดสรรพื้นที่ที่ไม่ปกติ

>[!TIP]
> - **Physical Extents** : เป็นหน่วยพื้นฐานที่เล็กที่สุดของพื้นที่เก็บข้อมูลที่ LVM สามารถจัดสรรได้
>- **Parallel Stripes** : คือการแบ่งข้อมูลออกเป็นส่วนๆ แล้วกระจายไปยังวอลุ่มฟิสิคัลหลายๆ วอลุ่มเพื่อเพิ่มประสิทธิภาพการอ่าน/เขียน
>- **Contiguous Allocation** : จัดสรรพื้นที่ฟิสิคัลติดกันสำหรับ Logical Volume
>- **Anywhere Allocation** : จัดสรรพื้นที่ฟิสิคัลไม่ติดกันจากวอลุ่มฟิสิคัลใดก็ได้ในกลุ่มวอลุ่ม 
>- **Cling Allocation** : ขยาย Logical Volume โดยจัดสรรพื้นที่ฟิสิคัลจากวอลุ่มฟิสิคัลเดียวกันที่ใช้จัดสรรพื้นที่ไปแล้ว

LVM volume groups และ Logical Volume จะรวมอยู่ในไดเร็กทอรีไฟล์พิเศษของอุปกรณ์ในไดเร็กทอรี `/dev` โดยมีเค้าโครงดังนี้:

-   `/dev/mapper` : ไดเร็กทอรีนี้เก็บลิงก์เชิงสัญลักษณ์ที่แสดง Logical Volume (LVs) ซึ่งเป็นพาร์ติชั่นเสมือนที่ LVM จัดการ โดยทั่วไปชื่อของลิงก์เหล่านี้จะขึ้นต้นด้วย `lv` และผู้ใช้กำหนดเอง (เช่น lv01, lv_data, lv_root)
- `/dev/lvm` : ไดเร็กทอรีนี้ประกอบด้วยโหนดตัว map อุปกรณ์ ซึ่งให้ข้อมูลเกี่ยวกับคุณสมบัติหรือส่วนประกอบ LVM เฉพาะ ตัวอย่างเช่น:
   * `pvlist` : แสดงรายละเอียดเกี่ยวกับ Physical Volume (PVs) ซึ่งเป็นพาร์ติชั่นดิสก์หรืออุปกรณ์ที่ประกอบกันเป็นกลุ่มวอลุ่ม
   * `vglist` : แสดงข้อมูลเกี่ยวกับ Volume Group (VGs) ซึ่งเป็นชุดของ PVs ที่จัดกลุ่มเพื่อการจัดการพื้นที่เก็บข้อมูลแบบรวมศูนย์
   * `lvchange` : อนุญาตให้แก้ไขคุณสมบัติของ Logical Volume หลังจากสร้าง

   ![Image](https://miro.medium.com/v2/resize:fit:1342/format:webp/0*aVQTBvKe8oocgmsd.png)
   
   รูปจาก: [https://medium.com/@nareerat.prr/what-is-lvm-24ae24322eff](https://medium.com/@nareerat.prr/what-is-lvm-24ae24322eff)

---
## สร้าง Volume Groups ใน Cluster

สร้าง Volume Group ในสภาพแวดล้อมที่มีคอมพิวเตอร์หลายเครื่องทำงานร่วมกัน (Cluster) ซึ่งแตกต่างจากการสร้างบนคอมพิวเตอร์เครื่องเดียว (Single Node)

จุดประสงค์:
- **เพิ่มพื้นที่จัดเก็บข้อมูล**: การรวมพื้นที่จัดเก็บข้อมูลจากหลายโหนดในคลัสเตอร์เข้าด้วยกัน เพิ่มพื้นที่โดยรวมที่สามารถใช้งานได้
- **เพิ่มความพร้อมใช้งาน**: หากโหนดใดเกิดขัดข้อง โหนดอื่นๆ ยังสามารถเข้าถึงข้อมูลได้ เนื่องจากกลุ่มวอลุ่มถูกแชร์ระหว่างโหนดต่างๆ
- **เพิ่มประสิทธิภาพ**: การกระจายการอ่านเขียนข้อมูลไปยังหลายโหนด ช่วยเพิ่มความเร็วในการเข้าถึงข้อมูล

สามารถสร้าง CLVM volume groups ใน cluster environment ได้ด้วยคำสั่ง `vgcreate` เช่นเดียวกับที่สร้างบนโหนด

**การสร้างและจัดการ Volume Groups ใน Cluster**

- **Volume Groups ที่แชร์ระหว่างสมาชิกใน Cluster** : ควรสร้างด้วยการตั้งค่าแอตทริบิวต์แบบคลัสเตอร์ (clustered attribute) โดยใช้คำสั่ง `vgcreate -cy` หรือ `vgchange -cy` แอตทริบิวต์นี้จะถูกตั้งค่าโดยอัตโนมัติหาก CLVMD (Clustered Logical Volume Manager Daemon) กำลังทำงานอยู่ แอตทริบิวต์แบบ Cluster จะส่งสัญญาณว่า Volume Groups นี้ควรได้รับการจัดการและป้องกันโดย CLVMD
- **Volume Groups ที่ไม่ได้แชร์ใน Cluster** : ควรปิดการใช้งานแอตทริบิวต์แบบคลัสเตอร์ด้วยคำสั่ง `vgcreate -cn` หรือ `vgchange -cn` เพื่อให้ Volume Groups นี้มองเห็นได้เฉพาะบนโฮสต์เดียวเท่านั้น

Volume Groups ที่สร้างด้วยแอตทริบิวต์แบบคลัสเตอร์บนพื้นที่จัดเก็บข้อมูลแบบแชร์จะสามารถมองเห็นได้บนคอมพิวเตอร์ทุกเครื่องในคลัสเตอร์ที่สามารถเข้าถึงพื้นที่จัดเก็บข้อมูลนั้นร่วมกันได้

สามารถกำหนดให้ Volume Groups เป็นแบบ local ซึ่งมองเห็นได้เฉพาะบนโหนดเดียวใน cluster ได้ โดยการใช้ตัวเลือก `-cn` ในคำสั่ง `vgcreate`

**ตัวอย่างการใช้งาน:**

สร้าง Volume Groups ที่จำกัด (local) เฉพาะโหนดที่ทำงานคำสั่ง 
```
vgcreate -cn vg1 /dev/sdd1 /dev/sde1
```
คำสั่งนี้สร้าง Volume Groups ชื่อ vg1 ที่ประกอบด้วย Physical Volumes /dev/sdd1 และ /dev/sde1

#### การปรับ Volume Groups ให้เป็น Local หรือ Clustered:
- สามารถใช้คำสั่ง `vgchange` พร้อมกับตัวเลือก `-c` เพื่อเปลี่ยนลักษณะของ Volume Groups ที่มีอยู่ ให้เป็นแบบ local หรือแบบ clustered 
#### การตรวจสอบกลุ่มวอลุ่มที่เป็นแบบ Clustered:
- ใช้คำสั่ง `vgs` เพื่อตรวจสอบว่ากลุ่มวอลุ่มที่มีอยู่เป็นกลุ่มวอลุ่มแบบคลัสเตอร์หรือไม่ คำสั่งนี้จะแสดงแอตทริบิวต์ 'c' หากกลุ่มวอลุ่มนั้นเป็นแบบคลัสเตอร์ ตัวอย่างเช่น
```
# vgs
  VG            #PV #LV #SN Attr   VSize  VFree
  VolGroup00      1   2   0 wz--n- 19.88G    0
  testvg1         1   1   0 wz--nc 46.00G 8.00M
```

ในตัวอย่างนี้ VolGroup00 ไม่ใช่ Volume Groups แบบ Cluster (ไม่มีแอตทริบิวต์ 'c') ในขณะที่ testvg1 เป็น Volume Groups แบบ Cluster (สังเกตแอตทริบิวต์ 'c' ใต้หัวข้อ Attr)

---
## การเพิ่ม  Physical Volumes ให้กับกลุ่ม Volume Group
ใช้คำสั่ง `vgextend` เพื่อเพิ่ม Physical Volumes เพิ่มเติมให้กับ Volume Group ที่มีอยู่คำสั่งนี้จะช่วยขยายความจุของ Volume Group โดยเพิ่ม Physical Volumes ที่ว่างอยู่หนึ่งหรือมากกว่า

```
vgextend <volume_group_name> <physical_volume>
```

ตัวอย่างการใช้งาน:
- `vgextend vg1 /dev/sdf1`/dev/sdf1 จะถูกเพิ่มเข้าไปในกลุ่มวอลุ่ม vg1 ส่งผลให้ความจุรวมของกลุ่มวอลุ่มเพิ่มขึ้น

---
## Volume Groups

คุณสมบัติของ Volume Groups แสดงออกมาได้ในสองคำสั่งคือ `vgs` และ `vgdisplay`

- `vgscan` : คำสั่งนี้ใช้สำหรับสแกนดิสก์ทั้งหมดเพื่อค้นหา Volume Group และสร้างไฟล์แคช LVM ขึ้นใหม่ นอกจากนี้ยังแสดงรายการ Volume Group ที่พบ
- `vgs` : คำสั่งนี้ใช้แสดงรายละเอียดของ Volume Group ทั้งหมดในรูปแบบตารางที่ปรับแต่งได้ เหมาะสำหรับการดูภาพรวมหรือใช้ในสคริปต์
- `vgdisplay` : คำสั่งนี้ใช้แสดงรายละเอียดเชิงลึกของ Volume Group ที่ระบุ เหมาะสำหรับการตรวจสอบข้อมูลและแก้ไขปัญหา

```
# vgdisplay new_vg
  --- Volume group ---
  VG Name               new_vg
  System ID
  Format                lvm2
  Metadata Areas        3
  Metadata Sequence No  11
  VG Access             read/write
  VG Status             resizable
  MAX LV                0
  Cur LV                1
  Open LV               0
  Max PV                0
  Cur PV                3
  Act PV                3
  VG Size               51.42 GB
  PE Size               4.00 MB
  Total PE              13164
  Alloc PE / Size       13 / 52.00 MB
  Free  PE / Size       13151 / 51.37 GB
  VG UUID               jxQJ0a-ZKk0-OpMO-0118-nlwO-wwqd-fD5D32
```

---
## สแกน Disk สำหรับ Volume Group เพื่อสร้าง Cache File

- **สแกนอุปกรณ์ดิสก์ทั้งหมดที่รองรับ** : เมื่อรันคำสั่ง `vgscan` มันจะตรวจสอบทุกอุปกรณ์ดิสก์ที่ระบบสามารถมองเห็น โดยเฉพาะอย่างยิ่งเพื่อค้นหาอุปกรณ์ที่ถูกกำหนดค่าเป็น LVM physical volumes (PVs) และ LVM volume groups (VGs)

- **สร้างและอัปเดต LVM Cache File** : ข้อมูลที่พบจากการสแกนจะถูกใช้ในการสร้างหรืออัปเดตไฟล์แคช LVM ซึ่งตั้งอยู่ที่ `/etc/lvm/cache/.cache` ไฟล์นี้ทำหน้าที่เก็บรายการของอุปกรณ์ LVM ที่พบล่าสุด ช่วยให้ LVM ทำงานได้รวดเร็วขึ้นโดยไม่ต้องสแกนดิสก์ทั้งหมดทุกครั้ง
- **รันอัตโนมัติและด้วยตนเอง** : คำสั่ง `vgscan` มักจะรันโดยอัตโนมัติในบางสถานการณ์ เช่น ตอนเริ่มระบบ หลังจากสร้างหรือลบ VGs/PVs หรือเมื่อ LVM ตรวจพบความไม่สอดคล้อง นอกจากนี้ คุณยังสามารถเรียกใช้คำสั่งนี้ด้วยตนเองเมื่อต้องการอัปเดตแคช LVM เอง

`vgscan` เป็นคำสั่งสำคัญที่ช่วยให้ LVM ติดตามและจัดการกับอุปกรณ์ดิสก์ที่เกี่ยวข้องอย่างมีประสิทธิภาพ

> [!NOTE]
> เพิ่มหรือลบอุปกรณ์ดิสก์บนโหนด: การเปลี่ยนแปลงนี้ทำให้ระบบมองเห็นอุปกรณ์ใหม่ที่ไม่ได้อยู่ในรายการตอนบูต จำเป็นต้องรัน `vgscan` เพื่อสแกนหาอุปกรณ์ LVM เพิ่มเติม เช่น เมื่อคุณเพิ่มดิสก์ใหม่บน SAN (Storage Area Network) หรือเสียบดิสก์ใหม่ที่มีป้ายกำกับเป็น PV

**ตัวอย่างการใช้งาน** :

```
# vgscan
  Reading all physical volumes.  This may take a while...
  Found volume group "new_vg" using metadata type lvm2
  Found volume group "officevg" using metadata type lvm2
```


คุณสามารถจำกัดขอบเขตการสแกนของคำสั่ง vgscan เพื่อไม่ให้สแกนอุปกรณ์บางประเภทได้ โดยกำหนดค่าตัวกรอง (filter) 

`filter = [accept|reject] <ประเภทอุปกรณ์> <ค่า>`

---

## ลบ Physical Volumes ออกจาก Volume Group

`vgreduce` จะลดขนาดความจุของ Volume Groups โดยการลบ Physical Volumes ที่ว่างอย่างน้อยหนึ่งโวลุ่ม

 ```
vgreduce my_volume_group /dev/hda1
```
- คำสั่งนี้จะลบ Physical Volumes `/dev/hda1` ออกจากกลุ่ม Volume Group `my_volume_group`

Physical Volumes ที่ถูกลบจะพร้อมใช้งานใหม่สำหรับ Volume Groups อื่นๆ หรือถูกลบออกจากระบบโดยสมบูรณ์

> [!TIP]
>ประโยชน์:
>- เพิ่มพื้นที่ว่างที่ไม่จำเป็นให้กับระบบ
>- ช่วยให้จัดการพื้นที่จัดเก็บข้อมูลได้อย่างมีประสิทธิภาพมากขึ้น
>- ลดความซับซ้อนในการจัดการ Volume Group ต่างๆ

ก่อนที่จะลบ Physical Volume ออก ควรตรวจสอบให้แน่ใจว่า Physical Volume นั้นไม่ได้ถูกใช้งานโดย Logical Volume ใดๆ

ใช้คำสั่ง `pvdisplay` แสดงข้อมูลเกี่ยวกับ Physical Volume ทั้งหมดในระบบ 

```
# pvdisplay /dev/hda1

-- Physical volume ---
PV Name               /dev/hda1
VG Name               myvg
PV Size               1.95 GB / NOT usable 4 MB [LVM: 122 KB]
PV#                   1
PV Status             available
Allocatable           yes (but full)
Cur LV                1
PE Size (KByte)       4096
Total PE              499
Free PE               0
Allocated PE          499
PV UUID               Sd44tK-9IRw-SrMC-MOkn-76iP-iftz-OVSen7
```

หากยังต้องการใช้ Physical volume อยู่ ต้องย้ายข้อมูลไปยัง Physical volume อื่นโดยใช้คำสั่ง `pvmove` 

ตัวอย่างการใช้งาน:

```
pvmove --size 10G /dev/sdc1 /dev/sdd1
```

- คำสั่งนี้จะย้ายข้อมูล 10GB จาก `/dev/sdc1` ไปยัง `/dev/sdd1`
### การลบ Physical volume ที่ขาดหายหรือเสียหายของ LVM 

**Physical volume ที่ขาดหาย (ไม่มีข้อมูล)**
- หาก Logical Volume ใดๆ ไม่ได้ถูกจัดสรรบน Physical volume ที่ขาดหาย สามารถใช้ `--removemissing` ในคำสั่ง `vgreduce` เพื่อลบ Physical volume นั้นออกจาก Volume Group ได้

- ตัวอย่างการใช้งาน: `vgreduce --removemissing my_vg`

**Physical volume ที่ขาดหาย (มีข้อมูล mirror)**
- หาก Physical volume ที่ขาดหาย ประกอบด้วย mirror image ของ Logical Volume แบบ mirror segment
- สามารถใช้ `--removemissing --mirrorsonly --force` ในคำสั่ง `vgreduce` เพื่อลบเฉพาะ mirror image ออกจาก Physical volume
- `--mirrorsonly` ระบุให้ลบเฉพาะ mirror image
- `--force` ข้ามการยืนยันการดำเนินการ
- ตัวอย่างการใช้งาน: `vgreduce --removemissing --mirrorsonly --force my_vg`

>[!TIP]
> **Mirror image แบบ mirror segment** คือ สำเนาข้อมูลของ Logical Volume ที่ถูกแบ่งออกเป็นส่วนย่อยๆ กระจายเก็บไว้บน Physical Volume หลายๆ ตัว เปรียบเสมือนการทำสำเนาข้อมูลสำรองเพื่อป้องกันข้อมูลสูญหายในกรณีที่ Physical Volume ตัวใดตัวหนึ่งเกิดขัดข้อง

---
## การเปิดใช้งานและปิดใช้งาน Volume Groups

การปิดใช้งานหรือเปิดใช้งาน Volume Groups ให้ใช้ argument `-a` หรือ `--available` ของคำสั่ง `vgchange`

**ตัวอย่างการปิดใช้งาน:**
```
vgchange -a n my_volume_group
```
- คำสั่งนี้จะปิดใช้งาน my_volume_group ตัวอักษร n ย่อมาจาก --available หมายถึงไม่พร้อมใช้งาน

**ตัวอย่างการเปิดใช้งาน:**

```
vgchange -a y my_volume_group
```
- คำสั่งนี้จะเปิดใช้งาน my_volume_group ตัวอักษร y ย่อมาจาก --available หมายถึงพร้อมใช้งาน

>[!WARNING]
>- ปิดใช้งาน Volume Groups เฉพาะเมื่อจำเป็นจริงๆ
>- ตรวจสอบให้แน่ใจว่าไม่มี Logical Volume ใดกำลังถูกใช้งานขณะปิดใช้งาน Volume Groups
>- สำรองข้อมูลสำคัญก่อนดำเนินการ

**การเปิดใช้งานและปิดใช้งาน Volume Group สำหรับ clustered locking**

การเปิดใช้งาน/ปิดใช้งาน Volume Group:
- `-e` (หรือ `--exclusive`): เปิดใช้งาน/ปิดใช้งาน Volume Group  เฉพาะบนโหนดเดียว
- `-l` (หรือ `--local`): เปิดใช้งาน/ปิดใช้งาน Volume Group เฉพาะบนโหนดปัจจุบัน

**ตัวอย่างการใข้งาน:**
เปิดใช้งาน  my_vg แบบ exclusive บนโหนดปัจจุบัน
```
vgchange -a e -l my_vg
```
**ปิดใช้งาน my_vg แบบ local:**
```
vgchange -a n -l my_vg
```

> [!NOTE]
> ล็อกแบบคลัสเตอร์ (clustered locking):
>- เป็นคุณสมบัติของ LVM ที่ช่วยให้ควบคุมการเข้าถึง Volume Group ร่วมกันระหว่างโหนดต่างๆ ในคลัสเตอร์
ช่วยป้องกันความขัดแย้งในการเขียนข้อมูลลงใน Volume Group เดียวกันจากหลายโหนด
>- เป็นคุณสมบัติของ LVM ที่ช่วยให้ควบคุมการเข้าถึง Volume Group ร่วมกันระหว่างโหนดต่างๆ ในคลัสเตอร์
ช่วยป้องกันความขัดแย้งในการเขียนข้อมูลลงใน Volume Group เดียวกันจากหลายโหนด

---
## การเปลี่ยนพารามิเตอร์ของ  Volume Group

`vgchange` สามารถเปลี่ยนพารามิเตอร์ต่างๆ ของ Volume Group ที่มีอยู่ได้
ตัวอย่างเช่น เปลี่ยนชื่อ Volume Group, ปรับขนาดพื้นที่ว่างขั้นต่ำ, กำหนดค่าการล็อก, เป็นต้น

**ตัวอย่างการใช้งาน:**
```
vgchange -M 128 vg00
```
- เปลี่ยนค่าพารามิเตอร์ -M (maximum number of logical volumes)
- กำหนดให้ vg00 สามารถสร้าง Logical Volume ได้สูงสุด 128 โวลุ่ม

> [!TIP]
> - เปลี่ยนชื่อ `vg00` เป็น `vg01`: `vgchange -n vg01 vg00`
> - ปรับขนาดพื้นที่ว่างขั้นต่ำของ `vg00` เป็น 10%: `vgchange -R 10% vg00`
> - เปิดใช้งานการล็
อกแบบคลัสเตอร์สำหรับ `vg00`: `vgchange -x y vg00`


---
## การลบ Volume groups
คำสั่ง `vgremove` ใช้สำหรับลบ Volume Group ออกจากระบบ เฉพาะเมื่อไม่มี Logical Volume อยู่ภายใน

```
vgremove <volume_group_name>
```

---
## การแยก Volume group

`vgsplit` ใช้สำหรับแบ่ง Physical Volume ภายใน Volume group และสร้าง Volume group ใหม่

```
vgsplit <volume_group_name> <new_volume_group_name> <physical-volume>
```

> [!NOTE]
>- Logical Volume ไม่สามารถแบ่งระหว่าง Volume group ได้
>- แต่ละ Logical Volume ต้องอยู่บน Physical Volume ทั้งหมดภายใน Volume group เดิมหรือ Volume group ใหม่
>- ใช้คำสั่ง `pvmove` ย้ายข้อมูลระหว่าง Physical Volume เพื่อเตรียมการแบ่ง Logical Volume ที่ซับซ้อน

**ตัวอย่างการใช้งาน:**
```
vgsplit bigvg smallvg /dev/sdc1 /dev/sdd1
```

- คำสั่งข้างต้นจะแบ่ง bigvg โดยสร้าง  ใหม่ชื่อ smallvg
- `/dev/sdc1` และ `/dev/sdd1` จะถูกย้ายจาก `bigvg` ไปยัง `smallvg`

---
## การรวมกลุ่ม Volume group

`vgmerge` จะรวม Volume group ดึงข้อมูล (source) ที่ไม่ได้ใช้งาน เข้ากับ Volume group ปลายทาง (destination) ที่ใช้งานอยู่หรือไม่ได้ใช้งาน

> [!IMPORTANT] ขนาดของหน่วยพื้นที่ทางกายภาพ (physical extent sizes) ของทั้งสอง Volume group ต้องเท่ากัน และข้อมูลของ Physical Volume และ Logical Volume ภายในทั้งสอง Volume group ต้องไม่เกินขีดจำกัดของ Volume group ปลายทาง
```
vgmerge <volume_group_name_1> <volume_group_name_2>
```
**ตัวอย่างการใช้งาน:**
```
vgmerge vg01 vg02
```
- รวม vg01 (ดึงข้อมูล) เข้ากับ vg02 (ปลายทาง)

---
## การสำรองข้อมูล Volume Group Metadata

คำสั่ง `vgcfgbackup` และ `vgcfgrestore` ในการสำรองและกู้คืนข้อมูล Volume Group Metadata ใน LVM

**การสำรองข้อมูลเมตาดาต้าอัตโนมัติ:**

LVM สร้างการสำรองข้อมูลเมตาดาต้าอัตโนมัติทุกครั้งที่มีการเปลี่ยนแปลงการกำหนดค่าของ Volume Group หรือ Logical Volume
- สามารถปิดใช้งานการสำรองข้อมูลอัตโนมัติได้ในไฟล์ `lvm.conf`
- โดยค่าเริ่มต้น ไฟล์สำรองข้อมูลเมตาดาต้าจะถูกเก็บไว้ใน `/etc/lvm/backup`
- ไฟล์เก็บถาวรเมตาดาต้าจะถูกเก็บไว้ใน `/etc/lvm/archive`

**การสำรองข้อมูลเมตาดาต้าด้วยตนเอง:**

คำสั่ง `vgcfgbackup` ใช้สำหรับสำรองข้อมูล Volume Group Metadata ไปยังไฟล์ที่กำหนด
```
vgcfgbackup my_vg
``` 
- สำรองข้อมูล Volume Group Metadata  `my_vg` ไปยัง `/etc/lvm/backup/my_vg.bak`
- สามารถระบุชื่อไฟล์สำรองข้อมูลที่ต้องการด้วยตัวเลือก `-f`


**การกู้คืนข้อมูลเมตาดาต้า:**

คำสั่ง `vgcfgrestore` ใช้สำหรับกู้คืนข้อมูล Volume Group Metadata  จากไฟล์สำรองข้อมูลหรือไฟล์เก็บถาวร
```
vgcfgrestore my_vg /etc/lvm/backup/my_vg.bak
``` 
- กู้คืนข้อมูลเมตาดาต้าของ `my_vg` จากไฟล์ `/etc/lvm/backup/my_vg.bak`
- สามารถระบุไฟล์เก็บถาวรด้วยตัวเลือก `-a`

---
## การเปลี่ยนชื่อ Volume Group
ใช้คำสั่ง `vgrename` เพื่อเปลี่ยนชื่อ Volume Group ที่มีอยู่

```
vgrename <my_volume_group_name> <new_volume_group_name>
```
- คำสั่งนี้จะเปลี่ยนชื่อกลุ่มวอลุ่ม my_volume_group_name เป็น new_volume_group_name
```
vgrename -n <new_volume_group_name> <my_volume_group_name>
```
- คำสั่งนี้เหมือนกับตัวอย่างก่อนหน้า แต่ใช้ตัวเลือก -n เพื่อระบุชื่อใหม่

>[!WARNING]
>- ตรวจสอบให้แน่ใจว่าชื่อใหม่ที่ต้องการตั้งนั้นยังไม่มีกลุ่มวอลุ่มอื่นใช้งานอยู่
>- การเปลี่ยนชื่อกลุ่มวอลุ่มอาจส่งผลต่อการกำหนดค่าของแอปพลิเคชันอื่นๆ ที่ใช้กลุ่มวอลุ่มนั้นอยู่ ดังนั้นควรแจ้งเตือนและสำรองข้อมูลไว้ก่อนดำเนินการ


---
## การย้าย Volume Group ไปยังระบบอื่น

ทำได้โดยใช้คำสั่ง `vgexport` และ `vgimport`

> [!NOTE]
>สามารถใช้อาร์กิวเมนต์ `--force` ของคำสั่ง `vgimport` ซึ่งช่วยให้คุณสามารถนำเข้า Volume Group ที่ขาดหายไป Physical Volume และเรียกใช้คำสั่ง `vgreduce --removemissing` ในภายหลัง

คำสั่ง `vgexport` ทำให้ volume group ที่ inactive ไม่สามารถเข้าถึงระบบได้ ซึ่งจะทำให้สามารถถอด physical volume ออกได้ 

ส่วนคำสั่ง `vgimport` ทำให้เครื่องสามารถเข้าถึง Volume group ได้อีกครั้ง หลังจากการใช้ `vgexport` ที่ทำให้ inactive

หากต้องการย้ายกลุ่มวอลุ่มจากระบบหนึ่งไปยังอีกระบบหนึ่ง ให้ดำเนินการขั้นตอนต่อไปนี้

**เตรียมระบบต้นทาง**

1. หยุดการใช้งานลอจิคัลโวลุ่ม (Logical Volume):
    -    ตรวจสอบให้แน่ใจว่าไม่มีผู้ใช้ใดเข้าถึงไฟล์บนโวลุ่มที่ใช้งานอยู่ใน Volume group 
    - ปลด (Unmount) ลอจิคัลโวลุ่มทั้งหมดภายใน Volume group  เพื่อป้องกันการเขียนข้อมูลขณะย้าย
2. ปิดใช้งาน Volume group:
    - ใช้คำสั่ง `vgchange -a n <ชื่อ  Volume group>` เพื่อปิดใช้งาน Volume group  
    - ตัวเลือก `-a n` กำหนดให้  Volume group   ไม่พร้อมใช้งาน (not available)
    - การปิดใช้งานจะป้องกันกิจกรรมใดๆ เกิดขึ้นกับ  Volume group  
3. ส่งออก Volume group:
    - ใช้คำสั่ง `vgexport <ชื่อ Volume group>` เพื่อส่งออก Volume group จากระบบ
    - คำสั่งนี้จะสร้างไฟล์เมตาดาต้าของ Volume group  และทำเครื่องหมาย Volume group ว่าไม่พร้อมใช้งานบนระบบต้นทาง
  
หลังจากที่คุณส่งออก Volume group, Physical Volume จะแสดงว่าอยู่ใน Volume group ที่ส่งออกเมื่อดำเนินการคำสั่ง `pvscan`

```
# pvscan
  PV /dev/sda1    is in exported VG myvg [17.15 GB / 7.15 GB free]
  PV /dev/sdc1    is in exported VG myvg [17.15 GB / 15.15 GB free]
  PV /dev/sdd1   is in exported VG myvg [17.15 GB / 15.15 GB free]
  ...
```

**ขั้นตอนการนำเข้าและเปิดใช้งาน Volume group บนระบบปลายทาง:**

1. เชื่อมต่อดิสก์กับระบบปลายทาง:
    - ตรวจสอบให้แน่ใจว่าดิสก์ที่ประกอบด้วย Volume group  ได้เชื่อมต่อกับระบบปลายทางอย่างถูกต้อง
2. ย้ายไฟล์เมตาดาต้า:
    - คัดลอกไฟล์เมตาดาต้าที่ส่งออกจากระบบต้นทาง `(/etc/lvm/backup/<ชื่อ Volume group>.bak)` ไปยังระบบปลายทาง
    - วางไฟล์นี้ไว้ในไดเรกทอรีเดียวกันบนระบบปลายทาง `(/etc/lvm/backup/<ชื่อ Volume group>.bak)`
3. นำเข้ากลุ่มวอลุ่ม:
    - ใช้คำสั่ง `vgimport <ชื่อ Volume group >` บนระบบปลายทางเพื่อนำเข้า Volume group 
    - คำสั่งนี้จะใช้ข้อมูลเมตาดาต้าที่ย้ายมาเพื่อสร้าง Volume group ใหม่บนระบบปลายทาง
4. เปิดใช้งานกลุ่มวอลุ่ม:
    - ใช้คำสั่ง `vgchange -a y <ชื่อ Volume group >` เพื่อเปิดใช้งาน Volume group บนระบบปลายทาง
    - ตัวเลือก `-a y` กำหนดให้ Volume group พร้อมใช้งาน (available)
5. สร้างและเชื่อมต่อระบบไฟล์:
    - สร้างระบบไฟล์ Logical Volume ภายใน Volume group  ด้วยคำสั่ง `mkfs`
    - เชื่อมต่อระบบไฟล์ด้วยคำสั่ง `mount` เพื่อให้สามารถใช้งานได้

**ตัวอย่างการใช้งาน:**
```
# ระบบปลายทาง
cp /path/to/<ชื่อ Volume group>.bak /etc/lvm/backup/<ชื่อ Volume group>.bak
vgimport <ชื่อ Volume group>
vgchange -a y <ชื่อ Volume group>
mkfs.ext4 /dev/<ชื่อ Logical volume>
mount /dev/<ชื่อ Logical volume> /mnt/<ชื่อ mount point>
```

---
## การสร้าง Volume Group Directory

`vgmknodes` โดยคำสั่งนี้จะทำการ check special file LVM2 ใน directory /dev ที่จำเป็นสำหรับ logical volume ที่ active โดยมันจะทำการสร้าง special file ที่หายไป เเละทำการลบอันที่ไม่ใช้เเล้ว

>[!TIP]
>- แก้ไขปัญหาไฟล์พิเศษ LVM2 ที่เสียหายหรือสูญหาย
>- ทำให้ LV ใช้งานได้โดยไม่ต้องสร้างใหม่
>- ช่วยในการกู้คืนข้อมูลหลังจากปัญหาฮาร์ดแวร์

ใช้ร่วมกับ `vgscan` ตัวเลือก `-m` หรือ `mknodes` กับ `vgscan` ทำให้ `vgmknodes` ทำงานโดยอัตโนมัติ
สะดวกสำหรับการอัปเดตข้อมูล Volume Group เมื่อเชื่อมต่ออุปกรณ์จัดเก็บข้อมูลใหม่

**ตัวอย่างการใช้งาน:**
- สร้างไฟล์พิเศษสำหรับ Volume Group  my_vg: `vgmknodes my_vg`
- ค้นหาและสร้างไฟล์พิเศษ Volume Group ใหม่: `vgscan -m`

---

## Reference

* Javatpoint. (n.d.). Linux file ownership. Retrieved from https://www.javatpoint.com/linux-file-ownership
* Red Hat. (n.d.). Volume group administration. Retrieved from https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/7/html/logical_volume_manager_administration/vg_admin
* Imeenick. (2012, January 1). Logical volume management (LVM). Retrieved from http://imeenick.blogspot.com/2012/01/logical-volume-management-lvm.html
* Nareerat, P. (2018, February 13). What is LVM. Medium. Retrieved from https://medium.com/@nareerat.prr/what-is-lvm-24ae24322eff
* IDN. (n.d.). LVM - Logical Volume Manager. Retrieved from https://www.idn.id/lvm-logical-volume-manager/

