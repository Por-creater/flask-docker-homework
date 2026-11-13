# Flask Docker Homework

เว็บแอปพลิเคชันง่าย ๆ ด้วย Flask ที่รับข้อความผ่านฟอร์ม (POST), แสดงผลบนหน้าเว็บ, และบันทึกลงไฟล์ `log.txt` ภายใน container

## โครงสร้างไฟล์

```
flask-docker-homework/
├── app.py              # โค้ด Flask
├── Dockerfile          # สร้าง image
├── docker-compose.yml  # รัน container
├── requirements.txt    # dependencies
└── README.md
```

## วิธีรัน

```bash
# build และรัน container
docker-compose up --build

# เปิดเบราว์เซอร์ไปที่
http://localhost:5000
```

กรอกข้อความในฟอร์มแล้วกด Submit → หน้าเว็บจะแสดงข้อความที่ส่งไป และข้อความจะถูกต่อท้าย (append) ลงไฟล์ `log.txt` ภายใน container พร้อม timestamp

## การตรวจสอบ log.txt ภายใน container

เปิด terminal อีกหน้าต่างขณะ container กำลังรันอยู่:

```bash
# ดูชื่อ container ที่กำลังรัน
docker ps

# เข้าไปดูไฟล์ log.txt ข้างใน container
docker exec -it flask_docker_homework cat log.txt

# หรือเข้าไปเปิด shell ข้างในเลย
docker exec -it flask_docker_homework /bin/sh
cat log.txt
```

## ภาพหน้าจอที่ต้องแนบส่ง (สร้างเองจากเครื่องของผู้เรียน)

ทำตามขั้นตอนนี้แล้ว capture หน้าจอ 3 ภาพ:

1. **ภาพหน้าเว็บฟอร์มกรอกข้อความ** — เปิด `http://localhost:5000` แล้วแคปหน้าฟอร์มว่างก่อนกด submit
2. **ภาพหลังจากกดปุ่มส่งข้อมูล** — กรอกข้อความ กด Submit แล้วแคปหน้าที่แสดง "Message received: ..."
3. **ภาพหน้าจอ Terminal** — แคป 2 ช่วง:
   - ตอนรันคำสั่ง `docker-compose up` (เห็น log ว่า container start สำเร็จ)
   - ตอนรัน `docker exec -it flask_docker_homework cat log.txt` (เห็นข้อความที่บันทึกไว้)

หลังรันจริงแล้ว ให้ copy ไฟล์ log.txt ตัวอย่างออกมาจาก container ด้วยคำสั่งนี้ แล้วใส่ไว้ในโฟลเดอร์โปรเจกต์ก่อน push ขึ้น GitHub:

```bash
docker cp flask_docker_homework:/app/log.txt ./log.txt
```

## ขั้นตอนส่งงาน

1. สร้าง repository บน GitHub ชื่อ `flask-docker-homework`
2. push ไฟล์ทั้งหมด: `app.py`, `Dockerfile`, `requirements.txt`, `docker-compose.yml`, `log.txt` (ตัวอย่างที่ copy ออกมา), และภาพหน้าจอ 3 ภาพ (แนะนำเก็บในโฟลเดอร์ `screenshots/`)
3. แนบลิงก์ GitHub repo ส่งใน Google Classroom
