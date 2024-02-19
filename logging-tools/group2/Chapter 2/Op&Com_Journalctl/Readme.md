# Option และ Command ทั้งหมดของคำสั่ง journalctl

## Option ทั้งหมดของคำสั่ง journalctl
<div align="center" style="width: 100%; margin: auto;">
<table style="width: 100%; border-collapse: collapse;">
	
| Options                 | Description                | Example   | Result |
| :---------------:  | :---------------------: | :-----------------: | :----------------: |
| --system | แสดงข้อความจาก service ของระบบ | journalctl --system | <img align="right" width="100%" src="image/jourSystem.png"> |
| --user | แสดงข้อความจาก service ของผู้ใช้ | journalctl --user | <img align="right" width="100%" src="image/jourUser.png"> |
| -M, --machine=CONTAINER | แสดงข้อความจาก machine หรือ container นั้นๆ | journalctl -M CONTAINER_NAME |  |
| -S, --since=DATE | แสดงข้อความตั้งแต่เวลาที่กำหนด | journalctl --since "2024-02-04 10:00:00" | <img align="right" width="100%" src="image/jourSince.png"> |
| -U, --until=DATE | แสดงข้อความจนถึงเวลาที่กำหนด | journalctl --until "2024-02-10 10:00:00" | <img align="right" width="100%" src="image/jourUntil.png"> |
| -c, --cursor=CURSOR | แสดงบันทึกตามตำแหน่งที่กำหนด | journalctl -c <cursor_value> |  |
| --after-cursor=CURSOR | แสดงบันทึกที่เกิดขึ้นหลังจากตำแหน่งที่กำหนด | journalctl --after-cursor=<cursor_value> |  |
| --show-cursor | แสดง curosr | journalctl --show-cursor | <img align="right" width="100%" src="image/jourShowCursor.png"> |
| --cursor-file=FILE |  |  |  |
| -b [ID][±offset], --boot [=ID][±offset] | แสดงข้อความที่เกี่ยวกับการบูต โดยกำหนดลำดับได้ | journalctl -b [ID][±offset] | <img align="right" width="100%" src="image/jourBoot.png"> |
| --list-boots | แสดงผลบูตแบบ list | journalctl --list-boots | <img align="right" width="100%" src="image/jourListBoot.png"> |
| -k, --dmesg | แสดงบันทึกในระดับ kernel | journalctl -k | <img align="right" width="100%" src="image/jourDmesg.png"> |
| -u, --unit=UNIT | แสดงข้อความเกี่ยวกับ unit ใน system unit | journalctl -u UNIT | <img align="right" width="100%" src="image/jourUnit.png"> |
| --user-unit=UNIT | แสดงข้อความเกี่ยวกับ unit ใน user unit | journalctl --user-unit=UNIT | <img align="right" width="100%" src="image/jourUserUnit.png"> |
| -t, --identifier=STRING | แสดงบันทึกที่เป็นค่า identifier ที่กำหนด | journalctl -t STRING | <img align="right" width="100%" src="image/jourIdentifier.png"> |
| -p, --priority=RANGE | แสดงข้อความตามระดับความสำคัญ (Range=0-7) | journalctl -p RANGE | <img align="right" width="100%" src="image/jourPriority.png"> |
| --facility=FACILITY | กรองและแสดงข้อความตาม facility(0-23) | journalctl --facility=FACILITY | <img align="right" width="100%" src="image/jourFacility.png"> |
| -g, --grep=PATTERN | กรองและแสดงข้อความตาม pattern | journalctl -g PATTERN | <img align="right" width="100%" src="image/jourGrep.png"> |
| --case-sensitive[=BOOL] | เงื่อนไขเพิ่มเติม โดยไม่สนพิมพ์เล็ก-ใหญ่ | journalctl --grep “error ” --case-sensitive | <img align="right" width="100%" src="image/jourCaseSensitive.png"> |
| -e, --pager-end | เพื่อเรียกใช้งาน pager | journalctl -e | <img align="right" width="100%" src="image/jourPager.png"> |
| -f, --follow | ติดตามบันทึกข้อความใหม่ที่เพิ่มเข้ามาใน journal ในขณะที่โปรแกรมกำลังทำงานอยู่ | journalctl -f | <img align="right" width="100%" src="image/jourFollow.png"> |
| -n, --lines[=INTEGER] | กำหนดจำนวนบันทึกข้อความที่จะแสดง | journalctl -n 1 | <img align="right" width="100%" src="image/jourLines.png"> |
| --no-tail | แสดงบันทึกข้อความทั้งหมดโดยไม่ติดตามบันทึกใหม่ | journalctl --no-tail | <img align="right" width="100%" src="image/jourNoTail.png"> |
| -r, --reverse | แสดงบันทึกข้อความในลำดับย้อนกลับ คือจากบันทึกล่าสุดไปยังบันทึกเก่าสุด | journalctl -r | <img align="right" width="100%" src="image/jourReverse.png"> |
| -o, --output=STRING | กำหนดรูปแบบการแสดงผลของบันทึกข้อความ เช่น json, json-pretty | journalctl -o json | <img align="right" width="100%" src="image/jourOutput.png"> |
| --output-fields=LIST | กำหนดรายการของฟิลด์ที่ต้องการให้แสดง เช่น MESSAGE, PRIORITY, SYSLOG_IDENTIFIER | journalctl --output-fields=MESSAGE | <img align="right" width="100%" src="image/jourOutputFields.png"> |
| --utc | แสดงเวลาในบันทึกข้อความตามเวลาสากล | journalctl --utc | <img align="right" width="100%" src="image/jourUtc.png"> |
| -x, --catalog | แสดงผลลัพธ์ในรูปแบบ catalog | journalctl -x | <img align="right" width="100%" src="image/jourCatalog.png"> |
| --no-full | ปิดการแสดงผลข้อความในโหมดเต็มหน้าจอ | journalctl --no-full | <img align="right" width="100%" src="image/jourNoFull.png"> |
| -a, --all | แสดงข้อความทั้งหมด | journalctl -a | <img align="right" width="100%" src="image/jourAll.png"> |
| -q, --quiet | ปิดข้อความเตือน | journalctl -q | <img align="right" width="100%" src="image/jourQuiet.png"> |
| --no-pager | ปิดการแบ่งหน้า โดยจะแสดงข้อความทั้งหมดอัตโนมัติ | journalctl --no-pager | <img align="right" width="100%" src="image/jourNoPager.png"> |
| --no-hostname | ไม่แสดงชื่อโฮสต์ของระบบ | journalctl --no-hostname | <img align="right" width="100%" src="image/jourNoHostname.png"> |
| -m, --merge | แสดงข้อความที่แทรกเข้ามา | journalctl -m | <img align="right" width="100%" src="image/jourMerge.png"> |
| -D, --directory=PATH | ระบุไดเร็กทอรีที่จะใช้สำหรับการค้นหา journal files | journalctl -D | <img align="right" width="100%" src="image/jourDirectory.png"> |
| --file=PATH | ระบุไฟล์บันทึก journal ที่ต้องการอ่าน | journalctl --file=PATH |  |
| --root=ROOT | ใช้สำหรับระบุไดเร็กทอรีรูท | journalctl --root=ROOT | <img align="right" width="100%" src="image/jourRoot.png"> |
| --image=IMAGE | แสดงภาพจาก disk image | journalctl --image=IMAGE |  |
| --namespace=NAMESPACE | ใช้ระบุ namespace | journalctl --namespace=NAMESPACE | <img align="right" width="100%" src="image/jourNamespace.png"> |
| --interval=TIME | กำหนดเวลาในการรีเฟรชข้อมูล เมื่อใช้ --setup-key | journalctl - f --interval=TIME | <img align="right" width="100%" src="image/jourInterval.png"> |
| --verify-key=KEY | ใช้เพื่อระบุคีย์ FSS สำหรับ verify เป็นการตรวจสอบความสมบูรณ์และความถูกต้องของข้อมูลใน journal files | journalctl --verify-key=KEY |  |
| --force | เมื่อ --setup-keys ผ่าน และ FSS ถูกกำหนดค่าแล้ว จะทำการสร้าง FSS ใหม่ | journalctl --force | <img align="right" width="100%" src="image/jourForce.png"> |
</table>
</div>

## Command ทั้งหมดของคำสั่ง journalctl
<div align="center" style="width: 100%; margin: auto;">
<table style="width: 100%; border-collapse: collapse;">
	
| Options                 | Description                | Example   | Result |
| :---------------:  | :---------------------: | :-----------------: | :----------------: |
| -h, --help | แสดงข้อความช่วยเหลือ | journalctl -h | <img align="right" width="100%" src="image/jourHelp.png"> |
| --version | แสดง version | journalctl --version | <img align="right" width="100%" src="image/jourVersion.png"> |
| -N, --fields | แสดงรายการชื่อฟิลด์ทั้งหมดที่ใช้อยู่ในปัจจุบัน | journalctl -N | <img align="right" width="100%" src="image/jourFields.png"> |
| -F, --field=FIELD | แสดงรายการค่าทั้งหมดที่ฟิลด์ที่ระบุใช้ | journalctl -F _PID | <img align="right" width="100%" src="image/jourField.png"> |
| --disk-usage | แสดงการใช้งานดิสก์ทั้งหมดของไฟล์เจอร์นัลทั้งหมด | journalctl --disk-usage | <img align="right" width="100%" src="image/jourDiskUsage.png"> |
| --vacuum-size=BYTES | ลดการใช้ดิสก์ให้ต่ำกว่าขนาดที่ระบุ | Journalctl –vauum-size=500 | <img align="right" width="100%" src="image/jourVacuumSize.png"> |
| --vacuum-files=INT | เหลือเพียงจำนวนไฟล์เจอร์นัลที่ระบุเท่านั้น | journalctl --vacuum-files=1 | <img align="right" width="100%" src="image/jourVacuumFiles.png"> |
| --vacuum-time=TIME | ลบไฟล์เจอร์นัลที่เก่ากว่าเวลาที่กำหนด | journalctl --vacuum-time=2weeks | <img align="right" width="100%" src="image/jourVacuumTime.png"> |
| --verify | ตรวจสอบความสอดคล้องของไฟล์ jounal | journalctl --verify | <img align="right" width="100%" src="image/jourVerify.png"> |
| --sync | ซิงโครไนซ์ข้อความบันทึกประจำวันที่ไม่ได้เขียนไปยังดิสก์ | journalctl journalctl --sync | <img align="right" width="100%" src="image/jourSync.png"> |
| --relinquish-var |หยุดการบันทึกลงในจาน เข้าสู่ระบบไฟล์ชั่วคราว | journalctl journalctl --relinquish-var | <img align="right" width="100%" src="image/jourRelinquish.png"> |
| --smart-relinquish-var | คล้ายกัน แต่ NOP หากไดเร็กทอรีบันทึกอยู่บนรูทเมาท์ | journalctl --smart-relinquish-var | |
| --flush | ล้างข้อมูลเจอร์นัลทั้งหมดจาก /run ลงใน /var | journalctl --flush | <img align="right" width="100%" src="image/jourFlush.png"> |
| --rotate | ขอหมุนเวียนไฟล์เจอร์นัลทันที | journalctl --rotate | <img align="right" width="100%" src="image/jourRotate.png"> |
| --header | แสดงข้อมูลส่วนหัวของวารสาร | journalctl --header | <img align="right" width="100%" src="image/jourHeader.png"> |
| --list-catalog | แสดงรหัสข้อความทั้งหมดในแค็ตตาล็อก | journalctl --list-catalog | <img align="right" width="100%" src="image/jourListCatalog.png"> |
| --dump-catalog | แสดงรายการในแค็ตตาล็อกข้อความ | journalctl --dump-catalog | <img align="right" width="100%" src="image/jourDumpCatalog.png"> |
| --update-catalog | อัพเดตฐานข้อมูลแค็ตตาล็อกข้อความ | sudo journalctl --update-catalog |  |
| --setup-keys |สร้างคู่คีย์ FSS ใหม่ | sudo journalctl --setup-keys | <img align="right" width="100%" src="image/jourSetupKeys.png"> |
</table>
</div>

