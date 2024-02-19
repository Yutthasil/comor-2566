## รีสตาร์ท Service
คำสั่งนี้หยุดบริการที่เลือกในเซสชันปัจจุบันและเริ่มต้นใหม่ทันที หากบริการที่เลือกไม่ได้ทำงาน คำสั่งนี้จะทําให้บริการทำงาน
```
systemctl restart name.service
```
> systemctl restart ssh

![restart](https://github.com/Markkerg/Process-1/blob/main/Assets/systemctl/restart.png)

## รีโหลด Service
การรีโหลดจะทำให้บริการนำเข้าการตั้งค่าใหม่โดยไม่ต้องหยุดการทำงานของบริการ
```
systemctl reload name.service
```
> systemctl reload ssh

![reload](https://github.com/Markkerg/Process-1/blob/main/Assets/systemctl/reload.png)
