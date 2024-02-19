# Interface device

![Alt text](https://cdn.pixabay.com/photo/2016/05/25/18/18/penguin-1415562_1280.png)
source: [linux image](https://pixabay.com/th/vectors/%E0%B9%80%E0%B8%9E%E0%B8%99%E0%B8%81%E0%B8%A7%E0%B8%99-tux-%E0%B8%AA%E0%B8%95%E0%B8%A7-%E0%B8%99%E0%B8%81-%E0%B8%99%E0%B8%B2%E0%B8%A3%E0%B8%81-1415562/)

## บทบาทหน้าที่

interface device มีบทบาทและหน้าที่สำคัญในการเชื่อมต่อระหว่างซอฟต์แวร์และฮาร์ดแวร์

#### ต่อไปนี้คือบางหน้าที่หลักของ interface device ใน Linux
1. การเชื่อมต่อระบบปฏิบัติการกับอุปกรณ์ฮาร์ดแวร์: Interface device เป็นตัวกลางที่ช่วยให้ระบบปฏิบัติการ Linux สามารถติดต่อและทำงานกับอุปกรณ์ฮาร์ดแวร์ต่าง ๆ ได้ เช่น การเชื่อมต่อกับ NIC, การใช้งาน USB devices หรือการจัดการกับอุปกรณ์เกี่ยวกับเสียงและวีดีโอ

2. การจัดการไดรเวอร์ (Driver Management): Interface device ใน Linux มักต้องใช้ไดรเวอร์เพื่อให้ OS สามารถทำงานกับฮาร์ดแวร์ได้อย่างถูกต้อง การจัดการไดรเวอร์นี้เป็นหน้าที่สำคัญของ interface device เพื่อให้ระบบสามารถรู้จักและปรับให้กับอุปกรณ์ต่าง ๆ ที่เชื่อมต่อ

3. การจัดการการสื่อสาร (Communication Management): Interface device มีหน้าที่ในการจัดการการสื่อสารระหว่างซอฟต์แวร์และฮาร์ดแวร์ นอกจากนี้ยังรวมถึงการจัดการข้อมูลที่ได้รับและส่งออกจากระบบ

4. การทำงานร่วมกับ Kernel: Interface device ทำงานร่วมกับ Linux Kernel เพื่อให้ระบบปฏิบัติการสามารถเข้าถึงและควบคุมฮาร์ดแวร์ได้อย่างเหมาะสม

5. การรับรู้เหตุการณ์ (Event Handling): Interface device สามารถรับรู้เหตุการณ์ที่เกิดขึ้นในระบบ เช่น การกดปุ่ม, การตรวจจับอุปกรณ์ที่เสียหาย หรือเหตุการณ์อื่น ๆ ที่สำคัญ

6. การจัดการพลังงาน (Power Management): บาง interface device มีบทบาทในการจัดการพลังงานของอุปกรณ์ฮาร์ดแวร์ เพื่อประหยัดพลังงานหรือการจัดการในรูปแบบอื่น ๆ

## พื้นฐานและหลักการทำงาน

พื้นฐานหรือหลักการทำงานของ interface device ใน Linux มีลักษณะดังนี้:

**Device Files:**
* Interface device มักถูกแทนด้วย device file ในระบบไฟล์ของ Linux ซึ่งประกอบด้วย `/dev` และมักจะมีชื่อเฉพาะสำหรับแต่ละอุปกรณ์ เช่น `/dev/sda` สำหรับ hard drive หรือ `/dev/ttyUSB0` สำหรับ USB serial device

**Kernel Modules:**
- บาง interface device ต้องใช้ kernel module เพื่อทำงานในระบบ โมดูลเหล่านี้จะถูกโหลดหรือถูกสร้างขึ้นเมื่อ interface device ถูกเชื่อมต่อกับระบบ

**Kernel Space vs. User Space:**
* การทำงานของ interface device มักเกิดใน kernel space และ user space ของระบบปฏิบัติการ Linux โดย kernel space มีการทำงานที่ใกล้เคียงกับฮาร์ดแวร์ และ user space มีการทำงานที่เกี่ยวข้องกับแอปพลิเคชันและการให้บริการสู่ผู้ใช้

**Interrupts:**
- Interface device สามารถใช้ interrupts เพื่อแจ้งเหตุการณ์หรือสถานะของอุปกรณ์กับระบบ ซึ่งทำให้ kernel สามารถตอบสนองได้อย่างรวดเร็ว

**File Operations:**
- แต่ละ interface device มี file operations เฉพาะที่ kernel สามารถเรียกใช้เพื่อทำงานกับอุปกรณ์นั้น ๆ เช่น read, write, open, close, ioctl (input output control) 

**Device Drivers:**
- Interface device มักจะต้องมี device driver ที่เป็นโปรแกรมที่ทำหน้าที่ควบคุมการทำงานของอุปกรณ์นั้น ๆ บนระบบปฏิบัติการ Linux

**Sysfs and Procfs:**
- Linux มี sysfs และ procfs ที่ให้ข้อมูลเกี่ยวกับอุปกรณ์และการทำงานของระบบ ผู้ใช้หรือแอปพลิเคชันสามารถอ่านหรือแก้ไขค่าต่าง ๆ ที่เกี่ยวข้องกับ interface device ผ่าน sysfs หรือ procfs

**File Descriptors:**
- Interface device มักถูกเปิดและใช้งานผ่าน file descriptors ซึ่งเป็นเลขที่กำหนดให้กับไฟล์ที่เปิดใช้งานการทำงานของ interface device ใน Linux มีความซับซ้อนและการทำงานที่ทันสมัย เนื่องจากระบบปฏิบัติการ Linux ได้รับการพัฒนาอย่างต่อเนื่องและรองรับหลายประเภทของอุปกรณ์และการเชื่อมต่อต่าง ๆ ในโลกของฮาร์ดแวร์

## เริ่มกันที่ Lspci Command
นี่คือตัวอย่างทั่วไป
```
lspci

```
ในตัวอย่างเราใช้ lspci ปราศจาก ```options``` หรือ ```flag``` คำสั่งนีจะแสดง list ของอุปกรณ์ PCI ทั้งหมด

### การใช้งานขั้นสูงของ Lspci

|**Argument**	 | **Description** | 
| :-------- | :------- | 
| **-v** | แสดงผลลัพธ์อย่างละเอียด (verbose) โดยแสดงข้อมูลเพิ่มเติมเกี่ยวกับแต่ละอุปกรณ์ เช่น ```lspci -nn``` |
|**-nn**|แสดงทั้ง vendor และ device code เช่น `lspci -nn`|
|**-k**|แสดง kernel drivers ที่รับผิดชอบการจัดการกับแต่ละอุปกรณ์ เช่น `lspci -k`|
|**-t**|แสดงอุปกรณ์ในรูปแบบของไดอะแกรมต้นไม เช่น `lspci -t`|
|**-i**|ใช้ไฟล์ PCI ID ที่ระบุแทนที่จะใช้ค่าเริ่มต้น เช่น `lspci -i` หรือ `/path/to/pci.ids`|
|**-d**|แสดงเฉพาะอุปกรณ์ที่มี vendor และ device ID ที่ระบุ เช่น `lspci -d 8086:100e`|
|**-s**|แสดงเฉพาะอุปกรณ์ในบัสที่ระบุเช่น `lspci -s 00:02.0`|
|**-x**|แสดงบางส่วนแรกของพื้นที่การกำหนดค่า เช่น `lspci -x`|
|**-xxx**|แสดงพื้นที่การกำหนดค่าทั้งหมด (***เฉพาะ root เท่านั้น) เช่น `lspci -xxx`|
|**-A**|ใช้วิธีการเข้าถึงที่ระบุเพื่ออ่านพื้นที่การกำหนดค่าฮาร์ดแวร์ของ PCI เช่น `lspci -A intel-conf1`|
|**-D**|แสดงหมายเลขโดเมนเสมอ เช่น `lspci -D`|
|**-F**|อ่านค่าการกำหนดค่าจากไฟล์ที่ระบุ เช่น `lspci -F dump.txt`|

### การแสดงผลลัพธ์อย่างละเอียด
**command**
```
lspci -v
```
**output**
```
00:01.0 VGA compatible controller: NVIDIA Corporation GP106 [GeForce GTX 1060 6GB] (rev a1) (prog-if 00 [VGA controller])
	Subsystem: Gigabyte Technology Co., Ltd GP106 [GeForce GTX 1060 6GB]
	Flags: bus master, fast devsel, latency 0, IRQ 33
	Memory at f6000000 (32-bit, non-prefetchable) [size=16M]
	Memory at e0000000 (64-bit, prefetchable) [size=256M]
	Memory at f0000000 (64-bit, prefetchable) [size=32M]
	I/O ports at e000 [size=128]
	[virtual] Expansion ROM at f7000000 [disabled] [size=512K]
	Capabilities: <access denied>
	Kernel driver in use: nvidia
	Kernel modules: nvidiafb, nouveau, nvidia_drm, nvidia
```
การใช้คำสั่ง ```lspci -v``` ใน Linux จะแสดงข้อมูลเกี่ยวกับอุปกรณ์ที่เชื่อมต่อผ่าน PCI bus โดยรายละเอียด ซึ่งประกอบด้วยข้อมูลเช่น vendor ID, device ID, ที่อยู่ของหน่วยความจำ, ข้อมูล I/O ports, และ driver ที่กำลังใช้งาน


## ทางเลือกอื่นนอกจาก lspci Command
นอกจากคำสั่ง ```lspci```แล้วยังมีเครื่องมือและคำสั่งทดแทนอื่นที่สามารถช่วยจัดการและแสดงรายการอุปกรณ์ PCI ใน Linux ได้
###  lsusb Command
**command**
```
lsusb
```
**output**
```
Bus 002 Device 002: ID 045e:0773 Microsoft Corp.
Bus 002 Device 001: ID 1d6b:0003 Linux Foundation
Bus 001 Device 003: ID 04f2:b685 Chicony Electronics Co., Ltd
Bus 001 Device 001: ID 1d6b:0002 Linux Foundation
```
คำสั่ง ```lsusb``` ใน Linux ถูกใช้เพื่อแสดงรายการของอุปกรณ์ USB ที่เชื่อมต่อกับระบบการใช้คำสั่งนี้จะช่วยในการตรวจสอบว่าอุปกรณ์ USB ต่าง ๆ ถูกตรวจพบและเชื่อมต่อกับระบบอย่างไร รายการที่แสดงอาจรวมถึงข้อมูลเชิงละเอียดเกี่ยวกับผู้ผลิต, รหัสผลิตภัณฑ์, และรายละเอียดเพิ่มเติมของอุปกรณ์ USB

### lshw Command
**command**
```
lshw
```
**output**
```
  *-cpu                     
       description: CPU
       product: Intel Core i7-7700K
       vendor: Intel Corp.
       physical id: 1
       bus info: cpu@0
       version: Intel(R) Core(TM) i7-7700K CPU @ 4.20GHz
       serial: To Be Filled By O.E.M.
       slot: SOCKET 0
       size: 4200MHz
       capacity: 4200MHz
       width: 64 bits
       clock: 100MHz
       capabilities: x86-64 fpu fpu_exception wp vme de pse tsc msr pae mce cx8 apic sep mtrr pge mca cmov pat pse36 clflush dts acpi mmx fxsr sse sse2 ss ht tm pbe syscall nx pdpe1gb rdtscp constant_tsc art arch_perfmon pebs bts rep_good nopl xtopology nonstop_tsc cpuid aperfmperf tsc_known_freq pni pclmulqdq dtes64 monitor ds_cpl vmx est tm2 ssse3 sdbg fma cx16 xtpr pdcm pcid sse4_1 sse4_2 x2apic movbe popcnt tsc_deadline_timer aes xsave avx f16c rdrand lahf_lm abm 3dnowprefetch cpuid_fault epb invpcid_single pti ssbd ibrs ibpb stibp tpr_shadow vnmi flexpriority ept vpid fsgsbase tsc_adjust bmi1 hle avx2 smep bmi2 erms invpcid rtm mpx rdseed adx smap clflushopt intel_pt xsaveopt xsavec xgetbv1 xsaves dtherm ida arat pln pts hwp hwp_notify hwp_act_window hwp_epp
       configuration: cores=4 enabledcores=4 threads=8
  *-memory
       description: System Memory
       physical id: 2
       slot: System board or motherboard
       size: 16GiB
     *-bank:0
          description: DIMM DDR4 Synchronous 2400 MHz (0.4 ns)
          product: CMK16GX4M1A2400C14
          vendor: Unknown
          physical id: 0
          serial: 00000000
          slot: ChannelA-DIMM0
          size: 16GiB
          width: 64 bits
          clock: 2400MHz (0.4ns)
     *-bank:1
          description: [empty]
          product: [empty]
          vendor: [empty]
          physical id: 1
          serial: [empty]
          slot: ChannelB-DIMM0
  ...

```
lshw คือคำสั่งที่ใช้สำหรับแสดงข้อมูลเกี่ยวกับ hardware คำสั่งนี้ช่วยให้ผู้ใช้งานสามารถดูข้อมูลเกี่ยวกับ CPU, RAM , การ์ดกราฟิก, การ์ดเสียง, ฮาร์ดไดรฟ์ และอุปกรณ์ฮาร์ดแวร์อื่น ๆ ที่เชื่อมต่อกับระบบของพวกเขา

การใช้คำสั่ง lshw มักช่วยในการตรวจสอบข้อมูลฮาร์ดแวร์เพื่อการ debug , การแก้ไขปัญหาทางฮาร์ดแวร์ หรือการตรวจสอบสเปกของระบบ สามารถใช้คำสั่งนี้เพื่อรับข้อมูลที่ละเอียดเกี่ยวกับฮาร์ดแวร์ทั้งหมดที่มีบนระบบได้

## การใช้คำสั่ง lspci เพื่อตรวจสอบข้อผิดพลาดหรือปัญหาที่เกี่ยวข้องกับฮาร์ดแวร์บนระบบ Linux


### Permission Denied Error
ข้อผิดพลาดที่อาจพบบ่อยเมื่อใช้คำสั่ง lspci คือข้อผิดพลาด 'Permission denied' หรือ 'การปฏิเสธสิทธิ์' นั่นล้วนเป็นเรื่องที่เกิดขึ้นเมื่อพยายามเข้าถึงข้อมูลฮาร์ดแวร์โดยไม่มีสิทธิ์ที่จำเป็น

ต่อไปนี้คือตัวอย่างของข้อผิดพลาดนี้:

command
```
lspci -v
```
output
```
lspci: Unable to open /proc/bus/pci
lspci: Cannot find any working access method.
```

ในตัวอย่างนี้ คำสั่ง lspci -v ล้มเหลวเนื่องจากไม่มีสิทธิ์ที่จำเป็นในการเข้าถึง /proc/bus/pci การแก้ไขปัญหานี้คือการรันคำสั่ง lspci ด้วย sudo:

command
```
sudo lspci -v
```
output
```
00:00.0 Host bridge: Intel Corporation 8th Gen Core Processor Host Bridge/DRAM Registers (rev 07)
        Subsystem: Lenovo Device 3801
        Flags: bus master, fast devsel, latency 0
        Capabilities: <access denied>
...
```
run คำสั่ง lspci ด้วยสิทธิ์ root ซึ่งทำให้มันสามารถเข้าถึงไดเรกทอรีที่จำเป็นและแสดงผลลัพธ์แบบ verbose ได้

### Incorrect or Unrecognized Command Options
ปัญหาที่พบบ่อยคือการใช้ตัวเลือกคำสั่งที่ไม่ถูกต้องหรือไม่รู้จัก หากใช้ตัวเลือกที่ lspci ไม่รู้จักมันจะแสดง error message

ต่อไปนี้คือตัวอย่างของข้อผิดพลาดนี้:

command
```
lspci -z
```
output
```
lspci: invalid option -- 'z'
Usage: lspci [<switches>]
```
-z ไม่ได้รับการรับรองโดยคำสั่ง lspci ซึ่งทำให้มันแสดง error message เพื่อแก้ไขปัญหานี้ ควรตรวจสอบหน้าคู่มือของ lspci (`man lspci`) หรือใช้ตัวเลือก --help (`lspci --help`) เพื่อรับรายการของตัวเลือกที่ถูกต้อง

### Best Practices and Optimization
เมื่อใช้คำสั่ง lspci, มีบางแนวทางที่ดีที่ควรจำไว้:

1. ใช้ command ที่ถูกต้องเสมอ: การใช้ตัวเลือกที่ไม่ถูกต้องหรือไม่รู้จักอาจทำให้เกิดข้อผิดพลาด ควรตรวจสอบหน้าคู่มือ (`man page`) ของ lspci หรือใช้ตัวเลือก --help หากไม่แน่ใจเกี่ยวกับตัวเลือกใด ๆ

2. ใช้ sudo เมื่อจำเป็น: บางการทำงานของ lspci ต้องการสิทธิ์ root หากเจอข้อผิดพลาด 'Permission denied', ลองรันคำสั่ง lspci ด้วย sudo

3. ใช้ grep เพื่อกรองผลลัพธ์: หากมีจำนวนของอุปกรณ์ที่ต้องการจัดการมาก ผลลัพธ์ของ lspci อาจทำให้สับสน สามารถใช้คำสั่ง grep เพื่อกรองผลลัพธ์และทำให้มันง่ายต่อการอ่าน ตัวอย่างเช่น `lspci | grep -i nvidia` จะแสดงเฉพาะบรรทัดที่มีคำว่า 'nvidia'

## ทำความเข้าใจระบบ PCI bus ใน Linux
"Peripheral Component Interconnect (PCI)" คือ ช่องสื่อสารข้อมูลที่ทำงานด้วยความเร็วสูงที่เชื่อมต่อ CPU กับฮาร์ดแวร์ที่ผนวกมากับเครื่อง (เช่น Ethernet controller และ video adapter) และการ์ดฮาร์ดแวร์เสริม (เช่น การ์ด Wi-Fi หรือ Graphics Processing Unit)

ใน Linux ระบบ PCI bus จะถูกตรวจพบและจัดการโดย kernel โดยอัตโนมัติ ซึ่งยังให้ส่วนต่อประสานให้แอปพลิเคชันทำงานร่วมกับอุปกรณ์ PCI คำสั่ง lspci เป็นหนึ่งในแอปพลิเคชันที่ออกแบบมาเพื่อให้สามารถดูและจัดการอุปกรณ์ PCI ในระบบได้ด้วยวิธีที่ใช้งานง่าย

มาดูตัวอย่างที่แสดงลำดับความสูงของ PCI bus โดยใช้ command -t:
command
```
lspci -t
```
output
```
-[0000:00]-+-00.0
           +-01.0-[01]--
           +-14.0
           +-16.0
           +-1c.0-[02]----00.0
           +-1c.4-[03]----00.0
           +-1f.0
           +-1f.2
           \-1f.3
```
คำสั่งนี้แสดงอุปกรณ์ในรูปแบบ diagram ที่มีลักษณะคล้าย tree เพื่อแสดงวิธีที่พวกมันเชื่อมต่อกับ bus ต่าง ๆ ในระบบ ทุกเลขแทนอุปกรณ์แต่ละตัว และเส้นแสดงวิธีที่พวกมันเชื่อมต่อกับ bus นั้น ๆ

## ข้อควรระวัง
การใช้คำสั่ง lspci และคำสั่งที่เกี่ยวข้องอื่น ๆ ในการตรวจสอบอินเทอร์เฟซของอุปกรณ์เป็นเครื่องมือที่มีประโยชน์สำหรับทำความเข้าใจเกี่ยวกับอุปกรณ์ฮาร์ดแวร์ที่ติดตั้งในระบบ Linux การทำงานนี้ควรทำด้วยความระมัดระวังเพื่อป้องกันไม่ให้เกิดความผิดพลาดหรือการเข้าถึงข้อมูลที่ไม่ได้รับอนุญาต เช่น การใช้ lspci บางทีต้องเป็น root

## References

1. https://ioflood.com/blog/lspci-linux-command/
2. chatgpt
