# 🔧 Volume Group Administration

&emsp; **Volume Group**
คือ กลุ่มของ Physical Volume ที่รวมกันเป็นก้อนๆหนึ่ง โดยภายใน Volume Group พื้นที่ว่างที่สามารจัดสรรได้
จะถูกเเบ่งเป็น unit ที่มีขนาดคงที่ เรียกว่า extents. </br>
&emsp; **extent** คือ unit ที่เล็กที่สุดของพื้นที่ที่สามารถจัดสรรได้ภายใน Physical Volume โดย extents จะถูกเรียกเป็น
Physical extents. </br>
</br>

[//]: # ([![IMAGE ALT TEXT HERE]&#40;https://img.youtube.com/vi/YOUTUBE_VIDEO_ID_HERE/0.jpg&#41;]&#40;https://youtu.be/dQw4w9WgXcQ?si=vB-JQ1_cXYx51HBb&#41;)


<hr>

## การสร้าง Volume Group

&emsp; &emsp; &emsp; ในการสร้าง Volume Group จาก Physical Volume เราจะทำได้โดยการเรียกใช้คำสั่ง

    vgcreate [ชื่อ vg] [Physical Volume ที่ต้องการ] [Physical Volume ที่ต้องการ]....

Example:

- `vgcreate vg1 /dev/sdd1`
- `vgcreate vg1 /dev/sdd1 /dev/sde1`

เมื่อ Physical Volume ถูกนำไปใช้ พื้นที่ว่างของมันจะถูกเเบ่งเป็น extent 4MB โดยค่า default ซึ่งเป็นขนาดขั้นต่ำ
โดยสามารถเพิ่มหรือลดค่าได้
> [!TIP]
> - ขนาดที่ใหญ่ของ extent ไม่มีผลต่อประสิทธิภาพ I/O ของ Logical Volume.
>- สามารถกำหนดขนาดของ extent ได้ด้วยการใส่ option `-s`
> - จำกัดจำนวน Logical Volume ใน Volume Group ได้ด้วยการ ใช้ option `-l`
> - จำกัดจำนวน Physical Volume ใน Volume Group ได้ด้วยการ ใช้ option `-p`
> - Volume group ที่ภูกสร้างจะถูกเพิ่มเข้าไปใน `/dev` เช่น สร้าง vg ชื่อ test1 เมื่อทำการดูใน /dev จะพบ test1


<hr>

[//]: # (## การจัดสรร LVM)

[//]: # ()

[//]: # (&emsp; &emsp; &emsp; เมื่อ **Logical Volume Manager&#40;LVM&#41;** จำเป็นที่จะต้องจัดสรร Physical extents สำหรับหนึ่ง logical)

[//]: # (volume หรือมากกว่า จะมีการจัดสรรดังต่อไปนี้ </br>)

[//]: # ()

[//]: # (- ชุดของ Physical extent ที่ไม่ได้ถูกจัดสรรถูกสร้างขึ้นเพื่อการพิจารณา ถ้าหากระบุ ranges ของ Physical Volume ไว้ที่ท้าย)

[//]: # (  command line จะทำให้มีเพียงเเต่ Physical extents ที่ไม่ได้จัดสรร ที่อยู่ใน ranges บนPhysical volumes)

[//]: # (  ที่ระบุเท่านั้นที่จะถูกนำมาพิจารณา</br>)

[//]: # ()

[//]: # (- เเต่ละ policy ของการจัดสรร จะพยายามจัดลำดับ โดยเริ่มด้วย policy ที่เข้มงวดที่สุด &#40;_contiguous_&#41; และ จบด้วย policy)

[//]: # (  การจัดสรรที่ ใช้ option `--alloc` หรือ ตั้งเป็นค่า default สำหรับ logical volume หรือ volume group เฉพาะสำหรับเเต่ละ)

[//]: # (  policy, ทำงานจาก)

[//]: # (  logical extent ที่หมายเลขต่ำสุด ของพื้นที่ logical volume ที่ว่าง ที่ต้องการบรรจุ โดยจัดสรรพื้นที่ให้ได้มากที่สุด,)

[//]: # (  ตามข้อจำกัดของ policy การจัดสรร เเละ)

[//]: # (  ถ้าหากต้องการพื้นที่เพิ่ม LVM จะไปยัง policy ถัดไป.)

[//]: # (  </br>)

[//]: # ()

[//]: # ()

[//]: # (- **ข้อจำกัดของ policy การจัดสรร**)

[//]: # (    - Policy ของการจัดสรรเเบบ `contigous` กำหนดให้ตำเเหน่ง physical ของ logical extent ใดๆที่ไม่ใช่ logical extent)

[//]: # (      ตัวเเรกของ logical volume ที่อยุ่ติด)

[//]: # (      ตำเเหน่ง physical ของ logical extent ก่อนหน้านั้นทันที, เมื่อ logical volume ถูก striped หรือ mirrored)

[//]: # (      ข้อจำกัดการจัดสรร `contigous` จะถูกนำไปใช้กับเเต่ละ stripe หรือ mirror image ที่ต้องการพื้นที่.</br>)

[//]: # (    - Policy ของการจัดสรรเเบบ `cling` กำหนดไว้ว่า Physical volume ที่ถูกใช้โดย logical extent จะถูกเพิ่มเข้าไปยัง)

[//]: # (      logical volume ที่ถูกใช้เเล้ว)

[//]: # (      อย่างน้อยหนึ่ง logical extent ก่อนหน้านั้นใน logical volume นั้น. หากมีการกำหนด)

[//]: # (      parameter `allocation/cling_tag_list` Physical volume)

[//]: # (      สองตัวจะถือว่า match กัน ถ้าหากมี tag ใดๆ บนทั้งสอง Physical volume. ซึ่งช่วยให้ groups ของ Physical Volume)

[//]: # (      ที่มีคุณสมบัติคล้ายกัน &#40;เช่น ตำเเหน่ง physical&#41;)

[//]: # (      สามารถ tag เเละถือว่าเทียบเท่ากัน ในการจัดสรร</br>)

[//]: # (    - Policy ของการจัดสรรเเบบ `normal` จะไม่เลือก physiacl extent ที่ share physical volume เดียวกันกับ logical extent)

[//]: # (      ที่ได้รับการจัดสรรให้)

[//]: # (      parallel logical volume &#40;คนละ stripe หรือ mirror image&#41; เเล้วที่ offset เดียวกันภายใน parallel logical volume)

[//]: # (      นั้น</br>)

[//]: # (      มื่อจัดสรร mirror log ในเวลาเดียวกันกับ logical volume เพื่อเก็บข้อมูล mirror log ไว้, policy)

[//]: # (      การจัดสรรจะพยายามเลือก Physical volume ที่ต่างกันสำหรับบันทึก log)

[//]: # (      เเละ ข้อมูลก่อน, ถ้าทำไม่ได้เเละ `allocation/mirror_logs_require_separate_pvs` มีค่า 0 จะอนุญาติให้ log share)

[//]: # (      physical volume ส่วนหนึ่งร่วมกับข้อมูล.</br>)

[//]: # (      ขณะเดียวกัน ถ้าจัดสรร thin pool metadata policy การจัดสรรของ normal จะทำเช่นเดียวกันกับ การจัดสรรของ mirror log)

[//]: # (      ตามค่าของ)

[//]: # (      parameter config `allocation/thin_pool_metadata_require_separate_pvs`)

[//]: # (    - ถ้าหากมี extent ว่างที่เพียงพอต่อ request ของการจัดสรร เเต่ policy การจัดสรร `normal` จะไม่ใช้ เเต่)

[//]: # (      policy `anywhere` จะใช้ เเม้ว่าการวาง 2 stripes)

[//]: # (      ไว้ใน physical volume เดียวกันจะทำให้ประสิทธิภาพลดลงก็ตาม</br>)

[//]: # (    - โดยเราสามารถที่จะเปลี่ยนเเปลง policy ของการจัดสรรได้ผ่านคำสั่ง `vgchange`</br>)

[//]: # (      Example: </br>)

[//]: # (      `vgchange --available y|n` เเก้ไข active status volume group ทั้งหมด </br>)

[//]: # (      `vgchange --available y|n ชื่อvolume-group` เเก้ไข active status volume group ที่ระบุ </br>)

[//]: # ()

[//]: # ()

[//]: # (<hr>)

## การสร้าง Volume Group ใน Cluster

&emsp; &emsp; &emsp; **Cluster** คือกลุ่มของ computer หรือ node Linux, storageที่ทำงานร่วมกันเป็นระบบเดียว . **Clustered
Logical Volume Manager** (CLVM)
ชุดของ extention การทำ clustering ไปยัง LVM extention พวกนี้ทำให้ cluster ของ computer สามารถที่จะจัดการ storage
ที่ใช้ร่วมกันได้ (เช่น SAN) ด้วย LVM โดย CLM
เป็นส่วนหนึ่งของ Resilient Storage Add-On โดย **Resilient Storage Add-On** ช่วยให้ storage ที่ share หรือ ระบบ clustered
file สามารถเข้าถึง storage device
เดียวกันผ่าน network ผ่าน pool ของ ข้อมูล ที่พร้อมให้ใช้งานสำหรับเเต่ละ server ในกลุ่ม</br>

สามารถสร้าง CLVM volume groups ใน cluster environment ด้วยคำสั่ง `vgcreate`
> [!NOTE]
> - ใน Red Hat Enterprise Linux 7 cluster จะถูกจัดการผ่าน Pacemaker
> - Clustered LVM logical Volume จะsupport ร่วมกับ Pacemaker clusters เท่านั้นเเละต้องกำหนด เป็น cluster resource

&emsp; &emsp; &emsp; Volume groups ที่ถูก share โดย สมาชิกของ cluster ควรที่จะถูกสร้างขึ้นด้วย attribute clustered
ด้วยคำสั่ง `vgcreate -cy` หรือ `vgchange -cy`
attribute clustered จะถูกกำหนดให้ อัตโนมัติ ถ้า CLVMD กำลังทำงานอยู่
attribute clustered นี้จะบอกว่า volume group นี้ควรที่จะถูกจัดการเเละ protect โดย CLVMD
เมื่อสร้าง volume group ที่ไม่ได้ถูก share โดย cluster เเละ ควรมองเห็นได้ด้วยเพียงเเค่ host ควรที่จะปิดใช้งาน attribute
cluster ด้วย `vgcreate -cn` หรือ `vgchange -cn`
</br>

โดยปกติเเล้ว volume groups ที่สร้างด้วย attribute clustered บน shared storage จะสามารถเห็นได้โดย computer
ที่สามารถเข้าถึง shared storage ได้
อย่างไรก็ตามเราสามารถที่จะสร้าง volume group ที่เป็น local เเละสามารถเห็นได้เพียงเเค่ node เดียว ใน cluster
ด้วยการใส่ `-cn` ต่อท้าย คำสั่ง `vgcreate`
</br>

Example: `vgcreate -c n vg1 /dev/sdd1 /dev/sde1` _เมื่อใช้คำสั่งนี้บน node จะทำการสร้าง volume group ใน cluster ที่เป็น
local สามารถเห็นได้
เเค่ node ทีใช้งานคำสั่งนี้_
</br>

เราสามารถที่จะเปลี่ยนเป็นเเบบ local หรือ cluster ได้ด้วยการใช้ `-c` ในคำสั่ง `vgchange` </br>
เเละ การที่จะเช็คว่า volume group เป็นเเบบ cluster ไหมสามารถเช็คด้วย การใช้คำสั่ง vgs เเละดูว่า มี c ใน attribute
ไหม</br>

<img justify-content = "center" src = "https://www.redhat.com/sysadmin/sites/default/files/styles/embed_large/public/2021-04/3_vgs.png?itok=IzeTjCrc"></img> </br>
รูปจาก: https://www.redhat.com/sysadmin/resize-lvm-simple</br>

จากในภาพจะเห็นว่าใน attribute ไม่มี attribute `c` อยู่ โดยหากมีจะเป็นบริเวณ attributeจะมีค่าเป็น `wz--nc`
<hr>

## การเพิ่ม Physical Volume ไปยัง Volume Group

&emsp; &emsp; &emsp; การที่จะเพิ่ม Physical volume ไปยัง volume group สามารถทำได้โดยการใช้ vgextend เพื่อเพิ่มความจุ
volume group ด้วยการเพิ่ม physical volume ที่ว่างเข้าไป

    vgextend ชื่อvolume-group physicalvolume

example: `vgextend vg1 /dev/sdf1`

<hr>

## การเเสดง Volume Group

&emsp; &emsp; &emsp; มี 2 คำสั่งที่สามารถเเสดง คุณสมบัติของ Volume group ได้ คือ vgs เเละ vgdisplay

`vgscan` ทำการ scan disk ทั้งหมดหา volume group เเละสร้างไฟล์ cache LVM ใหม่เเละยัง เเสดง volume group

`vgs` จะเเสดงข้อมูล volume group 1 อันต่อหนึ่งบรรทัด

`vgdisplay` จะเเสดงข้อมูล volume group เเละคุณสมบัติต่างๆ เช่น ขนาด, extent, จำนวน physical volume ในรูปเเบบของฟอร์ม
โดยถ้าใช้คำสั่งโดยไม่ระบุ volume group จะเเสดงข้อมูลของ volume group ทั้งหมดที่มีอยู่

<img src=https://www.junosnotes.com/wp-content/uploads/2021/07/List-and-Display-Existing-Volume-Groups-vgdisplay.png></img> </br>
รูปจาก : https://www.junosnotes.com/wp-content/uploads/2021/07/List-and-Display-Existing-Volume-Groups-vgdisplay.png

example:

- `vgdisplay`
- `vgdisplay vg01`

<hr>

## การเเสกน disk สำหรับ volume group เพื่อทำการสร้างไฟล์ cache

&emsp; &emsp; &emsp; คำสั่ง `vgscan` จะทำการสเเกน อุปกรณ์ disk ที่ supported ทั้งหมดในระบบเเละมองหา LVM physical volume
เเละ volume group
การทำเเบบนี้จะเป็นการสร้างไฟล์ cache LVM ใน `/etc/lvm/cache/.cache` ที่เป็นที่เก็บรายการอุปกรณ์ LVM ในปัจจุบันไว้

LVM ทำงานคำสั่ง `vgscan` อัตโนมัติเมื่อเริ่มต้นระบบ เเละ ในบางครั้งขณะ LVM operation เช่นเมื่อ execute คำสั่ง `vgcreate`
หรือ เวลาที่ LVM ตรวจพบความไม่สอดคล้อง

> [!NOTE]
> - อาจจำเป็นที่จะต้อง run คำสั่ง `vgscan` เองเมื่อเปลี่ยน config ของ hardware เเละ เพิ่มหรือ ลบ device จาก node
    ระบบมองเห็น device ใหม่ที่ไม่เห็นเมื่อ บูตระบบ
> - เช่นเมื่อต้องการเพิ่ม disk ใหม่เข้าไปในระบบ บน SAN หรือ เสียบอุปกรณ์ disk เข้าไปใหม่ ที่กำกับไว้ว่าเป็น physical
    volume

สามารถทำการกำหนด filter ในไฟล์ `/etc/lvm/lvm.conf` เพื่อทำการจำกัดการเเสกน เช่นการจำกัดการสเเกนอุปกรณ์ใดอุปกรณ์หนึ่ง

<img src = https://docs.oracle.com/cd/E24902_01/doc.91/e37833/img/vgscan.gif></img> </br>
รูปจาก: https://docs.oracle.com/cd/E24902_01/doc.91/e37833/img/vgscan.gif

<hr>

## การลบ Physical Volume จาก Volume group

&emsp; &emsp; &emsp; การที่เราจะลบ Physical Volume ที่ไม่ใช้เเล้วออกจาก Volume group เราจะใช้คำสั่ง `vgreduce`
ในการลดขนาดความจุของ volume group โดยการลบ physical volume
ที่ว่างออก ซึ่งจะทำให้ physical volume พวกนั้นสามารถนำเอาไปใช้ต่อใน physical volume อื่น หรือ เอาออกจากระบบได้

โดยการที่จะลบ physical volume ออกควรเเน่ใจว่า physical volume เหล่านั้นไม่ได้ถูกนำไปใช้กับ logical volume ใดๆ
โดยเราจะสามารถเช็คได้โดยการใช้คำสั่ง `pvdisplay`

<img src = https://www.golinuxcloud.com/wp-content/uploads/pvdisplay-command-to-display-attributes-of-physical-volumes.png></img> </br>
รูปจาก : https://www.golinuxcloud.com/wp-content/uploads/pvdisplay-command-to-display-attributes-of-physical-volumes.png </br>

โดยถ้าหาก physical volume ถูกใช้อยู่ เราสามารถใช้คำสั่งเพื่อย้ายข้อมูลออกได้ด้วย `pvmove` เเล้วจึงใช้ `vgreduce`
เพื่อเอา physical volume ออก

example:

- `vgreduce ชื่อvolume-group physical-volume`
- `vgreduce vg01 /dev/sde1`

> [!NOTE]
>  - ถ้า logical volume มี physical volume ที่ผิดพลาด ทำให้ใช้ logical volume ไม่ได้
>    - สามารถนำออกได้โดยการใช้ `--removemissing` ใน `vgreduce`
> - ถ้ามี physical volume ที่ผิดพลาดที่มี mirror image อยู่ ของ logical volume ประเภท segment mirror สามารถเอา image
    ออกจาก mirror ได้ด้วย
>   - `vgreduce --removemissing --mirrorsonly --force` โดยจะลบเพียง logical volume ที่เป็น mirror image ออกจาก physical
     volume

<hr>

## การ Activate เเละ Deactivate Volume groups

&emsp; &emsp; &emsp; โดยปกติเเล้วเมื่อทำการสร้าง volume group มันจะ activated ซึ่งหมายความว่า สามารถที่จะเข้าถึง logical
volume ใน volume group นั้นได้
เเต่ก็จะมีบางสถานการณ์ที่อาจต้องทำให้ volume group ไม่ทำงาน เเละทำให้ kernel ไม่รู้จัก โดยสามารถที่จะ active เเละ
deactive ได้ผ่านคำสั่ง

    vgchange -a y|n ชื่อvolume-group   // y คือ active n คือ deactive

หาก clustered locking เปิดใช้งานอยู่ ให้เพิ้ม `e` เพื่อที่จะ active หรือ deactive volume group บน node เดียวเท่านั้น
หรือ `l` เพื่อ active หรือ deactive volume group ใน local node,
logical volume ที่เป็นเเบบ single-host snapshots จะ active โดยเฉพาะเสมอ เพราะสามารถใช้ได้เพียงบน node
เดียวในคราวเดียวเท่านั้น

<hr>

## การเปลี่ยน Parameters ของ Volume group

&emsp; &emsp; &emsp; คำสั่ง `vgchange` นอกจากจะใช้สำหรับ active และ deactive เเล้ว มันยังสามารถที่จะใช้ในการเปลี่ยน
parameters ได้อีกด้วย

example:

- `vgchange -l 128 /dev/vg00` : เป็นการเปลี่ยนจำนวน logical volume สูงสุดของ volume group vg00 เป็น 128

<hr>

## การลบ Volume groups

    vgremove ชื่อของvolume-group ที่ต้องการจะลบ

example:

- `vgremove vg01`

<hr>

## การแบ่ง Volume group

&emsp; &emsp; &emsp; การที่เราจะเเยก physical volume ของ volume group เเละสร้าง volume group ใหม่
สามารถทำได้ด้วยการใช้คำสั่ง `vgsplit`

example:

- `vgsplit ชื่อvolume-group ชื่อvolume-groupใหม่ physical-volume`
- `vgsplit bigvg smallvg /dev/ram15`

> [!NOTE]
> - Logical volume ไม่สามารถเเบ่งระหว่าง volume group เเต่ละ logical volume ต้องอยู่่บน physical volume ทั้งหมดที่เป็น
    volume group เก่า หรือใหม่
> - เเต่ถ้าหากจำเป็น เราสามารถ force การเเบ่งได้ด้วยคำสั่ง `pvmove`

<hr>

## การรวม Volume group

&emsp; &emsp; &emsp; ในการที่จะรวม Volume group สองกลุ่มเข้าด้วยกัน จะใช้คำสั่ง `vgmerge` โดยจะสามารถผสม source ที่เป็น
volume inactive กับ
destination ที่เป็น active หรือ inactive Volume group ถ้าขนาดของ physical extent ของ Volume เท่ากัน และ physical เเละ
logical volume ของ volume group ทั้งสอง
พอดีกับ limit ของ Volume group ปลายทาง

example:

- `vgmerge vg01 vg02` : เป็นการรวม vg02 เข้ากับ vg01

<hr>

## การ Backup Volume group Metadata

&emsp; &emsp; &emsp; การสำรองข้อมูล metadata เเละการจัดเก็บ จะถูกสร้างโดยอัตโนมัติทุกครั้ง ที่มีการเปลี่ยนเเปลง config
กับ volume group หรือ logical volume
เเว่นเเต่ว่าจะถูกปิดใช้งานในไฟล์ `lvm.conf`. โดยปกติเเล้วข้อมูลสำรองของ metadata จะถูกเก็บไว้ใน `/etc/lvm/backup`
เเละการจัดเก็บจะเก็บไว้ที่ `/etc/lvm/archive` </br>

&emsp; &emsp; &emsp; เเต่เราสามารถที่จะ backup เองได้ด้วยการใช้คำสั่ง `vgcfgbackup`
เเละสามารถที่จะใช้คำสั่ง `vgcfgrestore` เพื่อที่จะทำการกู้คืน metadata ของ volume group
จากไฟล์จัดเก็บ ไปยัง Physical volume ทั้งหมดใน Volume group

<hr>

## การเปลี่ยนชื่อ Volume group

    vgrename ชื่อVolume-groupทเก่า ชื่อVolume-groupใหม่

example:

- `vgrename /dev/vg02 /dev/my_volume_group` : เปลี่ยนจาก vg02 เป็น my_volume_group
- `vgrename vg02 my_volume_group`: เปลี่ยนจาก vg02 เป็น my_volume_group

<hr>

## การย้าย Volume group ไปยัง System อื่น

&emsp; &emsp; &emsp; การจะย้าย Volume group ไปยัง system อื่นเเนะนำว่าให้ทำโดยการใช้คำสั่ง `vgexport` เเละ `vgimport`
ในการทำ

> [!NOTE]
> - สามารถที่จะใช้ `--force` เพื่อที่จะให้ `vgimport` บังคับ import volume group ที่มี physical volume ที่หายไป
    เเละใช้ `vgreduce --removemissing` ต่อ

คำสั่ง `vgexport` จำทำให้ volume group ที่เป็นเเบบ inactive ไม่สามารถเข้าถึง system ได้ ซึ่งจะทำให้สามารถที่จะถอด
physical volume ออกได้, ส่วน `vgimport` ทำให้เครื่องสามารถที่
จะเข้าถึง Volume group ได้อีกครั้ง หลังจากการใช้ vgexport ที่ทำให้ inactive

### ขั้นตอนการย้าย volume group จาก system ไปอีก system

1. ตรวจสอบให้เเน่ใจไม่มีใครใช้งานไฟล์บน Volume group จากนั้นทำการ unmount Logical volume
2. ใช้ `vgchange -a n` เพื่อทำการ deactive volume group
3. ใช้ `vgexport` เพื่อที่จะทำการ export volume group เพื่อเป็นการที่จะป้องกันไม่ให้ระบบที่คุณกำลังจะนำออกเข้าถึงได้
    - หลังจากที่ export เเล้ว เมื่อ `pvscan` จะเเสดงให้เห็นว่า Physical volume อยู่ใน Volume group ที่ export
    - example:
        - pvscan </br>
          PV /dev/sda1 is in exported VG myvg [17.15 GB / 7.15 GB free] </br>
          PV /dev/sdc1 is in exported VG myvg [17.15 GB / 15.15 GB free] </br>
          PV /dev/sdd1 is in exported VG myvg [17.15 GB / 15.15 GB free] </br>
          ...
        -
      จาก : https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/7/html/logical_volume_manager_administration/vg_admin#VG_remove_PV
    - เมื่อทำการ shutdown ระบบ คุณสามารถที่จะถอดปลั๊ก disk เเละเชื่อมกับระบบใหม่ได้
4. เมื่อเสียบปลั๊กเข้ากับระบบใหม่ ให้ใช้ `vgimport` เพื่อที่จะนำเข้า volume group
   ไปยังระบบใหม่เเละให้ระบบสามารถเข้าถึงได้
5. ทำการ active Volume group ด้วยการใช้คำสั่ง `vgchange -a y`
6. ทำการ mount เพื่อให้เเน่ใจว่ามันสามารถใช้ได้

<hr>

## การสร้าง Directory Volume group ใหม่

&emsp; &emsp; &emsp; การที่จะสร้าง directory ของ Volume group เเละ logical volume special file ให้ใช้คำสั่ง `vgmknodes`
โดยคำสั่งนี้จะทำการ check
special file LVM2 ใน directory /dev ที่จำเป็นสำหรับ logical volume ที่ active โดยมันจะทำการสร้าง special file ที่หายไป
เเละทำการลบอันที่ไม่ใช้เเล้ว

> [!TIP]
> - เราสามารถที่จะรวมการใช้ `vgmknodes` กับ `vgscan` ได้โดยการที่ใส่ `mknodes` ในคำสั่ง `vgscan`
> - example : `vgscan --mknodes`

<hr>

## 📚 Reference

- https://www.thegeekdiary.com/vgchange-command-examples-in-linux/#google_vignette
- https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/7/html/logical_volume_manager_administration/volume_group_overview
- https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/7/html/logical_volume_manager_administration/vg_admin
- https://us.sios.com/linux-clustering/
- https://access.redhat.com/documentation/th-th/red_hat_enterprise_linux/6/html/logical_volume_manager_administration/lvm_cluster_overview
- https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/8/html/package_manifest/resilient-storage-addon



    
    


