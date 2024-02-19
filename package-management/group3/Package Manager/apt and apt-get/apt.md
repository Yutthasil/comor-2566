# APT(Advanced Package Tool)

## อะไร คือ APT package manager
เป็นเครื่องมือสำหรับการจัดการ package ของ Linux ในตระกูล Dabian จึงรวมไปถึง Ubuntu ด้วยเช่นกัน


## คำสั่งต่างๆ


### Install

Install package เดียว
```
apt install ชื่อpackage
```

Install หลาย package ด้วยการเว้นวรรคเเล้วตามด้วยชื่อ package ถัดไป
```
apt install ชื่อpackage เเรก ชื่อpackage สอง
```

การลง packge นั้นใหม่อีกครั้งหลังจากลบทิ้งไป หรือ หากเกิดความเสียหายกับ package ก็สามารถใช้คำสั่งนี้ได้เช่นกัน 
```
reinstall ชื่อ package
```

เเสดง list ของ package ที่เรา install เอาไว้
```
apt list --installed
```





### Uninstall
ลบ package ซึ่งจะไม่ทำการลบการ data files เเละ configuration file
```
apt remove ชื่อpackage
```
ลบหลาย package ด้วยการเว้นวรรคเเล้วตามด้วยชื่อ package ถัดไป
```
apt remove ชื่อpackage1 ชื่อpackage2
```

ลบ package ซึ่งจะทำการลบ data files เเละ configuration file ออกไปด้วย
```
apt purge ชื่อpackage
```

ลบ ส่วนที่เป็น dependency ของ package ที่ถูกไปเเล้วเเต่ยังค้างอยู่ในระบบทั้งหมด
```
apt autoremove
```

ลบเฉพาะ dependency ของ  pacakage ที่ระบุ
```
apt autoremove ชื่อpackage
```



### Upgrade
ก่อนที่จะทำการ upgrade เราควรใช้คำสั่ง update เพื่อดึงข้อมูล version ล่าสุดของ package มาก่อน
```
apt update
```

คำสั่งนี้จะทำการทำให้ package อยู่ในเวอร์ชันล่าสุดของมันเพื่อเพิ่มศักยภาพการทำงานเเละเพิ่มความปลอดภัยของpackage apt สามารถใช้คำสั่งนี้คำสั่งเดียวเพื่อ upgrade package ทั้งหมดที่เราติดตั้งเอาไว้
```
apt upgrade
```

สำหรับ upgrade เฉพาะ package ที่ต้องการ
```
apt upgrade ชื่อpackage
```

คำสั่งเเสดง list ของ package ที่เราสามารถ update ได้
```
apt list --upgradable 
```



### Search
หา package ที่เราต้องการ output จะเป็น list ของ package ที่ตรงกับ input ของเรา ทำให้เราหา package ที่เราต้องการได้ง่ายขึ้น 
```
apt search ชื่อpackage
```


### เเสดงข้อมูลของ package 
```
apt show ชื่อpackage
```
จะได้ output เป็น ข้อมูลของ package ดังนี้  <br>
-Package: ชื่อของ package <br>
-Version: version ของ package <br>
-Installed-Size: จำนวนพื้นที่ที่ package นั้นใช้บน disk โดยไม่ได้รวมถึง dependency ของ package <br>
-Depends: list ของ dependency <br>
-APT-Manual-Installed: ระบุว่า package นั้นถูก install เเบบ manul หรือ install เเบบอัตโนมัติ <br>
-APT-Sources: repository ที่เก็บข้อมูลของ package นั้นๆ <br>
-Description: คำอธิบายของ package

## อะไรคือความเเตกต่างระหว่าง apt เเละ apt-get

1.apt เป็น เวอร์ชันใหม่กว่าของ apt-get  โดย apt-get ถูกปล่อย 1998 ตามมาด้วย apt ที่ถูกปล่อยในปี 2014 <br>
2.คำสั่งของ apt ถูกสร้างขึ้นมาให้มีความใช่ง่ายกว่า apt-get รวมถึง interface ของ apt ที่เป็น high-level UI จึงใช้งานง่ายกว่า apt-get ที่เป็น low-level UI <br>
3.apt สามารถใช้คำสั่ง apt search ชื่อpackage เพื่อค้นหา package ในขณะที่ apt get นั้นไม่สามารถทำได้จึงอาจจะต้องไปพึ่งพา apt-cache เเทน







# reference
1)https://blog.packagecloud.io/what-is-the-apt-package-manager-why-and-how-to-use-it/

2)https://contabo.com/blog/managing-packages-with-the-apt-package-manager/

3)https://www.linode.com/docs/guides/apt-package-manager/

4)https://aws.amazon.com/compare/the-difference-between-apt-and-apt-get/



