# Zypper

## Zypper คือ

Zypper เป็น default package manager ที่ใช้ในการดูแลระบบ OpenSUSE และ SUSE Linux Enterprise เป็นอินเทอร์เฟซบรรทัดคำสั่งของตัวจัดการแพ็คเกจ ZYpp (เครื่องมือจัดการแพ็กเกจของ Zypper) จึงไม่จำเป็นต้องทำการติดตั้ง zypper ในระบบปฎิบัติการ linux ของ SUSE _การจะใช้งาน zypper นั้นคือการเปลี่ยนแปลงทั้งระบบจึงจำเป็นจะต้องมีสิทธิการเข้าถึงการดำเนินการบนระบบ หรือมีสิทธิผู้ใช้ root จึงจะสามารถใช้งานในระบบได้_

## ระบบ OpenSUSE และ SUSE Linux Enterprise คืออะไร

1. openSUSE เป็นระบบปฎิบัติการ Linux แบบ open source พัฒนาและจัดจำหน่ายโดยบริษัท SUSE GmbH ซึ่งเป็นบริษัทซอฟต์แวร์และบริการที่มีความเชี่ยวชาญในด้านระบบปฏิบัติการและบริการคลาวด์
2. SUSE Linux Enterprise เป็น Linux Distribution เช่นเดียวกันกับ openSUSE แต่ถูกสร้างมาในเชิงพาณิชย์ที่ออกแบบมาเป็นพิเศษสำหรับองค์กรและการใช้งานจริง ซึ่งจะมีการสนับสนุนและรับประกันคุณภาพและความปลอดภัย รวงถึงมีฟีเจอร์และการสนับสนุนทางธุรกิจ พร้อมกับบริการที่ให้คำปรึกษาและการสนับสนุนทางเทคนิค

## การเรียกใช้ Zypper

- การเรียกใช้ zypper นั้นต้องใช้คำสั่งขึ้นต้นด้วย

```
zypper
```

- หรือหากต้องการทราบคำสั่ง

```
zypper help
```

- Package file format: `.rpm`

## คำสั่งพื้นฐานของ Zypper

1. การจัดการแพ็คเกจ

- ค้นหาแพ็คเกจ:

```
zypper search <package_name>
```

- ติดตั้งแพ็คเกจ:

```
zypper install <package_name>
```

- ลบแพ็คเกจ:

```
zypper rm <package_name>
```

- แสดงข้อมูลเกี่ยวกับแพ็คเกจที่ระบุ:

```
zypper info <package_name>
```

- อัปเดตรายการแพ็คเกจทั้งหมด:

```
zypper update
```

- อัปเดตเฉพาะแพ็คเกจ:

```
zypper update <package_name>
```

- แสดงรายการแพ็คเกจที่ติดตั้ง:

```
zypper list-installed
```

- แสดงรายการแพ็คเกจที่อัพเดต:

```
zypper list-updates
```

2. การจัดการที่เก็บข้อมูล (repositories)

- แสดงรายการที่เก็บข้อมูล:

```
zypper repos
```

- เพิ่มเก็บข้อมูล:

```
zypper addrepo <repository_URL> <alias>
```

- ลบที่เก็บข้อมูล:

```
zypper removerepo <alias>
```

- จัดการรูปแบบที่เก็บข้อมูล:

```
zypper modify <alias>
```

- รีเฟรชรายการจากที่เก็บข้อมูล:

```
zypper refresh
```

- ดูการเปลี่ยนแปลง:

```
zypper lu
```

3. เปิด session zypper shell เพื่อรันคำสั่ง
   _ใน session zypper shell ใช้คำสั่งเหมือนใน shell ปกติ ไม่เหมือนใน zypper terminal_

```
zypper shell
```

4. แสดงรายการแพทช์ของระบบปฏิบัติการ
   _ ความสามารถในการติดตั้งแพตช์ความปลอดภัยของระบบปฏิบัติการเท่านั้น _

```
zypper lp
```

ตัวอย่าง output :

`Repository: openSUSE-15.3-Updates`
`======================= Patch summary =======================`
`Repository      | Updates  | Security | Recommended | Optional | Applied`
`----------------+----------+----------+-------------+----------+---------`
`openSUSE-15.3-Updates |     2    |     1    |     1       |     0    |     2   `

5. การจัดการเกี่ยวกับ cache รวมถึง metadata cache

- ล้างแคชทั้งหมด:

```
zypper clean
```

- ล้างแค่เฉพาะ metadata cache:

```
zypper clean-metadata
```

- ล้างแคชของแพ็คเกจเท่านั้น:

```
zypper clean-packages
```

# Reference about zypper

1. https://th.linux-console.net/?p=2474

2. https://www.linuxadictos.com/th/aprende-zypper-con-estos-sencillos-comandos.html

3. https://www.linode.com/docs/guides/linux-package-management-overview/
