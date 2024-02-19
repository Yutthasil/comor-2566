# :penguin: Kernel :penguin:
### Kernel Module :notebook:
**Kernel Module** ทำหน้าที่เหมือนเป็น driver ที่ควบคุมการทำงานส่วนต่างๆ ทั้งในส่วนของฮาร์ดแวร์ รวมถึง file system ที่อยู่ในระบบปฏิบัติการ 
ข้อดีของ Kernel Module คือ สามารถติดตั้ง หรือนำ Kernel Module ออกไปจากระบบได้อย่างอิสระ โดยไม่จำเป็นต้องไปสร้าง Kernel ตัวใหม่

### Module Location :open_book:
- **/lib/modules/$(uname -r)/kernel** คือไดเรกทอรีหลักที่ใช้เก็บโมดูลของ kernel ทั้งหมดที่ถูกติดตั้งในระบบ หากต้องการแทรก ค้นหาไฟล์ หรือลบโมดูลออกจากเคอร์เนล สามารถเข้าไปค้นหาในไดเร็กทอรีโมดูลนี้ได้
    
  **Kernel Modules Subdirectories**
  
    | Directory | Description |
    | :---: | --- |
    | arch | The arch subdirectory contains all of the architecture specific kernel code |
    | drivers | All of the system's device drivers live in directory |
    | init | The initialization code for the kernel and start looking at how the kernel works |
    | include | Kernel headers |
    | ipc | Code used for process communication |
    | kernel | The main kernel code. specific in arch/*/kernel |
    | lib | Misc library routines |

### The `lsmod` Command :page_facing_up:
  - lsmod เป็นคำสั่งที่ใช้แสดงรายการโมดูลใน Linux Kernel โดยจะแสดงผลลัพธ์ออกมาเป็นไฟล์ /proc/modules
  - Syntax:
    
    ```
    lsmod 
    ```
  - ตัวอย่างผลลัพธ์
   
    ```
    host-3@host-3-server $ lsmod
    Module                  Size  Used by
    hid_logitech_hidpp     36864  0
    hid_logitech_dj        20480  0
    vmw_vsock_vmci_transport    32768  0
    vsock                  36864  1 vmw_vsock_vmci_transport
    vmw_vmci               69632  1 vmw_vsock_vmci_transport 
    ```
### The `modinfo` Command :page_facing_up:
  - คำสั่ง **modinfo** ใช้ในการแสดงข้อมูลโมดูลใน Linux Kernel
  - Syntax:
    
    ```
    modinfo [ OPTION ] [modulename|filename...] 
    ```
    
    **modinfo Command Options**
  
    | Options | Options Meaning |
    | :---: | --- |
    | -F, --field | Only print this field value, one per line |
    | -b basedir, --basedir basedir | Root directory for modules, / by default |
    | -k kernel | Provide information about a kernel other than the running one |
    | -o, --only-matching | Invert the sense of matching, to select non-matching lines |

  - ตัวอย่าง การแสดงข้อมูลตามชื่อ โดยการใช้ `lsmod` ในการดึงข้อมูลออกมา
   
    ```
    host-3@host-3-server $ lsmod
    Module                  Size  Used by
    ...
    vboxdrv               483328  2 vboxnetadp,vboxnetflt
    host-3@host-3-server $ modinfo vboxdrv
    filename:       /lib/modules/4.15.0-91-generic/misc/vboxdrv.ko
    version:        6.1.6 r137129 (0x002d0001)
    license:        GPL
    description:    Oracle VM VirtualBox Support Driver
    author:         Oracle Corporation
    srcversion:     1B117C52DF5B4D7EFB983ED
    depends:        
    retpoline:      Y
    name:           vboxdrv
    vermagic:       4.15.0-91-generic SMP mod_unload 
    parm:           force_async_tsc:force the asynchronous TSC mode (int)
    ```
### The `insmod` Command :page_facing_up:
  - insmod เป็นคำสั่งที่ใช้เพื่อโหลด(load) โมดูลเคิร์นเนล(kernel module) ลงใน kernel ของระบบ
  - Syntax:
    
    ```
    insmod [file name] [module-options...] 
    ```
  - ตัวอย่างแสดงการรันคำสั่ง `insmod` จากไดเร็กทอรี /lib/modules/$(uname -r) และไฟล์ .ko มีอยู่ในไดเร็กทอรี
   
    ```
    host-3@host-3-server $ insmod kernel/drivers/net/wireless/airo.ko
    host-3@host-3-server $ lsmod | grep axnet
    Module                  Size  Used by
    airo                   66291  0
    ```

### The `rmmod` Command :page_facing_up:
  - คำสั่ง rmmod ใช้เพื่อลบโมดูลออกจากเคอร์เนล สามารถใช้ `modprobe` พร้อมกับ `-r` แทนการใช้ rmmod ได้
  - Syntax:
    
    ```
    rmmod [-f] [-s] [-v] [modulename] 
    ```
  - ตัวอย่างการลบโมดูลออก โดยใช้คำสั่ง `lsmod`
   
    ```
    host-3@host-3-server $ rmmod axnet
    host-3@host-3-server $ lsmod | grep axnet
    host-3@host-3-server $
    ```
### The `modprobe` Command :page_facing_up:
  - modprobe เป็นคำสั่งที่ใช้แสดงรายการ แทรก หรือลบโมดูลออกจากเคอร์เนล โดยจะค้นหาในไดเร็กทอรีโมดูล `/lib/modules/$ (uname -r)`
  - Syntax:
    
    ```
    modprobe [ OPTIONS ] [modulename] [module parameters...]
    ```
    **modinfo Command Options**
  
    | Options | Options Meaning |
    | :---: | --- |
    | -f --force | Tries to strip any versioning information from the module |
    | -n, --dry-run, --show | does everything but insert or delete the modules (or run the install or remove commands) |
    | -v, --verbose | Prints messages about what the program is doing |
    | -r | `modprobe` to remove a module |

### The `depmod` Command :page_facing_up:
  - depmod เป็นคำสั่งที่ใช้ในการสร้างหรืออัปเดตไฟล์ใน Linux kernel
   - Syntax:
    
      ```
      depmod [ OPTIONS ] 
      ```
      **modinfo Command Options**
     
     | Options | Options Meaning |
     | :---: | --- |
     | -a --all | Probes all modules |
     | -C --config file or directory | overrides the default configuration file `at /etc/depmod.conf`  |
     | -n --dry-run | sends the resulting and the various map files to standard output |

   - ตัวอย่างการค้นหาไฟล์ `.ko` ใน /lib/modules/$(uname -r) เมื่อไฟล์ถูกพบ depmod จะทำงานและ จากนั้นจะรันคำสั่ง `modprobe` เพื่อติดตั้งโมดูล
   
      ```
      host-3@host-3-server $ ln -s /lib/modules/4.15.0-91-generic/kernel/crypto/md4.ko /lib/modules/4.15.0-91-generic/
      host-3@host-3-server $ depmod -a
      host-3@host-3-server $ modprobe md4
      ```
    
### Configuration :wrench:
  - คำสั่ง **modprobe** สามารถใช้เพิ่มหรือลบโมดูลได้ โดยมีไฟล์ .conf ทั้งหมดภายในส่วนขยายไดเร็กทอรี /etc/modprobe.d สำหรับระบุตัวเลือกที่จำเป็นสำหรับโมดูลต่างๆ 
  - file configuration สามารถใช้สร้าง alias (นามแฝงสำหรับโมดูล) หรือเปลี่ยนแปลงลักษณะการทำงานของ modprobe ตามความต้องการ
  - ไฟล์ .conf อยู่ในไดเร็กทอรี /etc/modprobe.d และใน Linux เวอร์ชันเก่า จะอยู่ในไฟล์ /etc/modprobe.conf

**Loadable module**
 - สามารถกำหนดค่าในไฟล์ .conf ที่อยู่ในไดเรกทอรี /etc/modules-load.d เพื่อโหลดโมดูลเหล่านั้นขณะที่ระบบกำลังเริ่มในส่วนของ init ของกระบวนการบูต
 - ทุกโมดูลจะถูกระบุหนึ่งโมดูลต่อ 1 บรรทัด เช่นสร้างไฟล์ /etc/modules.d/networking.conf และกำหนดโมดูลให้มีการโหลด 3 รายการดังนี้
   ```
   tun
   e1000e
   brcmfmac
   ```
- การจำกัดไม่ให้โมดูลถูกโหลด ให้ทำการเพิ่มชื่อของโมดูลลงในไฟล์ที่อยู่ใน /etc/modprobe.d/ และให้เริ่มต้นทุกชื่อโมดูลด้วย "blacklist"
  ```
  blacklist uhci_hcd
  blacklist nvidia
  ```
- การสร้างชื่อแฝง (alias) สำหรับชื่อโมดูล สามารถสร้างfile .conf /etc/modprobe.d/ เช่น myalias.conf และ กำหนดผ่านโครงสร้าง alias [alias] [module name]
  ตัวอย่างด้านล่างเป็นการสร้าง alias mymod แทนชื่อโมดูลที่ยาวเกินไป
  ```
    alias mymod really_long_module_name
  ```
### Kernel Paramiters :newspaper:
- ไดเรกทอรี /proc/sys มีไฟล์และไดเรกทอรีหลายรายการที่มีประโยชน์ในการเปลี่ยนแปลงการตั้งค่าของคอนเน็กเตอร์ มีประโยชน์เมื่อต้องการแก้ปัญหาหรือปรับแต่งระบบ Linux

  ไดเรกทอรี /proc/sys ถูกแบ่งออกเป็นไดเรกทอรีย่อยได้แก่:

  | Subdirectory | What it is |
  | :---: | --- |
  | abi/ | Execution domains & personalities |
  | debug/ | <empty> |
  | dev/ |Device specific information (eg dev/cdrom/info)|
  | fs/ | Specific filesystems filehandle, inode, dentry and quota tuning binfmt_misc <Documentation/admin-guide/binfmt-misc.rst> |
  | kernel/ | Global kernel info / tuning miscellaneous stuff |
  | net/ | Networking stuff, for documentation look in: <Documentation/networking/> |
  | vm/ | Memory management tuning buffer and cache management |
  | user/ | Per user per user namespace limits |

**The `sysctl` Command**

- คำสั่ง sysctl เป็นเครื่องมือซอฟต์แวร์ที่อ่านและปรับเปลี่ยนคุณสมบัติของ kernel เช่น เวอร์ชัน, maximum limits, และการตั้งค่าความปลอดภัย
- สามารถใช้งานได้ทั้งในโหมดแบบอินเทอร์แอคทีฟและแบบสคริปต์
- Syntax:
  ```
  sysctl [ OPTIONS ]
  ```
  | Options | Options Meaning |
  | :---: | --- |
  | -a, --all | Display all values currently available. |
  | -e, --ignore | Use this option to ignore errors about unknown keys. |
  | -p {FILENAME}, --load[=FILENAME] | Load in sysctl settings from the file specified or /etc/sysctl.conf if none given. |
  | -r, --pattern pattern | Only apply settings that match pattern. |
  | -w, --write | Use this option when you want to change a sysctl setting. |

- การดูว่า attributes มีอะไรบ้างให้ใช้คำสั่ง -a จะทำการแสดงผล parameters ทั้งหมดที่มีการ config ในปัจจุบัน
  ```
  host-3@host-3-server$ sysctl -a
  abi.vsyscall32 = 1
  debug.exception-trace = 1
  debug.kprobes-optimization = 1
  dev.cdrom.autoclose = 1
  dev.cdrom.autoeject = 0
  dev.cdrom.check_media = 0
  dev.cdrom.debug = 0
  dev.cdrom.info = CD-ROM information, Id: cdrom.c 3.20 2003/12/17
  ```

**The `sysctl.conf` File**
- systcl preload และ configuration file สามารถกำหนดได้ที่ /etc/sysctl.d/99-sysctl.conf
- การกำหนดค่าแต่ละอย่างจะอยู่ภายในไฟล์ต่างๆ ภายใน etc/sysctl.d 
- การเปลี่ยนแปลงตั้งค่าสามารถทำได้ผ่านการจัดการไฟล์หรือใช้ sysctl
- ตัวอย่างคำสั่งต่อไปนี้จะเป็นการเปลี่ยนแปลงค่าของพารามิเตอร์ kernel.sysrq จนกว่าระบบจะถูกรีบูต
  ```
  host-3@host-3-server$ sysctl kernel.sysrq=1
  ```
- หากต้องการรักษาการเปลี่ยนแปลงระหว่างรีบูต ให้ทำเพิ่มหรือแก้ไขบรรทัดที่ต้องการในไฟล์ /etc/sysctl.d/99-sysctl.conf หรือสร้างไฟล์พารามิเตอร์ที่เกี่ยวข้องในไดเรกทอรี /etc/sysctl.d/

### Monitoring :desktop_computer:
**The `/proc` Directory**
- ไฟล์ /proc เป็น virtual filesystem ตัวหนึ่ง บางครั้งถูกเรียกว่า pseudo-file system ของข้อมูลของ process
- ถือเป็นศูนย์ควบคุมและรวบรวมข้อมูลสำหรับ kernel เนื่องจากคำสั่งส่วนใหญ่เป็นการเรียกใช้ไฟล์ในไดเรกทอรีนี้ ตัวอย่างเช่น 'lsmod' คือการเรียก 'cat /proc/modules' เป็นต้น
  
  | Directories | Contentents |
  | :---: | --- |
  | /proc/cmdline | Options passed to the kernel by the boot loader at boot time, such as mounting the kernel as read-only. |
  | /proc/cpuinfo | Information about the processor, such as its type, make, model, and performance. |
  | /proc/devices | List of device drivers configured into the currently running kernel. |
  | /proc/filesystems | Filesystems configured into the kernel. |
  | /proc/interrupts | Shows which interrupts are in use, and how many of each there have been. |
  | /proc/ioports | Which I/O ports are in use at the moment. |
  | /proc/meminfo | Information about memory usage, both physical and swap. |
  | /proc/modules | Which kernel modules are loaded at the moment. |
  | /proc/net | Status information about network protocols. |
  | /proc/stat | Various statistics about the system, such as the number of page faults since the system was booted. |
  | /proc/uptime | The length of time the kernel has been running since boot and spent in idle mode (both in seconds). |
- สามารถหาข้อมูลเกี่ยวกับ kernel ได้ในไฟล์ /proc/version
  ```
  host-3@host-3-server$ cat /proc/version
  Linux version 5.15.0-91-generic (buildd@lcy02-amd64-045) (gcc (Ubuntu 11.4.0-1ubuntu1~22.04)) 11.4.0,
   GNU 1d (( GNU Bitnutils for Ubantu) 2.38)# 101-Ubuntu SMP Tue Nov 14 13:30:38 UTC 2023
  ```
  ความหมายของผลลัพธ์
  - 5 -- Kernel version
  - 15 -- Major revision
  - 0 -- Minor revision
  - 91 -- Bug fix
  - generic - บอกว่ากำลังใช้ Ubantu ที่เป็น Desktop version โดยหากเป็น Server version จะเป็นคำว่า 'server'

**The `dmesg` Command**
- ใช้เพื่อเขียนข้อความเคอร์เนลบน Linux และระบบปฏิบัติการที่คล้าย Unix อื่น ๆ บนเอาต์พุตมาตรฐานในรูปแบบที่เป็นระเบียบมากขึ้น
- dmesg ใช้สำหรับตรวจสอบหรือควบคุมบัฟเฟอร์วงแหวนเคอร์เนล การดำเนินการเริ่มต้นคือการแสดงข้อความทั้งหมดในบัฟเฟอร์วงแหวนเคอร์เนล
- ข้อความที่สร้างโดยเคอร์เนลเป็นส่วนพื้นฐานของการ monitoring เนื่องจากในกรณีที่อุปกรณ์ล้มเหลวเราจะมีการสรุปเกี่ยวกับสิ่งที่เกิดขึ้นและใช้มาตรการสนับสนุนที่จำเป็น เมื่อเชื่อมต่อหรือยกเลิกการเชื่อมต่ออุปกรณ์ฮาร์ดแวร์ในระบบ
- Syntax:
  ```
  dmesg [ OPTIONS ]
  ```
  | Option Choice | Meaning |
  | :---: | --- |
  | -c, --read-clear | Clear the ring buffer after first printing its contents. |
  | -e, --reltime | Display the local time and the delta in human-readable format. Be aware that conversion to the local time could be inaccurate (see -T for more details). |
  | -f, --facility list | Restrict output to the given (comma-separated) list of facilities. |
  | -H, --human | Enable human-readable output. See also --color, --reltime and --nopager. |
  | -L, --color[=when] | Colorize the output. The optional argument when can be auto, never or always. If the when argument is omitted, it defaults to auto. The colors can be disabled; for the current built-in default see the --help output. See also the COLORS section below. |
  | -l, --level list | Restrict output to the given (comma-separated) list of levels. |
- ตัวอย่างผลลัพธ์
  ```
  host-3@host-3-server $ dmesg -H
  [Aug 4 12:58] Linux version 4.15.0-91-generic (buildd@lgw01-amd64-013) (gcc version 
  [  +0.000000] Command line: BOOT_IMAGE=/boot/vmlinuz-5.15.0-91-generic root=UUID=6e7
  [  +0.000000] KERNEL supported cpus:
  [  +0.000000]   Intel GenuineIntel
  [  +0.000000]   AMD AuthenticAMD
  [  +0.000000]   Centaur CentaurHauls
  [  +0.000000] x86/fpu: Supporting XSAVE feature 0x001: 'x87 floating point registers
  [  +0.000000] x86/fpu: Supporting XSAVE feature 0x002: 'SSE registers'
  [  +0.000000] x86/fpu: Enabled xstate features 0x3, context size is 576 bytes, using
  [  +0.000000] e820: BIOS-provided physical RAM map:
  [  +0.000000] BIOS-e820: [mem 0x0000000000000000-0x000000000009a7ff] usable
  [  +0.000000] BIOS-e820: [mem 0x00000000000f0000-0x00000000000fffff] reserved
  [  +0.000000] BIOS-e820: [mem 0x0000000000100000-0x00000000bfdffbff] usable
  [  +0.000000] BIOS-e820: [mem 0x00000000bfdffc00-0x00000000bfe53bff] ACPI NVS
  [  +0.000000] BIOS-e820: [mem 0x00000000bfe53c00-0x00000000bfe55bff] ACPI data
  [  +0.000000] BIOS-e820: [mem 0x00000000bfe55c00-0x00000000bfffffff] reserved
  [  +0.000000] BIOS-e820: [mem 0x00000000f8000000-0x00000000fbffffff] reserved
  [  +0.000000] BIOS-e820: [mem 0x00000000fec00000-0x00000000fed003ff] reserved
  [  +0.000000] BIOS-e820: [mem 0x00000000fed20000-0x00000000fed9ffff] reserved
  [  +0.000000] BIOS-e820: [mem 0x00000000fee00000-0x00000000feefffff] reserved
  [  +0.000000] BIOS-e820: [mem 0x00000000ffb00000-0x00000000ffffffff] reserved
  [  +0.000000] BIOS-e820: [mem 0x0000000100000000-0x000000033bffffff] usable
  [  +0.000000] NX (Execute Disable) protection: active
  ```
  
- ในระบบที่เป็นระบบเก่า บางบรรทัดของ dmesg จะเริ่มต้นด้วยชื่ออุปกรณ์ตามด้วยเครื่องหมายโคลอนแล้วตามด้วยรายละเอียด มักปรากฏเป็นกลุ่มที่มีอุปกรณ์เดียวกันต่อเนื่องกันในหลายบรรทัด




| References |
| :---: |
|[LibreTexts Engineering](https://eng.libretexts.org/Bookshelves/Computer_Science/Operating_Systems/Linux_-_The_Penguin_Marches_On_(McClanahan)/06%3A_Kernel_Module_Management/3.09%3A_The_dmesg_Command) |
|[Linux Adicts](https://www.linuxadictos.com/th/dmesg-comandos-informacion-solucionar-problemas-linux.html) |
|[Admin Info](https://th.admininfo.info/qu-hace-y-c-mo-usar-el-comando-dmesg-linux)|









