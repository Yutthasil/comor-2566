# I/O
## lsusb
</div>
บทบาทหน้าที่ของ lsusb<br>
lsusb เป็นคำสั่งในระบบปฏิบัติการ Linux ที่ใช้สำหรับแสดงรายการของอุปกรณ์ USB ที่เชื่อมต่อกับเครื่องคอมพิวเตอร์ บทบาทที่สำคัญคือ
แสดงรายการอุปกรณ์ USB lsusb สามารถดูรายการของอุปกรณ์ USB ทั้งหมดที่เชื่อมต่อกับเครื่อง Linux รวมถึงรายละเอียดเกี่ยวกับแต่ละอุปกรณ์ เช่น Vendor ID, Product ID, และรุ่นของอุปกรณ์นั้นๆ<br><br>

หลักการทำงานของ lsusb<br>
บน linux เมื่อใช้คำสั่ง lsusb ในเครื่อง Linux, ระบบจะทำการสืบค้น (scan) อุปกรณ์ USB ที่เชื่อมต่อกับเครื่อง lsusb จะอ่านข้อมูลเกี่ยวกับอุปกรณ์ USB จากไดรเวอร์ที่ติดตั้งในระบบปฏิบัติการ Linux lsusb จะแสดงข้อมูลเพิ่มเติมเกี่ยวกับแต่ละอุปกรณ์ USB เช่น Vendor ID, Product ID, และรุ่นของอุปกรณ์นั้นๆ<br><br>
```
$ lsusb
```
Output:<br>
![2024-02-07 (2)](https://github.com/CosmoGuy112/PHost/assets/112687372/41b1e3e0-9326-4d7c-bacd-ead9a840fb87)


ซึ่งอาจมีตัวเลือก (options) ต่างๆ ที่สามารถใช้เพื่อกำหนดการแสดงผลหรือการทำงานของคำสั่งได้ บางตัวเลือกที่มักใช้คือ <br>


Options: -v: ตัวเลือกนี้ใช้สำหรับแสดงผลลัพธ์ในโหมด verbose และยังแสดงข้อมูลรายละเอียดเกี่ยวกับอุปกรณ์ที่เชื่อมต่ออยู่
```
$ lsusb -v
```
Output:<br>
![2024-02-09 (28)](https://github.com/CosmoGuy112/PHost/assets/112687372/23ab1c3d-bc01-487e-864e-bc15bd46a3c6)


Options: -s: ตัวเลือกนี้ใช้สำหรับแสดงเฉพาะอุปกรณ์ที่ระบุโดยหมายเลขของบัสและ/หรืออุปกรณ์เท่านั้น
```
$ lsusb -s 2:2
```
Output:<br>
![3](https://github.com/CosmoGuy112/PHost/assets/112687372/042844f4-47ef-4b89-a7eb-1e9dff638b8a)


Options: -t: ตัวเลือกนี้ใช้สำหรับการดัมพ์ลำดับของอุปกรณ์ USB ในลักษณะของต้นไม้
```
$ lsusb -t
```
Output:<br>
![2](https://github.com/CosmoGuy112/PHost/assets/112687372/57ae1a3f-15b8-46a3-9545-f750011f1745)

Options: -D ตัวเลือกนี้ใช้สำหรับการระบุชื่อไฟล์อุปกรณ์ที่ต้องการดูข้อมูลได้ในรูปแบบของชื่อไฟล์ โดยทั่วไปแล้วไฟล์อุปกรณ์จะอยู่ในรูปแบบ /dev/usb/บัส/อุปกรณ์ หรือ /dev/bus/usb/บัส/อุปกรณ์ โดยที่ "บัส" แทนหมายเลขของบัส USB และ "อุปกรณ์" แทนหมายเลขอุปกรณ์ USB ที่ต้องการดูข้อมูล
```
$ lsusb -D /dev/usb/002/004
```
Output:<br>
![2](https://github.com/CosmoGuy112/PHost/assets/112687372/6aaaf995-46fc-4e0f-a42a-9ee82d7b7778)

ข้อควรระวังในการใช้งาน<br>
ในบางกรณี อาจต้องใช้สิทธิ์ root เพื่อเรียกใช้คำสั่ง lsusb เพราะต้องการสิทธิ์สำหรับการอ่านข้อมูลจาก USB หรือการ์ดส่วนเสริม <br><br>







## lspcmcia
</div>
บทบาทหน้าที่ของ lspcmcia<br>
เป็นคำสั่งในระบบปฏิบัติการ Linux ที่ใช้สำหรับแสดงข้อมูลเกี่ยวกับการต่อการ์ด PCMCIA (Personal Computer Memory Card International Association) ที่เชื่อมต่อกับเครื่องคอมพิวเตอร์ สามารถดูรายการของการ์ด PCMCIA ที่เชื่อมต่อกับเครื่อง Linux ได้ รวมถึงรายละเอียดเกี่ยวกับแต่ละการ์ด เช่น ชื่อของการ์ด, รุ่น, และสถานะของการ์ดนั้นๆ<br><br>

หลักการทำงานของ lspcmcia<br>
บน linux เมื่อใช้คำสั่ง lspcmcia ระบบจะทำการสร้างข้อมูลเกี่ยวกับการ์ด PCMCIA ที่เชื่อมต่อกับเครื่อง<br><br>
```
$ lspci
```
Output:<br>
![2](https://github.com/CosmoGuy112/PHost/assets/112687372/de834e39-f665-4e49-affa-159401db1f7e)

ซึ่งอาจมีตัวเลือก (options) ต่างๆ ที่สามารถใช้เพื่อกำหนดการแสดงผลหรือการทำงานของคำสั่งได้ บางตัวเลือกที่มักใช้คือ <br>

Options: -v ตัวเลือกนี้ใช้สำหรับการแสดงข้อมูลเพิ่มเติมในรูปแบบ verbose เช่น ข้อมูลเกี่ยวกับผู้ผลิต (vendor), รุ่น (model), และคุณสมบัติอื่น ๆ ของอุปกรณ์ PCI
```
$ lspci -v
```
Output:<br>
![4](https://github.com/CosmoGuy112/PHost/assets/112687372/65967001-bb54-4983-8932-d08ba0f12899)


Options: -t ตัวเลือกนี้ใช้สำหรับการแสดงข้อมูลในรูปแบบของต้นไม้ (tree structure) เพื่อแสดงความสัมพันธ์ระหว่างอุปกรณ์ PCI แต่ละตัว
```
$ lspci -t
```
Output:<br>
![6](https://github.com/CosmoGuy112/PHost/assets/112687372/7bae550c-06d5-42e1-a1f2-5c79cfed0ef6)



Options: -vv ตัวเลือกนี้ใช้สำหรับการแสดงข้อมูลเพิ่มเติมในรูปแบบ verbose อย่างละเอียด เช่น ข้อมูลเกี่ยวกับ I/O ports, memory regions, และอื่น ๆ
```
$ lspci -vv
```
Output:<br>
![7](https://github.com/CosmoGuy112/PHost/assets/112687372/620117d9-560c-4fd3-a8b2-3ed9a5f23479)


Options: -nn ตัวเลือกนี้ใช้สำหรับการแสดงข้อมูลในรูปแบบ numeric (ที่ไม่มีการแปลงรหัสเป็นชื่อของอุปกรณ์) เช่น Vendor ID และ Device ID เป็นต้น
```
$ lspci -nn
```
Output:<br>
![8](https://github.com/CosmoGuy112/PHost/assets/112687372/0bee10fc-ee0a-4ca2-9d97-40a686013e60)

Options: -xxx ตัวเลือกนี้ใช้สำหรับการแสดงข้อมูลเพิ่มเติมอย่างละเอียด เช่น ข้อมูลเกี่ยวกับระบบชุดควบคุม (capabilities), การกำหนดค่า (configuration) และข้อมูลอื่น ๆ
```
$ lspci -xxx
```
Output:<br>
![9](https://github.com/CosmoGuy112/PHost/assets/112687372/3705e1fe-33c4-4e67-8cf0-f100732b0f64)

ข้อควรระวังในการใช้งาน<br>
ในกรณีที่จะทำการดำเนินการอะไรกับการ์ด PCMCIA ที่แสดงใน lspcmcia ควรทำการสำรองข้อมูลก่อนเพื่อป้องกันการสูญเสียข้อมูล<br><br>







## lsdev
</div>
บทบาทหน้าที่ของ lsdev<br>
เป็นคำสั่งที่ใช้สำหรับแสดงรายการของอุปกรณ์ที่เชื่อมต่อกับระบบปฏิบัติการ Linux ซึ่งรวมถึงอุปกรณ์ที่เชื่อมต่อผ่านพอร์ต หรือโมดูลของคอมพิวเตอร์เช่น USB, PCI, และอุปกรณ์ต่างๆที่ติดตั้งในระบบ<br><br>

หลักการทำงานของ lsdeva<br>
lsdev จะสแกนระบบเพื่อตรวจสอบอุปกรณ์ที่เชื่อมต่อทั้งหมด แล้วจะแสดงรายการของอุปกรณ์ทั้งหมดที่พบในระบบ รวมถึงรายละเอียดเกี่ยวกับแต่ละอุปกรณ์<br><br>
```
$ lsdev
```
Output:<br>
![3](https://github.com/CosmoGuy112/PHost/assets/112687372/f324b761-eb13-4a5a-b653-8fba2bcfffdb)

ข้อควรระวังในการใช้งาน<br>
อาจแสดงข้อมูลที่มีรายละเอียดมากเกินไปหรือที่ไม่จำเป็นต่อการใช้งาน และอาจทำให้ยุ่งยากในการอ่านและการทำงาน ควรพิจารณาเฉพาะข้อมูลที่เป็นประโยชน์และสำคัญสำหรับงานที่คุณกำลังดำเนินการ<br><br>




## lsblk
</div>
บทบาทหน้าที่ของ lsblk<br>
lsblk เป็นยูทิลิตี้บรรทัดคำสั่งที่ใช้สำหรับแสดงรายการอุปกรณ์บล็อกบนระบบ Linux อุปกรณ์บล็อกประกอบด้วยอุปกรณ์เก็บข้อมูลที่เก็บข้อมูลในรูปแบบของบล็อก ซึ่งโดยทั่วไปคือฮาร์ดดิสก์ไดรฟ์ (HDD) หรือไดรฟ์โซลิดสเทต (SSD)<br><br>

หลักการทำงานของ lsblk<br>
หลักการทำงานของ lsblk คือการสแกนและแสดงข้อมูลเกี่ยวกับอุปกรณ์บันทึกข้อมูลทั้งหมดที่เชื่อมต่อกับระบบ Linux เพื่อให้ผู้ใช้สามารถเข้าใจโครงสร้างของระบบสําหรับการจัดเก็บข้อมูลได้ง่ายขึ้น และจัดการกับพาร์ติชันและอุปกรณ์เกี่ยวกับการเก็บข้อมูลได้อย่างมีประสิทธิภาพ<br><br>
```
$ lsblk
```
Output:<br>
![21](https://github.com/CosmoGuy112/PHost/assets/112687372/2bdfd111-1c81-4783-9069-92c0462b4e62)


Options: -a ตัวเลือกนี้ใช้สำหรับการแสดงข้อมูลของทุกอุปกรณ์ รวมถึงอุปกรณ์ที่ไม่มีการแสดงผลโดยปกติ
```
$ lsblk -a
```
Output:<br>
![20](https://github.com/CosmoGuy112/PHost/assets/112687372/0227e4de-c2a0-4b5c-a100-4ae11dfe83ef)

Options: -b ตัวเลือกนี้ใช้สำหรับการแสดงขนาดของอุปกรณ์ในหน่วยข้อมูลเก็บบิต (bytes)
```
$ lsblk -b
```
Output:<br>
![11](https://github.com/CosmoGuy112/PHost/assets/112687372/ac282848-32d6-433c-988c-e465fb384ff0)

Options: -d ตัวเลือกนี้ใช้สำหรับการไม่แสดงข้อมูลของอุปกรณ์ลูกของแต่ละอุปกรณ์
```
$ lsblk -d
```
Output:<br>
![12](https://github.com/CosmoGuy112/PHost/assets/112687372/e92de6a3-4b6e-41db-9637-ad65e290db36)

Options: -l ตัวเลือกนี้ใช้สำหรับแสดงรายการอุปกรณ์ในรูปแบบของรายการ (list)
```
$ lsblk -l
```
Output:<br>
![13](https://github.com/CosmoGuy112/PHost/assets/112687372/ed86ca2e-f5f7-4cdc-a2d8-6bf133a5761c)

Options: -n ตัวเลือกนี้ใช้สำหรับการไม่แสดงหัวข้อตาราง คำสั่งนี้จะแสดงข้อมูลของอุปกรณ์ block storage โดยไม่มีการแสดงหัวข้อตาราง ซึ่งจะทำให้ผลลัพธ์มีรูปแบบที่เข้าใจง่ายและสั้นกว่าเวอร์ชันที่แสดงหัวข้อตารางออกมา
```
$ lsblk -n
```
Output:<br>
![14](https://github.com/CosmoGuy112/PHost/assets/112687372/6ae13b21-b31f-432a-b1af-7ff6b1e257da)

Options: -r ตัวเลือกนี้ใช้สำหรับการแสดงข้อมูลในรูปแบบของข้อมูลสรุป (raw data)
```
$ lsblk -r
```
Output:<br>
![15](https://github.com/CosmoGuy112/PHost/assets/112687372/a7ef5b10-1bf9-49fe-9816-d42eb9b90546)

Options: -t ตัวเลือกนี้ใช้สำหรับการแสดงข้อมูลเกี่ยวกับโทโปโลจีของอุปกรณ์
```
$ lsblk -t
```
Output:<br>
![16](https://github.com/CosmoGuy112/PHost/assets/112687372/a88e5096-0cce-4768-bdad-01b3c721ee4a)


Options: -p ตัวเลือกนี้ใช้สำหรับการแสดงตำแหน่งของอุปกรณ์เก็บบันทึก block storage
```
$ lsblk -p
```
Output:<br>
![17](https://github.com/CosmoGuy112/PHost/assets/112687372/b8c6d4af-123f-49f8-8d1e-5dc59eda8101)

Options: -S ตัวเลือกนี้ใช้สำหรับการแสดงข้อมูลเฉพาะอุปกรณ์ที่เชื่อมต่อผ่าน SCSI (Small Computer System Interface)
```
$ lsblk -S
```
Output:<br>
![18](https://github.com/CosmoGuy112/PHost/assets/112687372/73ee9053-0641-4856-8f5a-bb7edbc580c8)

Options: -i ตัวเลือกนี้ใช้สำหรับการกลับการเรียงลำดับข้อมูล
```
$ lsblk -i
```
Output:<br>
![19](https://github.com/CosmoGuy112/PHost/assets/112687372/70ca31da-10a2-4b0e-a10c-299361ea4469)


ข้อควรระวังในการใช้งาน<br>
หากมีการทำงานใด ๆ กับอุปกรณ์ในขณะที่ใช้คำสั่ง อาจจะทำให้ไม่ได้แสดงข้อมูลปัจจุบัน<br><br>











## lscpu
</div>
บทบาทหน้าที่ของ lscpu<br>
ให้ข้อมูลเกี่ยวกับ CPU บนระบบ Linux<br><br>

หลักการทำงานของ lscpu<br>
เรียกข้อมูล CPU จากระบบไฟล์ proc และแสดงข้อมูลนั้นในรูปแบบที่เข้าใจง่ายแก่ผู้ใช้งาน
<br><br>
```
$ lscpu
```
Output:<br>
![7](https://github.com/CosmoGuy112/PHost/assets/112687372/ecb470ac-c59a-47a2-9141-104f9c943011)<br>

Options: -e ตัวเลือกนี้ใช้สำหรับการแสดงข้อมูลที่เกี่ยวข้องกับ CPU และแสดงในรูปแบบที่มนุษย์อ่านได้
```
$ lscpu -e
```
Output:<br>
![cpu1](https://github.com/CosmoGuy112/PHost/assets/109953192/a6c5d1cf-aaac-4d9b-9968-4713d9e3683a)<br>

Options: -p ตัวเลือกนี้ใช้สำหรับการแสดงข้อมูลโปรเซสเซอร์ในรูปแบบที่แยกวิเคราะห์ได้ง่าย
```
$ lscpu -p
```
Output:<br>
![cpu2](https://github.com/CosmoGuy112/PHost/assets/109953192/9ca125d7-dfa8-4be5-a984-e0b60f7e3c66)<br>

Options: -x ตัวเลือกนี้ใช้สำหรับการแสดงข้อมูลชุด CPU โดยใช้มาสก์เลขฐานสิบหก
```
$ lscpu -x
```
Output:<br>
![cpu3](https://github.com/CosmoGuy112/PHost/assets/109953192/5cc3683f-9926-4bf6-9792-33d748ca5b62)<br>

Options: -J ตัวเลือกนี้ใช้สำหรับการแสดงข้อมูลข้อมูล CPU ในรูปแบบ JSON
```
$ lscpu -J
```
Output:<br>
![cpu4](https://github.com/CosmoGuy112/PHost/assets/109953192/ce41e4c1-6adb-4bad-9fab-685cbd551f76)<br>

Options: -h ตัวเลือกนี้ใช้สำหรับต้องการพิมพ์ข้อความช่วยเหลือเกี่ยวกับคำสั่ง “lscpu ” และตัวเลือก
```
$ lscpu -h
```
Output:<br>
![cpu5](https://github.com/CosmoGuy112/PHost/assets/109953192/fb749ad9-1b0c-4652-8c4e-9d7ea6ebcc36)<br>

Options: -V ตัวเลือกนี้ใช้สำหรับการแสดงข้อมูลเวอร์ชันของเครื่องมือคำสั่ง “lscpu ”
```
$ lscpu -V
```
Output:<br>
![cpu6](https://github.com/CosmoGuy112/PHost/assets/109953192/d6094c65-19c0-4139-9159-5c7a7e6b5fb0)<br>

ข้อควรระวังในการใช้งาน<br>
อาจจะต้องใช้สิทธิ์การเข้าถึง บางครั้งอาจจะต้องใช้กับคำสั่ง sudo หรืออาจจะต้องให้สิทธิ์แก่ผู้ใช้งานคนอื่น<br><br>












## lsmod
</div>

บทบาทหน้าที่ของ lsmod<br>
การแสดงรายชื่อของโมดูลที่โหลดอยู่ในระบบปฏิบัติการ Linux เพื่อให้ผู้ใช้สามารถดูรายละเอียดเกี่ยวกับโมดูลนั้น ๆ ได้ เช่น ชื่อของโมดูล, ขนาดของโมดูล, และการใช้งานของโมดูล<br><br>

หลักการทำงานของ lsmod<br>
จะทำงานโดยอ่านข้อมูลจากไฟล์ /proc/modules ซึ่งเป็นที่เก็บข้อมูลเกี่ยวกับโมดูลที่โหลดอยู่ในระบบปฏิบัติการ Linux และแสดงผลลัพธ์<br><br>
```
$ lsmod
```
Output:<br>
![8](https://github.com/CosmoGuy112/PHost/assets/112687372/1fee35ec-afee-487a-99bd-af56e9dbde50)
<br>

ข้อควรระวังในการใช้งาน<br>
อาจจะแสดงข้อมูลไม่ตรงตามสถานะปัจจุบัน<br><br>

## lshw
</div>
บทบาทหน้าที่ของ lshw<br>
แสดงข้อมูลรายละเอียดเกี่ยวกับการกำหนดค่าฮาร์ดแวร์ของระบบเครื่องคอมพิวเตอร์หรืออุปกรณ์ Linux อื่น ๆ เช่น ชนิดของหน่วยประมวลผล<br><br>

หลักการทำงานของ lsdev<br>
การสแกน, รวบรวม, และแสดงข้อมูลเกี่ยวกับฮาร์ดแวร์ที่ติดตั้งในระบบของ Linux แล้วแสดงออกมา
<br><br>
```
$ lshw
```
Output:<br>
![2024-02-07 (24)](https://github.com/CosmoGuy112/PHost/assets/112687372/265b8985-3b70-4c23-8eb7-be3c6a229994)<br>

Options: -html ตัวเลือกนี้ใช้สำหรับการแสดงข้อมูลฮาร์ดแวร์ของระบบและแสดงเป็นเอกสาร HTML ซึ่งสามารถเปิดดูในเว็บเบราว์เซอร์ได้
```
$ lshw -html
```
Output:<br>
![hw1](https://github.com/CosmoGuy112/PHost/assets/109953192/d4571b97-b5fd-4e2c-9b74-eb4fcfad4005)<br>

Options: -xml ตัวเลือกนี้ใช้สำหรับการแสดงข้อมูลโปรเซสเซอร์ในรูปแบบที่แยกวิเคราะห์ได้ง่าฮาร์ดแวร์ของระบบในรูปแบบ XML คำสั่งนี้จะสร้างไฟล์ XML ที่บรรจุข้อมูลทั้งหมดเกี่ยวกับฮาร์ดแวร์ของระบบ
```
$ lshw -xml
```
Output:<br>
![hw2](https://github.com/CosmoGuy112/PHost/assets/109953192/9c0ecc9d-e27d-4586-8a04-fee0e8678482)<br>

Options: -businfo ตัวเลือกนี้ใช้สำหรับการแสดงข้อมูลเกี่ยวกับชนิดของอินเทอร์เฟซบัสที่ใช้ในการเชื่อมต่อกับอุปกรณ์ฮาร์ดแวร์ของระบบ
```
$ lshw -businfo
```
Output:<br>
![hw4](https://github.com/CosmoGuy112/PHost/assets/109953192/011c5ac5-163f-48cd-86f6-69afa8bdc8e2)<br>

Options: -shot ตัวเลือกนี้ใช้สำหรับการแสดงรายการอุปกรณ์ฮาร์ดแวร์ที่ติดตั้งในระบบและเส้นทางของแต่ละอุปกรณ์ฮาร์ดแวร์ภายในโครงสร้างของฮาร์ดแวร์ในระบบ
```
$ lshw -shot
```
Output:<br>
![hw3](https://github.com/CosmoGuy112/PHost/assets/109953192/a69bda3c-c72e-43c8-94a6-02f0fe2ef06f)<br>

ข้อควรระวังในการใช้งาน<br>
ต้องมีสิทธิ์ในการเข้าถึงข้อมูลฮาร์ดแวร์ทั้งหมด อาจจะต้องใช้ร่วมกับคำสั่ง sudo<br><br>



# References
## Webpage
<li>https://www.hostpacific.com/command-linux/</li>
<li>https://th.linux-console.net/?p=12402</li>
<li>https://th.linux-console.net/?p=16235</li>
<li>https://th.linux-console.net/?p=7871</li>
<li>https://www.geeksforgeeks.org/lshw-command-in-linux-with-examples/</li>
<li>https://www.cyberciti.biz/faq/linux-display-information-about-installed-hardware/</li>
<li>https://linuxize.com/post/lsmod-command-in-linux/</li>
<li>https://www.seancdavis.com/posts/three-ways-to-add-image-to-github-readme/</li>
<li>https://tecadmin.net/lsusb-command-in-linux/</li>
<li>https://access.redhat.com/documentation/th-th/red_hat_enterprise_linux/6/html/deployment_guide/s2-sysinfo-hardware-lspcmcia</li>
<li>https://www.ibm.com/docs/en/aix/7.1?topic=l-lsdev-command</li>
<li>https://www.thegeekstuff.com/2014/04/lspci-examples/</li>
<li>https://www.geeksforgeeks.org/lsusb-command-in-linux-with-examples/</li>
<li>https://www.geeksforgeeks.org/lsusb-command-in-linux-with-examples/</li>
