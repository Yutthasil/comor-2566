# Repository Set up & Package Management
- [Repository Set up \& Package Management](#repository-set-up--package-management)
  - [Package Management](#package-management)
    - [overview \& Concept](#overview--concept)
    - [Benefit](#benefit)
  - [Debian](Debian(65070064)/README.md#debian)
  - [Redhat Package Manager](RedhatPackageManager(65070005)/RPM.md#red-hat-package-manager-rpm)
  - [APT](APT(65070007,65070040)/README.md#advanced-packaging-tool-apt)
  - [YUM](YUM(65070034,65070047)/README.md#yellowdog-updater-modified-yum)
  - [Constrbutors](#constrbutors)

# Package Management
- [**Overview**](#overview)
- [**Core concept for package management**](#core-concept-for-package-management)
    - [**Packages**](#packages)
    - [**Repositories**](#repositories)
    - [**Dependencies**](#dependencies-1)
    - [**Package managers**](#package-managers)
- [**references**](#references)

## Overview
package management คือกระบวนการของการติดตั้ง, การอัพเด็ท, การกําหนดค่าคอนฟิก, เเละการลบออก ของเเพคเก็จซอฟเเวร์บนระบบคอมพิวเตอร์ โดยส่วนใหญ่นั้น เเพคเก็จซอฟเเวร์จะประกอบไปด้วยโค้ดที่ถูกคอมไพล์เเล้ว,ไลบรารี่,ไฟล์คอนฟิก หรือเมต้าดาต้าต่างๆที่จําเป็นต่อการติดตั้งหรือจําเป็นต่อการทํางานบางส่วนของซอฟเเวร์ ระบบ package management จะเป็นส่วนสําคัญในการช่วยให้ผู้ใช้เเละ admin สามารถจัดการกับเเพคเก็จเหล่านี้ได้อย่างมีประสิทธิภาพ

โดยมีหน้าที่สําคัญต่างๆของระบบได้เเก่ :

### Installation:
package manager จัดการด้านการติดตั้งโดยการเช็ค components ต่างๆที่จําเป็นในการติดตั้งนั้นมีครบถ้วนเเละพร้อมใช้งาน
### Updates:
package manager เพิ่มประสิทธิภาพในการติดตั้งซอฟเเวร์ที่ up-to-date ซึ่งจะทําให้ได้ซอฟเเวร์ที่มีความเป็นปัจจุบัน
### Dependencies: 
ซอฟเเวร์จําเป็นที่จะต้องใช้ไลบรารี่หรือส่วนประกอบอื่นๆเพื่อทํางาน ตัว package manager จะคอยจัดการในส่วนนี้ให้
### Configuration: 
package manager จะคอย provide เครื่องมือเพื่อช่วยติดตั้งซอฟเเวร์ในลักษณะที่ผู้ใช้ต้องการ ทําให้สามารถปรับเเต่งวิธีการติดตั้งได้
### Removal:
เมื่อผู้ใช้ต้องการลบซอฟเเวร์ตัวใดตัวหนึ่ง package manager สามารถช่วยให้ผู้ใช้ลบหรือกําจัดซอฟเเวร์ตัวนั้นอย่างหมดจด โดยการลบไฟล์ที่มีความเกี่ยวข้องกับตัวซอฟเเวร์ทั้งหมด
### Security:
package manager นั้นมีการเเถม security features ต่างๆมาให้เช่น digital signature เพื่อปกป้อง integrity ของตัวเเพคเก็จเองจากการเเก้ไขของบุคคลภายนอกที่ไม่มีสิทธิ

## Core concept for package management

### Packages
ซอฟเเวร์ส่วนใหญ่ของระบบ Linux หรือ Unix นั้นจะถูกเเบ่งระจายออกเป็น "เเพคเก็จ" โดยถูก archive ไว้เเละเก็บไฟล์ pre-compiled binary, script ขั้นตอนการติดตั้ง, ไฟฟล์ปรับเเต่ง config, dependencies requirements เเละรายละเอียดอื่นๆเกี่ยวกับซอฟเเวร์ เเพคเก็จเหล่านี้จะถูกกระจายเเละ format ในลักษณะที่เเตกต่างกันออกไปตาม package format ต่างๆเช่น .deb สําหรับ debian/ubuntu เเละ .rpm สําหรับ CentOS/RHEL ดดยส่วนใหญ่เเล้วจะเป็นเรื่องที่ง่ายสําหรับ user ในการติดตั้งไฟล์ package เหล่านี้เเต่จะมีข้อควรระวังบางส่วนเช่น เเพคเก็จที่ได้มานั้นมีความถูกต้อง มีการเเก้ไขบัคต่างเเละระบบ security ที่เป็นปัจจุบันหรือไม่เเละตรงกับ dependencies ที่ software จะใช้หรือเปล่า

### Repositories
การที่ user จะได้ไฟล์นั้นมีมากมายหลายวิธี เเต่ส่วนใหญ่นั้น user จะได้ไฟล์ผ่าน software repositories (หรือบางทีถูกเรียกย่อๆว่า repos) เพื่อให้ได้เเพคเก็จที่ต้องการ. repositories นั้นเปรียบเสมือนกับสถานที่เก็บเเพคเก็จต่างๆซึ่งส่วนใหญจะสามารถเข้าถึงได้ผ่านอินเทอเน็ตโดย repos สามารถเก็บไล่ได้ตั้งเเต่เเพคเก็จเดียวไปจนถึงพันกว่าเเพคเก็จเลยก็มี

### Dependencies
ทุกๆครั้งที่ซอฟเเวร์จะทํางานบนระบบปฎิบัติการณ์ต่างๆนั้น เป็นเรื่องปกติที่ซอฟเเวร์จําเป็นที่จะต้องพึ่งพาซอฟเเวร์อื่นๆในการทํางานโดยบน linux นั้นจะมีเเพคเก็จที่เก็บเมต้าดาต้าที่มีระบุเเพคเก็จเพิ่มเติมที่จําเป็นในการทํางานอยู่ เเพคเก็จเหล่านี้นั้นเรียกว่า dependencies เเพคเก็จที่มีเมต้าดาต้าเหล่านี้สามารถมีได้ถึงร้อยกว่า dependencies โดยเมื่อทัาการติดตั้ง, อัพเกรด หรือลบ package, dependencies เหล่านี้เองก็ต้องถูกติดตั้ง, อัพเกรด หรือลบออกตามจําเป็นเช่นเดียวกัน

### Package Managers
package manager เป็นตัวช่วยลดความซับซ้อนสําหรับ end-user โดยการทําให้ขั้นตอนของการติดตั้ง, อัพเกรดหรือลบเเพคเก็จเเละ dependencies ต่างๆ เป็นไปอย่างอัตโนมัติเเละง่ายซึ่งช่วยเพิ่ม user-experience เเละความสามารถในการจัดการซอฟเเวร์บน linux ได้อย่างเป้นระบบเเละมีประสิทธิภาพ ซึ่งมีความหลากหลายตามระบบที่ใช้ต่างกัน

## references
Core concept for package management
https://www.linode.com/docs/guides/linux-package-management-overview/#package-managers


### Constrbutors

| Student ID | Name        | Topic worked               | Image           |
|------------|-------------|----------------------------|-----------------|
| 65070005   | Kanokpol poykham | Redhat                     |                 |
| 65070007   | Kanonrat Berkkhunthod | apt management             |                 |
| 65070019   | Kittipon Siriamornkit | overview, concept, benefit |                 |
| 65070034   | Chirakit Marachchalee | yum pacakge management     |                 |
| 65070040   | Junbeom kim | apt package management     |                 |
| 65070047   | Chaipiphat Pongprapachuen | yum package management     |                 |
| 65070064   | Napat Wetchapun | Debian                     |                 |
