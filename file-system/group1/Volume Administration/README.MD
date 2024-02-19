# Logical Volume Management - LVM
### การจัดการระดับตรรก (Logical Volume Management - LVM)
&nbsp;&nbsp;&nbsp;&nbsp;เป็นเทคนิคการจัดการพื้นที่เก็บข้อมูลบนฮาร์ดดิสก์ โดยมีข้อดีเหนือการแบ่งพาร์ติชันแบบเดิมๆ LVM ทำหน้าที่เหมือนเป็นตัวกลางในการบริหารจัดการพื้นที่ โดยแบ่งฮาร์ดดิสก์หลายๆ ตัวออกมาเป็นกลุ่มที่เรียกว่า "กลุ่มวอลุ่ม" (Volume Group) จากนั้นแบ่งพื้นที่ภายในกลุ่มวอลุ่มนั้นออกเป็น "วอลุ่มตรรก" (Logical Volume) อีกที ซึ่งวอลุ่มตรรกนี้จะมองเหมือนพาร์ติชันทั่วไป แต่มีความยืดหยุ่นและใช้งานได้สะดวกกว่า

![Image](https://cdn.thefastcode.com/static/article_img/43113.jpg)

รูปจาก: [https://www.thefastcode.com/th-thb/article/what-is-logical-volume-management-and-how-do-you-enable-it-in-ubuntu](https://www.thefastcode.com/th-thb/article/what-is-logical-volume-management-and-how-do-you-enable-it-in-ubuntu)

> [!NOTE] 
>ความสามารถพิเศษของ LVM:
>- ย้ายวอลุ่มตรรกไปมาระหว่างฮาร์ดดิสก์: ไม่จำเป็นต้องแบ่งพาร์ติชันตายตัว สามารถย้ายข้อมูลระหว่างฮาร์ดดิสก์ได้โดยไม่กระทบการใช้งาน
>- ขยายและลดขนาดวอลุ่มตรรกแบบ On-the-fly: ปรับขนาดพื้นที่ของวอลุ่มได้ตามต้องการโดยไม่ต้องฟอร์แมตไดร์ฟใหม่
>- สร้าง Snapshot ของวอลุ่มตรรก: สร้างสำเนาข้อมูลของวอลุ่มในขณะนั้น เหมือนการถ่ายภาพสถานะข้อมูล ณ เวลาที่ต้องการ
>- เปลี่ยนฮาร์ดดิสก์แบบ Hot-plug: เปลี่ยนฮาร์ดดิสก์ที่เสียโดยไม่ต้องหยุดการทำงานของระบบ
>- เลือกใช้ Mirroring หรือ Striping: เพิ่มความปลอดภัยหรือประสิทธิภาพการทำงานของวอลุ่มได้ตามต้องการ

![Image](https://cdn.thefastcode.com/static/article_img/43112.jpg)

รูปจาก: [https://www.thefastcode.com/th-thb/article/what-is-logical-volume-management-and-how-do-you-enable-it-in-ubuntu](https://www.thefastcode.com/th-thb/article/what-is-logical-volume-management-and-how-do-you-enable-it-in-ubuntu)

>[!TIP]
>โดยสรุปแล้ว LVM เป็นเทคโนโลยีที่ช่วยให้การจัดการพื้นที่เก็บข้อมูลมีความยืดหยุ่น ปลอดภัย และมีประสิทธิภาพมากขึ้น เหมาะสำหรับผู้ใช้งานที่ต้องการความสะดวกในการบริหารจัดการฮาร์ดดิสก์

### การจัดการระดับตรรก (Logical Volume Management - LVM) แบ่งโครงสร้างเป็น 3 ระดับดังนี้:

1. <b>Physical Volume</b>: ดิสก์จริงหรือพาร์ติชันภายในดิสก์ แต่ละส่วนต้องมีการกำหนดเลเบลด้วยคำสั่ง pvcreate เพื่อให้ LVM จัดการได้ เลเบลนี้จะมีข้อมูลอุปกรณ์และรหัสเฉพาะตัว
2. <b>Volume Group</b>: กลุ่มของดิสก์หรือพาร์ติชันที่ถูกรวมเข้าด้วยกันเพื่อบริหารพื้นที่แบบรวมศูนย์
3. <b>Logical Volume</b>: หน่วยเก็บข้อมูลเสมือนที่มองเหมือนพาร์ติชันทั่วไป สร้างจากพื้นที่ภายในกลุ่มวอลุ่ม

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![Image](https://cdn.thegeekdiary.com/wp-content/uploads/2014/10/LVM-basic-structure.png)
   
รูปจาก: [https://medium.com/@nareerat.prr/what-is-lvm-24ae24322eff](https://medium.com/@nareerat.prr/what-is-lvm-24ae24322eff)

### คำสั่งควบคุม LVM มี 2 แบบ:

1. ชุดคำสั่งย่อยๆ: มีหลายคำสั่งเช่น `pvcreate`, `vgcreate`, `lvcreate`
2. คำสั่ง `lvm`: คำสั่งหลักพร้อมซับคำสั่ง เช่น `lvm vgcreate` ทำงานเหมือนกันกับชุดคำสั่งย่อยๆ เพียงแต่รวมไว้ให้สะดวก
 
### ขั้นตอนการตั้งค่า LVM บน Linux:

1. สร้างและกำหนดค่าดิสก์จริงหรือพาร์ติชันด้วย `pvcreate` : `pvcreate /dev/sdb`
2. รวมดิสก์หรือพาร์ติชันที่เตรียมไว้เป็นกลุ่มวอลุ่มด้วย `vgcreate` : `vgcreate myvg /dev/sdb`
3. สร้างวอลุ่มตรรกภายในกลุ่มวอลุ่มด้วย `lvcreate` : `lvcreate -L 10G -n mylv myvg`

### คำสั่ง LVM จะขึ้นต้นด้วยอักษรที่แสดงระดับการทำงาน:

- `pv`: คำสั่งเกี่ยวกับดิสก์จริงหรือพาร์ติชัน
- `vg`: คำสั่งเกี่ยวกับกลุ่มวอลุ่ม
- `lv`: คำสั่งเกี่ยวกับวอลุ่มตรรก
- `lvm`: คำสั่งทั่วไปของระบบ

>[!TIP]
>ข้อมูลที่จัดทำนี้อาศัยจากบทความต้นฉบับและคำแนะนำจากการประเมิน ผลลัพธ์ที่ได้มุ่งเน้นความถูกต้อง ชัดเจน และเป็นประโยชน์


ตัวอย่างนี้แสดงวิธีการเตรียมฮาร์ดดิสก์ 1TB (/dev/sdb) สำหรับใช้กับ LVM และสร้าง logical volume โดยถือว่าฮาร์ดดิสก์มีพาร์ติชันเดียว (/dev/sdb1) ครอบคลุมพื้นที่ทั้งหมด
1. กำหนดเลเบลพาร์ติชันเป็น LVM physical volume: `sudo pvcreate /dev/sdb1`
ตรวจสอบข้อมูล: `pvdisplay`
2. สร้างกลุ่มวอลุ่ม (volume group): `sudo vgcreate DEMO /dev/sdb1`
ตรวจสอบข้อมูล: `vgdisplay`
4. สร้าง logical volume ขนาด 100GB: `sudo lvcreate -L 100G -n web1 DEMO` ตรวจสอบข้อมูล: `lvdisplay`

 
>[!TIP]
>- การแบ่งพาร์ติชันก่อนสร้างดิสก์จริงไม่ส่งผลต่อประสิทธิภาพ แต่ช่วยให้ใช้งานกับซอฟต์แวร์และระบบปฏิบัติการหลากหลาย
>- คำสั่ง LVM ส่วนใหญ่ใช้กับ logical volume เช่น การกำหนด striping, mirroring, และ contiguous allocation
>- Logical volume สามารถเข้าถึงได้ผ่านอุปกรณ์ /dev/DEMO/web1
>- บทความนี้ยังแนะนำวิธีสร้าง filesystem แบบ ext4 เพื่อแสดงเทคนิคเพิ่มเติมของ LVM

ขั้นตอนสุดท้ายของการตั้งค่า Logical Volume บนฮาร์ดดิสก์ 1TB (/dev/sdb) โดยเน้นที่การเข้าถึงและใช้งาน Logical Volume:

### ตัวเลือกที่น่าสนใจส่วนใหญ่ของ LVM อยู่ที่ระดับ Logical Volume
- การกำหนด striping, mirroring และ contiguous allocation จะทำที่ระดับ Logical Volume

### เข้าถึง Logical Volume
- สามารถเข้าถึง Logical Volume ที่สร้างไว้ผ่านอุปกรณ์ `/dev/DEMO/web1`

### สร้างและ Mount filesystem
- `sudo mkfs /dev/DEMO/web1`: สร้าง filesystem แบบ ext4 บน Logical Volume
- `sudo mkdir /mnt/web1`: สร้าง directory `/mnt/web1` เพื่อเป็น mount point
- `sudo mount /dev/DEMO/web1 /mnt/web1`: Mount Logical Volume onto the mount point, ทำให้สามารถใช้งานพื้นที่ได้เหมือน directory ทั่วไป

> [!TIP]
>โดยสรุป ขั้นตอนเหล่านี้ช่วยให้คุณสามารถจัดการพื้นที่เก็บข้อมูลบนฮาร์ดดิสก์ได้อย่างยืดหยุ่นและมีประสิทธิภาพมากขึ้นผ่าน Logical Volume Management (LVM)

## Reference
หนังสือ: UNIX and Linux_System Administration Handbook

- [https://medium.com/@nareerat.prr/what-is-lvm-24ae24322eff](https://medium.com/@nareerat.prr/what-is-lvm-24ae24322eff)
- [https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/8/html/configuring_and_managing_logical_volumes/assembly_lvm-activation-configuring-and-managing-logical-volumes](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/8/html/configuring_and_managing_logical_volumes/assembly_lvm-activation-configuring-and-managing-logical-volumes)
- `UNIX AND LINUX SYSTEM
ADMINISTRATION
HANDBOOK
FIFTH EDITION BOOK` with James Garnett, Fabrizio Branca, and Adrian Mouat
- [https://www.thefastcode.com/th-thb/article/what-is-logical-volume-management-and-how-do-you-enable-it-in-ubuntu](https://www.thefastcode.com/th-thb/article/what-is-logical-volume-management-and-how-do-you-enable-it-in-ubuntu)