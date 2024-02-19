# Repository Setup using yum (CentOS/RedHat) #
 ถ้าหากต้องการใช้ yum ในการ Install external softwares หรือ Update ให้เป็น Software version ล่าสุด, ต้องใช้ Repository ที่อยู่บน Internet
โดยค่า Default จากการติดตั้ง CentOS จะมีการ Config repository ไปที่ mirrorlist.centos.org เป็น website ที่แสดงรายชื่อ website repository ที่  เปิดให้ download file rmp อีกที

 ซึ่งจากการตั้งค่า Default ทำให้เราต้องไปดาวน์โหลดไฟล์จาก Website ที่อยู่ต่างประเทศ ซึ่งจะช้า ดังนั้นวิธีแก้ก็คือ เปลี่ยน config ของ Repository ให้ชี้มายัง Website ในประเทศไทย

ตัวอย่าง config file CentOS-Base.repo ซึ่งเก็บ Config Repository ชื่อ  base, extras และ updates
```
[root@cent62-yum ~]# cat /etc/yum.repos.d/CentOS-Base.repo
# CentOS-Base.repo
#
# The mirror system uses the connecting IP address of the client and the
# update status of each mirror to pick mirrors that are updated to and
# geographically close to the client.  You should use this for CentOS updates
# unless you are manually picking other mirrors.
#
# If the mirrorlist= does not work for you, as a fall back you can try the
# remarked out baseurl= line instead.
#
#

[base]
name=CentOS-$releasever - Base
mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=os
#baseurl=http://mirror.centos.org/centos/$releasever/os/$basearch/
...
```

 โดยใน Config Repository “base” จะเป็นตัวที่ดึงข้อมูล และชื่อ Website ที่ Config ไว้ใน option “mirrorlist” ซึ่งเวลาจะใช้งานต้องแทนค่าตัวแปร
 ซึ่งเราจะใช้คำสั่ง yum-config-manager ตามด้วยชื่อ Repository เพื่อแสดง Config “base” ทำให้ผลลัพธ์ แทนที่ค่าตัวแปรที่ ($) ที่เขียนไว้ใน Config file เรียบร้อยแล้ว
```
[root@cent62-yum ~]# yum-config-manager base
Loaded plugins: fastestmirror
========================= repo: base =========================
[base]
bandwidth = 0
base_persistdir = /var/lib/yum/repos/x86_64/6
baseurl =
...
mirrorlist = http://mirrorlist.centos.org/?release=6&arch=x86_64&repo=os
mirrorlist_expire = 86400
name = CentOS-6 - Base
...
```

ใช้คำสั่ง curl ในการดึงข้อมูลจาก Website ที่ระบุไว้ใน “mirrorlist” มาเพื่อแสดงรายชื่อ Website ที่สามารถนำมาใช้เป็น Repository ได้
```
[root@cent62-yum ~]# curl 'http://mirrorlist.centos.org/?release=6&arch=x86_64&repo=os'

http://mirrors.psu.ac.th/pub/centos/6.2/os/x86_64/

http://mirror.issp.co.th/centos/6.2/os/x86_64/

http://mirror1.ku.ac.th/centos/6.2/os/x86_64/

http://mirror.yourconnect.com/centos/6.2/os/x86_64/

http://mirrors.btte.net/centos/6.2/os/x86_64/

...
```

ผลลัพธ์ที่ได้จะเปลี่ยนไปเรื่อยๆ 

การ run คำสั่ง yum repolist เพื่อใช้ดูข้อมูล Repository ที่จะใช้ ในการ run ครั้งแรก ระบบจะไปดึงข้อมูลของ Repository ใหม่จากบน Internet แต่ในครั้งต่อๆไป ระบบจะไปดึงข้อมูลจาก Cache แทน
```
[root@cent62-yum ~]# yum repolist
Loaded plugins: fastestmirror, security
Determining fastest mirrors
 * base: mirrors.btte.net
 * extras: mirrors.btte.net
 * updates: mirrors.btte.net
base                                                     | 3.7 kB     00:00
base/primary_db                                          | 4.5 MB     00:23
extras                                                   | 3.5 kB     00:00
extras/primary_db                                        | 6.3 kB     00:00
updates                                                  | 3.5 kB     00:00
updates/primary_db                                       | 3.0 MB     00:10
repo id                        repo name                                  status
base                           CentOS-6 - Base                            6,294
extras                         CentOS-6 - Extras                              4
updates                        CentOS-6 - Updates                           832
repolist: 7,130
```

ซึ่งการใช้ Defualt Config  ทำให้ไม่สามารถควบคุมได้ว่าจะใช้ Repository จาก Website ไหน, จากตัวอย่าง จะเป็นการไปใช้ Repository จากประเทศจีน

## การเปลี่ยนมาใช้ Repository ภายในประเทศไทย ##
 เพราะว่า Default Config จะเป็นการไปใช้ Repository จากต่างประเทศ ทำให้มีความเร็วต่ำ จึงแนะนำให้ใช้ Repository ที่อยู่ในประเทศไทย เพื่อความเร็วในการ Download โดยดูจากชื่อ Domain ของ Website ต่างๆ ที่ลงท้ายด้วย .th และจากผลของคำสั่ง curl จะมี
  - http://mirrors.psu.ac.th/pub/centos/6.2/os/x86_64/
  - http://mirror.issp.co.th/centos/6.2/os/x86_64/
  - http://mirror1.ku.ac.th/centos/6.2/os/x86_64/

 ตัวอย่าง การเปลี่ยน Repository มาที่ประเทศไทยของ ม.เกษตร สำหรับ centos 5
 ```
# cd /etc/yum.repos.d/
# rm -f *
# wget http://mirror1.ku.ac.th/yum-centos/5/CentOS-Base.repo
# yum -y update
```

### การเปลี่ยนคอนฟิก repos ให้มาใช้เว็บไซต์ที่ต้องการ ###
ทำได้โดยแก้ไขไฟล์ Repository, ปิด Config mirrorlist แล้วไปตั้งค่า Website ใน Config baseurl

เช่น หากต้องการเปลี่ยน Repository ชื่อ base, extras, updates ให้ชี้ไปที่ mirrors.psu.ac.th สามารถทำได้ โดยแก้ไขไฟล์ CentOS-Base.repo

สังเกตจากการแก้ไข config baseurl ในแต่ละ Repository  จะไม่เหมือนกัน และจะใช้ชื่อตัวแปร ($) ในการระบุชื่อเวอร์ชั่น ไม่ควรระบุเป็น 6.2 เนื่องจาก หากมีเวอร์ชั่นใหม่ออกมา ไฟล์ Config Repository นี้ จะไม่สามารถใช้งานได้อีก
```
[root@cent62-yum ~]# cat /etc/yum.repos.d/CentOS-Base.repo
...
[base]
name=CentOS-$releasever - Base
#mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=os
baseurl=http://mirrors.psu.ac.th/pub/centos/$releasever/os/$basearch/
gpgcheck=1
gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-6
enabled = 1 

#released updates
[updates]
name=CentOS-$releasever - Updates
#mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=updates
baseurl=http://mirrors.psu.ac.th/pub/centos/$releasever/updates/$basearch/
gpgcheck=1
gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-6
enabled = 1 

#additional packages that may be useful
[extras] name=CentOS-$releasever - Extras
#mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=extras
baseurl=http://mirrors.psu.ac.th/pub/centos/$releasever/extras/$basearch/
gpgcheck=1
gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-6
enabled = 1
```

ใช้คำสั่ง yum repolist -v ในการดูข้อมูลเพิ่มเติมของแต่ละ Repository
```
[root@cent62-yum ~]# yum -v repolist
Loading "fastestmirror" plugin
Loading "security" plugin
Config time: 0.044
Yum Version: 3.2.29
Loading mirror speeds from cached hostfile
Setting up Package Sacks
pkgsack time: 0.073
Repo-id      : base
Repo-name    : CentOS-6 - Base
Repo-revision: 1324003045
Repo-updated : Fri Dec 16 09:38:07 2011
Repo-pkgs    : 6,294
Repo-size    : 5.1 G
Repo-baseurl : http://mirrors.psu.ac.th/pub/centos/6/os/x86_64/
Repo-expire  : 21,600 second(s) (last: Mon May  7 13:16:01 2012)

Repo-id      : extras
Repo-name    : CentOS-6 - Extras
Repo-revision: 1327502687
Repo-updated : Wed Jan 25 21:44:47 2012
Repo-pkgs    : 4
Repo-size    : 3.0 M
Repo-baseurl : http://mirrors.psu.ac.th/pub/centos/6/extras/x86_64/
Repo-expire  : 21,600 second(s) (last: Mon May  7 13:16:02 2012)

Repo-id      : updates
Repo-name    : CentOS-6 - Updates
Repo-revision: 1336165833
Repo-updated : Sat May  5 04:31:48 2012
Repo-pkgs    : 832
Repo-size    : 1.7 G
Repo-baseurl : http://mirrors.psu.ac.th/pub/centos/6/updates/x86_64/
Repo-expire  : 21,600 second(s) (last: Mon May  7 13:16:02 2012)

repolist: 7,130
```

ซึ่งหลังจากเปลี่ยนแล้ว,  yum ก็จะไปดาวน์โหลดไฟล์จาก Repository จาก Website ที่ระบุใน baseurl แทน

## References ##
- https://secure.jvh.co.th/index.php/knowledgebase/26/Linux-Server-CentOS--%E0%B9%80%E0%B8%9B%E0%B8%A5%E0%B8%A2%E0%B8%99%E0%B8%84%E0%B8%AD%E0%B8%99%E0%B8%9F%E0%B8%81-yum-%E0%B9%83%E0%B8%AB%E0%B8%A1%E0%B8%B2%E0%B9%83%E0%B8%8A-repos-%E0%B9%83%E0%B8%99%E0%B9%84%E0%B8%97%E0%B8%A2.html
- https://hosxp.net/smf2/index.php?topic=14555.0
- http://wiki.openvz.org/Yum_-_installing
- http://www.electrictoolbox.com/install-yum-with-rpm-on-centos/
