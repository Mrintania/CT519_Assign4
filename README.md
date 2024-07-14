# Nginx Reverse Proxy with Docker Compose

โปรเจกต์นี้แสดงการใช้งาน Nginx เป็น reverse proxy เพื่อกระจายงานไปยัง web server สองตัวโดยใช้ Docker Compose

## โครงสร้างโปรเจกต์
```
assign4/
├── docker-compose.yml
├── web1/
│   └── index.html
└── web2/
    └── about/
        └── index.html
        └── photos.jpeg
```

## การติดตั้ง

1. ตรวจสอบว่าคุณได้ติดตั้ง Docker และ Docker Compose บนเครื่องของคุณแล้ว
2. Clone หรือดาวน์โหลดโปรเจกต์นี้ไปยังเครื่องของคุณ

## การใช้งาน

1. เปิด terminal และนำทางไปยังโฟลเดอร์ของโปรเจกต์:
```bash
cd ~/assign4
```
2. สร้างและเริ่มต้น containers:

```bash
docker-compose up --build
```

3. เข้าถึงเว็บไซต์:
- หน้าหลัก: http://localhost/ (จะแสดงเนื้อหาจาก web1)
- หน้า About: http://localhost/about (จะแสดงเนื้อหาจาก web2)

4. หากต้องการหยุดการทำงานของ containers กด Ctrl+C ใน terminal ที่รัน docker-compose

5. หากต้องการหยุดและลบ containers:

```bash
docker-compose down
```

## รายละเอียดเพิ่มเติม

- **web1**: เซิร์ฟเวอร์ที่ให้บริการหน้าหลัก ทำงานบนพอร์ต 80 ภายใน container
- **web2**: เซิร์ฟเวอร์ที่ให้บริการหน้า About ทำงานบนพอร์ต 80 ภายใน container
- **nginx**: ทำหน้าที่เป็น reverse proxy กระจายการร้องขอไปยัง web1 และ web2 ตาม URL path

## การแก้ไขปัญหา

หากคุณพบปัญหาในการรัน containers ลองทำตามขั้นตอนต่อไปนี้:

1. ตรวจสอบว่า Docker และ Docker Compose ทำงานอย่างถูกต้อง
2. ตรวจสอบว่าไม่มี services อื่นที่ใช้พอร์ต 80 บนเครื่องของคุณ
3. ลอง rebuild images:\

```
docker-compose build --no-cache
```

4. หากยังมีปัญหา ลองลบ containers และ images ทั้งหมดแล้วเริ่มต้นใหม่:

```
docker-compose down --rmi all
docker-compose up --build
```

## การสนับสนุน

หากคุณมีคำถามหรือพบปัญหา กรุณาสร้าง issue ในระบบ issue tracking ของ repository นี้