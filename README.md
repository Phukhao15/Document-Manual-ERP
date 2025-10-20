 🔒 การตั้งค่า Fail2Ban บน Linux Server

## 📁 1. เข้าสู่ไดเรกทอรีของ Fail2Ban
```bash
cd /etc/fail2ban
📄 2. สร้างไฟล์ jail.local

ไฟล์ jail.local จะใช้สำหรับเก็บการตั้งค่าที่ปรับแต่งเฉพาะของคุณ โดยไม่แก้ไขไฟล์ต้นฉบับ jail.conf
ให้คัดลอกไฟล์ต้นฉบับมาสร้างเป็นไฟล์ใหม่ดังนี้:
sudo cp jail.conf jail.local

📝 3. แก้ไขไฟล์ jail.local

เปิดไฟล์ด้วยโปรแกรมแก้ไขข้อความที่คุณต้องการ เช่น nano หรือ vi
sudo nano jail.local
# หรือ
sudo vi jail.local

  4. เพิ่ม IP ที่ต้องการยกเว้น (Whitelist)

ภายในไฟล์ jail.local ให้ทำดังนี้:

ค้นหาบรรทัดที่ขึ้นต้นด้วย ignoreip 
<img width="1018" height="481" alt="Screen Shot 2568-10-20 at 2 27 08 PM" src="https://github.com/user-attachments/assets/5bc7c91a-95dc-4a61-89f0-8f4fd2bf140d" />

ignoreip = 127.0.0.1/8 ::1  (เฉพาะ  Localhost)
ignoreip = 127.0.0.1/8 ::1 172.16.0.0/16 (ทั้ง subnet ของ ip ที่ต้องการ)

  5. Restart Service ของ Fail2ban

เพื่อให้การตั้งค่าใหม่มีผล ให้สั่ง Restart service:
sudo systemctl restart fail2ban

  6 เช็ค Status 
  sudo systemctl status fail2ban
