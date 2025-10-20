# 🔒 การตั้งค่า Fail2Ban 

## 📁 1. เข้าสู่ไดเรกทอรีของ Fail2Ban  
```bash
cd /etc/fail2ban
```

---

## 📄 2. สร้างไฟล์ `jail.local`  
ไฟล์ `jail.local` จะใช้สำหรับเก็บการตั้งค่าที่ปรับแต่งเฉพาะของคุณ โดยไม่แก้ไขไฟล์ต้นฉบับ `jail.conf`  
ให้คัดลอกไฟล์ต้นฉบับมาสร้างเป็นไฟล์ใหม่ดังนี้:

```bash
sudo cp jail.conf jail.local
```

---

## 📝 3. แก้ไขไฟล์ `jail.local`  
เปิดไฟล์ด้วยโปรแกรมแก้ไขข้อความที่คุณต้องการ เช่น `nano` หรือ `vi`

```bash
sudo nano jail.local
# หรือ
sudo vi jail.local
```

จากนั้นทำการปรับแต่งค่าตามต้องการ เช่น:
```ini
[sshd]
enabled = true
port = ssh
filter = sshd
logpath = /var/log/auth.log
maxretry = 5
bantime = 3600
findtime = 600
```

---

## ⚙️ 4. เพิ่ม IP ที่ต้องการยกเว้น (Whitelist)  
ภายในไฟล์ `jail.local` ให้ค้นหาบรรทัดที่ขึ้นต้นด้วย `ignoreip` และเพิ่ม IP ที่คุณต้องการ **ยกเว้นจากการถูกแบน (Whitelist)** เช่น:

```ini
ignoreip = 127.0.0.1/8 ::1        # เฉพาะ localhost  
ignoreip = 127.0.0.1/8 ::1 172.16.0.0/16   # ทั้ง subnet 172.16.0.0/16
```

> 💡 คุณสามารถเพิ่มหลาย IP หรือ subnet ได้ โดยคั่นด้วยช่องว่าง

![Fail2Ban Whitelist Example](https://github.com/Phukhao15/Document-Manual-ERP/blob/main/Screen%20Shot%202568-10-20%20at%203.15.05%20PM.png?raw=true)

---

## 🔄 5. รีสตาร์ทบริการของ Fail2Ban  
เพื่อให้การตั้งค่าใหม่มีผล ให้สั่งรีสตาร์ท service:

```bash
sudo systemctl restart fail2ban
```

---

## ✅ 6. ตรวจสอบสถานะการทำงาน  
ตรวจสอบว่า Fail2Ban ทำงานอยู่หรือไม่ด้วยคำสั่ง:

```bash
sudo systemctl status fail2ban
```

หากต้องการดู jail ทั้งหมดที่เปิดใช้งาน:
```bash
sudo fail2ban-client status
```

หรือดูสถานะของ jail เฉพาะ เช่น SSH:
```bash
sudo fail2ban-client status sshd
```

---

### 📘 สรุปขั้นตอน  
| ลำดับ | คำสั่ง | รายละเอียด |
|--------|---------|-------------|
| 1 | `cd /etc/fail2ban` | เข้าสู่ไดเรกทอรีหลักของ Fail2Ban |
| 2 | `sudo cp jail.conf jail.local` | คัดลอกไฟล์ตั้งค่าเดิม |
| 3 | `sudo nano jail.local` | แก้ไขไฟล์เพื่อตั้งค่า |
| 4 | `ignoreip = ...` | เพิ่ม IP ที่ต้องการยกเว้น |
| 5 | `sudo systemctl restart fail2ban` | รีสตาร์ทบริการ |
| 6 | `sudo systemctl status fail2ban` | ตรวจสอบสถานะการทำงาน |

---




