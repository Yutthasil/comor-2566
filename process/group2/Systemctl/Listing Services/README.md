## แสดงรายการ Service
ใช้คำสั่งต่อไปนี้
```
systemctl list-units --type=service --all
```
![list](https://linuxhint.com/wp-content/uploads/2021/03/image2-20.png)

## แสดงรายการ Service ที่มีสถานะที่กําหนด
ใช้คำสั่งต่อไปนี้
```
systemctl list-units --type=service --state=STATE
```
> systemctl list-units --type=service --state=running

![running](https://linuxhint.com/wp-content/uploads/2021/03/image3-20.png)

## หน่วยและสถานะของ systemd:

- **UNIT:** ชื่อหน่วย systemd
  
- **LOAD:** บอกว่าการกำหนดค่าของหน่วยได้ถูกแปลเป็นระบบโดย systemd หรือไม่
  
- **ACTIVE:** สถานะสรุปเกี่ยวกับว่าหน่วยทำงานอยู่หรือไม่
  
- **SUB:** สถานะระดับต่ำที่แสดงข้อมูลรายละเอียดเพิ่มเติมเกี่ยวกับหน่วย
  
- **DESCRIPTION:** คำอธิบายย่อของหน่วยนี้
