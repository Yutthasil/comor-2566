# Physical Volume Administration
### 1. การสร้าง Physical Volume

หัวข้อย่อยต่อไปนี้จะอธิบายคำสั่งที่ใช้สำหรับการสร้าง Physical Volume

### 1.1 การตั้งค่าประเภทพาร์ติชัน

สำหรับอุปกรณ์ดิสก์ทั้งหมด: หากคุณใช้ทั้งดิสก์เป็น Physical Volume ดิสก์นั้นจะต้องไม่มีตารางพาร์ติชัน
สำหรับพาร์ติชันดิสก์ DOS: รหัสพาร์ติชันควรตั้งค่าเป็น 0x8e โดยใช้คำสั่ง fdisk หรือ cfdisk หรือคำสั่งเทียบเท่า
สำหรับอุปกรณ์ดิสก์ทั้งหมด: เฉพาะตารางพาร์ติชันเท่านั้นที่จะต้องถูกลบ ซึ่งจะทำลายข้อมูลทั้งหมดบนดิสก์นั้นอย่างแท้จริง การใช้คำสั่ง dd ดังกล่าวจะลบข้อมูลทั้งหมดบนดิสก์ โปรดดำเนินการอย่างระมัดระวังและแน่ใจว่าคุณสำรองข้อมูลไว้เรียบร้อยก่อน คุณสามารถลบตารางพาร์ติชันที่มีอยู่โดยการเซ็ตเซกเตอร์แรกเป็นศูนย์ด้วยคำสั่งต่อไปนี้:

```
# dd if=/dev/zero of=PhysicalVolume bs=512 count=1
```

 ### 1.2 การเตรียมใช้งาน Physical Volumes

 คำสั่ง pvcreate ใช้สำหรับเตรียมอุปกรณ์บล็อก (ดิสก์หรือพาร์ติชัน) ให้สามารถใช้งานเป็น Physical Volume ภายในระบบ LVM ซึ่งขั้นตอนนี้เปรียบได้กับการฟอร์แมตไดร์ฟสำหรับใช้งานกับระบบแฟ้มข้อมูล โดยคำสั่งตัวอย่างด้านล่างจะทำการสร้าง Physical Volume จากอุปกรณ์บล็อก 3 ตัว ได้แก่ /dev/sdd, /dev/sde และ /dev/sdf เพื่อให้พร้อมใช้งานสำหรับการสร้าง Logical Volume ในภายหลัง:
```
 # pvcreate /dev/sdd /dev/sde /dev/sdf
 ```

> [!TIP]
> ก่อนใช้งานคำสั่งนี้ โปรดตรวจสอบให้แน่ใจว่าคุณสำรองข้อมูลบนอุปกรณ์เหล่านั้นเรียบร้อยแล้ว เนื่องจากกระบวนการนี้จะลบข้อมูลทั้งหมดบนอุปกรณ์
อุปกรณ์บล็อกที่ใช้สามารถเป็นทั้งดิสก์ทั้งหมดหรือพาร์ติชันภายในดิสก์
คำสั่ง pvcreate มีตัวเลือกเพิ่มเติมมากมายสำหรับการกำหนดค่า Physical Volume โดยละเอียด สามารถศึกษาข้อมูลเพิ่มเติมได้จากหน้า man page ของคำสั่ง

แทนที่จะใช้ทั้งดิสก์ คุณสามารถสร้าง Physical Volume จากพาร์ติชันภายในดิสก์ได้ โดยใช้คำสั่ง pvcreate ร่วมกับชื่อพาร์ติชันนั้น ตัวอย่างต่อไปนี้แสดงการสร้าง Physical Volume จากพาร์ติชัน /dev/hdb1 เพื่อใช้กับ Logical Volume ภายหลัง:
 ```
# pvcreate /dev/hdb1
 ```

### 1.3 การสแกนหาอุปกรณ์ที่ถูกบล็อก
คุณสามารถสแกนหาบล็อกอุปกรณ์ที่อาจใช้เป็น Physical Volumeได้ด้วยคำสั่ง `lvmdiskscan` ดังแสดงในตัวอย่างต่อไปนี้:
```
# lvmdiskscan
  /dev/ram0                    [       16.00 MB]
  /dev/sda                     [       17.15 GB]
  /dev/root                    [       13.69 GB]
  /dev/ram                     [       16.00 MB]
  /dev/sda1                    [       17.14 GB] LVM physical volume
  /dev/VolGroup00/LogVol01     [      512.00 MB]
  /dev/ram2                    [       16.00 MB]
  /dev/new_vg/lvol0            [       52.00 MB]
  /dev/ram3                    [       16.00 MB]
  /dev/pkl_new_vg/sparkie_lv   [        7.14 GB]
  /dev/ram4                    [       16.00 MB]
  /dev/ram5                    [       16.00 MB]
  /dev/ram6                    [       16.00 MB]
  /dev/ram7                    [       16.00 MB]
  /dev/ram8                    [       16.00 MB]
  /dev/ram9                    [       16.00 MB]
  /dev/ram10                   [       16.00 MB]
  /dev/ram11                   [       16.00 MB]
  /dev/ram12                   [       16.00 MB]
  /dev/ram13                   [       16.00 MB]
  /dev/ram14                   [       16.00 MB]
  /dev/ram15                   [       16.00 MB]
  /dev/sdb                     [       17.15 GB]
  /dev/sdb1                    [       17.14 GB] LVM physical volume
  /dev/sdc                     [       17.15 GB]
  /dev/sdc1                    [       17.14 GB] LVM physical volume
  /dev/sdd                     [       17.15 GB]
  /dev/sdd1                    [       17.14 GB] LVM physical volume
  7 disks
  17 partitions
  0 LVM physical volume whole disks
  4 LVM physical volumes
```

### 2. Displaying Physical Volumes

---

มีคำสั่งสามคำสั่งที่คุณสามารถใช้เพื่อแสดงคุณสมบัติของPhysical Volumes LVM: `pvs`, `pvdisplay` และ `pvscan`

<b>คำสั่ง `pvs`</b> ใช้แสดงข้อมูลเกี่ยวกับ Physical Volume (PV) ภายในระบบ LVM โดยแสดงผลลัพธ์เป็นรายบรรทัด

<b>คุณสมบัติเด่นของคำสั่ง pvs</b>:

แสดงข้อมูล PV แบบย่อ เหมาะสำหรับการตรวจสอบเบื้องต้น
สามารถปรับแต่งรูปแบบการแสดงผลได้หลากหลาย (ดูรายละเอียดเพิ่มเติมใน Section 4.8 ของเอกสารอ้างอิง)
เหมาะสำหรับเขียนสคริปต์ เนื่องจากสามารถกำหนดรูปแบบเฉพาะตามความต้องการ
 ตัวอย่างผลลัพธ์ของคำสั่ง pvs:
```
   PV         VG   Fmt Attr PSize  PFree
  /dev/sda2  vg0 lvm2 a--   200G     0
  /dev/sdb1  vg1 lvm2 a--   100G    50G
```

<b>อธิบายผลลัพธ์:</b>

- <b>PV</b>: ชื่อของ Physical Volume
- <b>VG</b>: Volume Group ที่ PV สังกัด (ว่างเปล่าถ้ายังไม่ถูกเพิ่มเข้า VG)
- <b>Fmt</b>: ฟอร์แมตของ PV (เช่น lvm2)
- <b>Attr</b>: แอทริบิวต์ของ PV (เช่น a-- หมายถึง อ่านได้ เขียนได้ ไม่สามารถสำรองข้อมูลได้)
- <b>PSize</b>: ขนาดทั้งหมดของ PV
- <b>PFree</b>: พื้นที่ว่างของ PV

<b>ตัวเลือกเพิ่มเติม:</b>
- `-o`, `--options`: ระบุฟิลด์ที่ต้องการแสดงผล ตัวอย่าง: pvs -o name,vg,size
- `-h`, `--human`: แสดงขนาดหน่วยเป็นแบบอ่านง่าย (MB, GB, TB)
- `-a`, `--all`: แสดง PV ทั้งหมด รวมถึง PV ที่ไม่ได้อยู่ใน VG

คำสั่ง `pvdisplay`:
แสดงรายละเอียดของ Physical Volume (PV) แต่ละตัวในระบบ LVM แบบหลายบรรทัด
แสดงข้อมูลคุณสมบัติพื้นฐาน เช่น ขนาด, กลุ่ม Volume Group, ฟอร์แมต, สถานะการใช้งาน
รูปแบบการแสดงผลคงที่ ไม่สามารถปรับแต่งได้

<b>ตัวอย่างผลลัพธ์:</b>
```
# pvdisplay
  --- Physical volume ---
  PV Name               /dev/sdc1
  VG Name               new_vg
  PV Size               17.14 GB / not usable 3.40 MB
  Allocatable           yes
  PE Size (KByte)       4096
  Total PE              4388
  Free PE               4375
  Allocated PE          13
  PV UUID               Joqlch-yWSj-kuEn-IdwM-01S9-XO8M-mcpsVe
```

<b>คำสั่ง pvscan:</b>

- สแกนอุปกรณ์บล็อกทั้งหมดในระบบที่รองรับ LVM เพื่อค้นหา PV
- แสดงผลลัพธ์เป็นตาราง สรุปชื่อ PV, กลุ่ม Volume Group, ฟอร์แมต, ขนาด และพื้นที่ว่าง

<b>ตัวอย่างผลลัพธ์:</b>
```
# pvscan
 PV /dev/sdb2   VG vg0   lvm2 [964.00 MB / 0   free]
 PV /dev/sdc1   VG vg0   lvm2 [964.00 MB / 428.00 MB free]
 PV /dev/sdc2            lvm2 [964.84 MB]
 Total: 3 [2.83 GB] / in use: 2 [1.88 GB] / in no VG: 1 [964.84 MB]
```

> [!NOTE] 
>- ไฟล์ `lvm.conf` สามารถกำหนดตัวกรองเพื่อให้คำสั่ง `pvscan` ไม่สแกนอุปกรณ์บางตัว
>- ดูรายละเอียดการกำหนดตัวกรองใน Section 4.5 "Controlling LVM Device Scans with Filters"

### 3. การป้องกันการจัดสรรพื้นที่บน Physical Volume
---

คำสั่ง `pvchange` ช่วยควบคุมการจัดสรรพื้นที่ Physical Extents ภายใน Physical Volume (PV) ซึ่งมีประโยชน์ในกรณีต่อไปนี้:

- มีปัญหาเกี่ยวกับดิสก์ เช่น ข้อผิดพลาด
- เตรียมการนำ PV ออกจากระบบ

ตัวอย่างคำสั่งด้านล่างปิดกั้นการจัดสรรพื้นที่บน PV ชื่อ `/dev/sdk1`
```
# pvchange -x n /dev/sdk1
```

<b>อธิบายตัวเลือกคำสั่ง:</b>

- `-x`: ระบุการดำเนินการ ปิดกั้นการจัดสรรพื้นที่
- `n`: ยืนยันคำสั่ง (necessary)
- `/dev/sdk1`: ชื่อของ Physical Volume
 
<b>เปิดใช้งานการจัดสรรพื้นที่อีกครั้ง:</b>

คุณสามารถเปิดใช้งานการจัดสรรพื้นที่บน PV ที่ปิดกั้นไว้เดิม ด้วยตัวเลือก `-xy` ในคำสั่ง `pvchange`

```
# pvchange -xy /dev/sdk1
```

<b>ข้อควรระวัง:</b>

- ใช้คำสั่งนี้ด้วยความระมัดวัง เนื่องจากอาจส่งผลต่อการใช้งานพื้นที่เก็บข้อมูล
- ตรวจสอบให้แน่ใจว่าได้สำรองข้อมูลไว้ก่อนดำเนินการ

### 4. การปรับขนาด Physical Volume (PV) ใน LVM
---
 
คำสั่ง `pvresize` ใช้ปรับขนาด Physical Volume (PV) ภายในระบบ LVM ซึ่งหมายถึงการเปลี่ยนแปลงขนาดพื้นที่ดิสก์ที่ LVM มองเห็น คุณสามารถใช้คำสั่งนี้ได้แม้ LVM ยังใช้งาน PV นั้นอยู่

<b>สถานการณ์ที่อาจต้องใช้คำสั่ง pvresize:</b>

- เพิ่มพื้นที่ดิสก์ให้กับ PV (กรณีขยายดิสก์หรือเพิ่มพาร์ติชัน)
- ลดขนาดพื้นที่ดิสก์ของ PV (กรณีจำเป็นต้องใช้พื้นที่สำหรับวัตถุประสงค์อื่น)
 
<b>ข้อควรระวัง:</b>

- การปรับขนาด PV อาจส่งผลต่อข้อมูลที่มีอยู่ ตรวจสอบให้แน่ใจว่าได้สำรองข้อมูลไว้ก่อน
- ไม่สามารถลดขนาด PV ให้เล็กกว่าขนาดข้อมูลที่ใช้งานอยู่
- การเพิ่มขนาด PV ต้องพิจารณาความเข้ากันได้ของฮาร์ดแวร์และระบบไฟล์
 
<b>ตัวอย่างคำสั่ง:</b>

- เพิ่มขนาด PV `/dev/sda` เป็น 200GB: `pvresize /dev/sda +200G`
- ลดขนาด PV `/dev/sdb` เป็น 50GB: `pvresize /dev/sdb -50G`

### 5. การนำ Physical Volume ออกจากระบบ LVM
---

เมื่อต้องการนำอุปกรณ์ดิสก์ (Physical Volume: PV) ออกจากระบบ LVM ทำได้ดังนี้:

<b>กรณี PV ว่างเปล่า:</b>

1. ใช้คำสั่ง `pvremove` เพื่อลบเลเบล LVM ออกจาก PV คำสั่งนี้จะลบข้อมูลเมตาเดต้าของ LVM บน PV ที่ว่างเปล่า
2. ตัวอย่าง: `pvremove /dev/ram15` (จากตัวอย่างคำสั่งที่ให้)
 
<b>กรณี PV มีข้อมูลอยู่:</b>

1. ตรวจสอบว่า PV เป็นสมาชิกของ Volume Group (VG) หรือไม่
2. <b>ถ้าเป็นสมาชิกของ VG:</b>
- นำ PV ออกจาก VG ด้วยคำสั่ง `vgreduce` (ดูรายละเอียดใน Section 4.3.7 ของเอกสารอ้างอิง LVM)
- หลังจากนั้นจึงใช้ `pvremove` เพื่อลบเลเบล LVM
3. <b>ถ้าไม่เป็นสมาชิกของ VG:</b>
ใช้ `pvremove` เพื่อลบเลเบล LVM ได้โดยตรง

<b>ข้อควรระวัง:</b>

- การใช้ `pvremove` จะลบข้อมูลเมตาเดต้าของ LVM บน PV
- ตรวจสอบให้แน่ใจว่าได้สำรองข้อมูลไว้ก่อนดำเนินการ
- กรณี PV มีข้อมูลอยู่ ห้ามใช้ `pvremove` โดยตรง ควรนำออกจาก VG ก่อน

## Reference
- [https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/7/html/logical_volume_manager_administration/physvol_admin#doc-wrapper](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/7/html/logical_volume_manager_administration/physvol_admin#doc-wrapper)

- [https://medium.com/@yhakimi/lvm-how-to-create-and-extend-a-logical-volume-in-linux-9744f27eacfe](https://medium.com/@yhakimi/lvm-how-to-create-and-extend-a-logical-volume-in-linux-9744f27eacfe)

- [https://www.digitalocean.com/community/tutorials/an-introduction-to-lvm-concepts-terminology-and-operations](https://www.digitalocean.com/community/tutorials/an-introduction-to-lvm-concepts-terminology-and-operations)
- `UNIX AND LINUX SYSTEM
ADMINISTRATION
HANDBOOK
FIFTH EDITION BOOK` with James Garnett, Fabrizio Branca, and Adrian Mouat
- [https://man7.org/linux/man-pages/man1/tar.1.html](https://man7.org/linux/man-pages/man1/tar.1.html)
- [https://www.ibm.com/docs/es/aix/7.1?topic=subsystem-physical-volumes](https://www.ibm.com/docs/es/aix/7.1?topic=subsystem-physical-volumes)