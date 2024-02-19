## เปิดใช้งาน Service
กำหนดค่าให้บริการเริ่มต้นโดยอัตโนมัติ ทุกครั้งที่ระบบเปิดใหม่
```
systemctl enable name.service
```
> systemctl enable ssh

![enable](https://github.com/Markkerg/Process-1/blob/main/Assets/systemctl/enable.png?raw=true)

## ปิดใช้งาน Service
ปิดใช้งานบริการ ป้องกันไม่ให้บริการเริ่มต้นโดยอัตโนมัติทุกครั้งที่ระบบเปิดใหม่
```
systemctl disable name.service
```
> systemctl disable ssh

![disable](https://github.com/Markkerg/Process-1/blob/main/Assets/systemctl/disable.png)
