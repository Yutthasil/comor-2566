# Host-3
Computer Organization and Operating System Assignment (Chapter: Host, Sec: 3)

## Overview :mag:
Host หมายถึง คอมพิวเตอร์หรือเซิร์ฟเวอร์ที่ทำหน้าที่ในเครือข่าย โดยประกอบด้วยการทำงานร่วมกันของ sub components เหล่านี้เพื่อให้ระบบทำงานได้ตามปกติ sub components ดังกล่าวได้แก่<br />
1. Host Configuration<br />
  - ทำหน้าที่จัดเก็บและจัดการข้อมูลในไฟล์ /etc/hosts เพื่อให้ host สามารถติดต่อและทำงานกับเครื่องอื่นๆได้ตามที่ต้องการ อย่างมีประสิทธิภาพ <br /><br />
   ตัวอย่างคำสั่ง:<br />
   คำสั่งที่ใช้เพื่อดูว่าเนื้อหาภายในไฟล์ /etc/hosts มีกี่บรรทัด
  ```
  $ cat /etc/hosts
  ```
2. I/O Devices<br />
   - อุปกรณ์ I/O เป็นอุปกรณ์ที่รับข้อมูลเข้าระบบผ่าน คีย์บอร์ด, เมาส์ และส่งข้อมูลออกผ่านจอมอนิเตอร์ เป็นหลัก<br /><br />
   ตัวอย่างคำสั่ง:<br />
   คำสั่งเพื่อแสดงรายละเอียดของอุปกรณ๋ PCI ทั้งหมด
  ```
 $ lspci -v
  ```
3. Kernel<br />
  - ส่วนสำคัญที่คอยดูแล บริหารทรัพยากรของระบบ และติดต่อกับฮาร์ดแวร์ และซอฟแวร์ <br /><br />
  ตัวอย่างคำสั่ง:<br />
   `depmod [option]` หรือก็คือคำสั่งสร้างไฟล๋หรืออัปเดตไฟล์ใน kernel
  ```
  $ depmod -a
  ```
4. Memory<br />
 - มีหน้าที่ในการรับผิดชอบการเก็บข้อมูลที่ใช้ในการทำงานของระบบ  <br /><br />
 ตัวอย่างคำสั่ง:<br />
   คำสั่ง free ใช้ในการแสดงข้อมูลการใช้งาน memory
  ```
  $ free
  ```
## Topic :card_index_dividers:
- [Host Configuration](https://github.com/aaomprt/Host-3/tree/main/Host%20Configuration) :paperclip:
- [Input Output Devices](https://github.com/aaomprt/Host-3/tree/main/Input%20Output%20Devices) :keyboard:
- [Kernel](https://github.com/aaomprt/Host-3/tree/main/Kernel) :pushpin:
- [Memory](https://github.com/aaomprt/Host-3/tree/main/Memory) :floppy_disk:

## Members :space_invader:

| ID  | Name | Topic | Image |
| ------------- | --------------------------- | :-------------: | :-----------: |
| 65070008  | นางสาวกมลนิตย์ ธรรมชาติ  | Kernel | <img src="https://scontent.fbkk28-1.fna.fbcdn.net/v/t39.30808-6/426359464_1475576286636292_2307075857368261346_n.jpg?stp=cp6_dst-jpg_p180x540&_nc_cat=105&ccb=1-7&_nc_sid=3635dc&_nc_ohc=ClEWIRrpeMIAX-vlqYc&_nc_ht=scontent.fbkk28-1.fna&oh=00_AfDEFF-K0TOSfIDXQq_E61Bmg8-hWh7BJju6XA2O2pSY3g&oe=65C8C6F1" width="35%"> |
| 65070026  | นางสาวเกวลี ธนโชติชญานี  | Host Overview | <img src="https://scontent.fbkk6-2.fna.fbcdn.net/v/t39.30808-6/425522581_2045555435809006_4730840397820863971_n.jpg?_nc_cat=109&ccb=1-7&_nc_sid=3635dc&_nc_ohc=8HnGVj095z4AX9KSzIV&_nc_ht=scontent.fbkk6-2.fna&oh=00_AfC3x933jMF7GTGdYRSLjkr6oW8jE-caK6ffW6R-ZTUBQQ&oe=65C98D5E" width="35%"> |
| 65070113  | นายนพกร บุญมี  | Memory | <img src="https://github.com/aaomprt/Host-3/assets/117189340/891729e4-b890-4c68-8ae3-bc88cbd90e5d" width="35%"> |
| 65070131  | นางสาวปราณปรีญา เม่งมั่งมี  | Kernel | <img src="https://scontent.fbkk3-4.fna.fbcdn.net/v/t39.30808-1/357108356_6260830513993404_6867662345275536233_n.jpg?stp=dst-jpg_p320x320&_nc_cat=108&ccb=1-7&_nc_sid=5740b7&_nc_eui2=AeE80EGz3AZxG-4hQSqa8CPv13EjVCntvmjXcSNUKe2-aJtoXaAb9LTWeWh3jWBvlbhOJYQAyFBcKMZfPDlEP3m8&_nc_ohc=YabJ-qpm2wYAX8SQZGG&_nc_ht=scontent.fbkk3-4.fna&oh=00_AfDiuW7gOZ0MjkbfcwWLZ3aoRssuPImaqVbGtDO4L_1otw&oe=65CA83B7" width="35%"> |
| 65070132  | นางสาวปลายฟ้า พุ่มเจริญ  | Host Configuration | <img src="https://cdn.discordapp.com/attachments/915993422660259881/1202653940727152741/IMG_3290.jpg?ex=65ce3dc3&is=65bbc8c3&hm=9c4ac38e162bee4d0f3cbeeca94a675d112c047b0d5381369901d86ebfa6122d" width="35%"> |
| 65070137  | นางสาวปานฤทัย ผิวสุข  | Host Configuration | <img src="https://scontent.fbkk22-4.fna.fbcdn.net/v/t39.30808-6/426748090_2045454635819086_4290629315869297157_n.jpg?_nc_cat=109&ccb=1-7&_nc_sid=dd5e9f&_nc_ohc=W7nj3MNRNMoAX9jqJ1A&_nc_ht=scontent.fbkk22-4.fna&oh=00_AfBVLSViEwyaxXeiqrINlAkeIqT2z1ABPY8Zh_LElID1nQ&oe=65CA476D" width="35%"> |
| 65070145  | นางสาวพรรณราย สุคง  | Input and Output Devices | <img src="https://cdn.discordapp.com/attachments/1147610510951452702/1205128300499042304/IMG_5969.jpg?ex=65d73e31&is=65c4c931&hm=482eca9b1bb4288d457e90af282b39a7ef370ec31e4f8f2a96226811567dd9d4&" width="35%"> |

## [Reference](https://github.com/aaomprt/Host-3/blob/main/references.md) :unlock:



