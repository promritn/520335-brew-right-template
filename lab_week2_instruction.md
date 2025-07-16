# Lab Week2 : Hello Docker

## 0. สร้าง Branch ใหม่ 
```bash
git checkout -b lab/week2
```

## 1. โครงสร้างโปรเจกต์

```
lab_week2/
├── app.py
├── requirements.txt
├── Dockerfile
└── docker-compose.yml
```

---

## 2. ตรวจสอบไฟล์

```bash
ls -R
```

ควรแสดง:

```
app.py
requirements.txt
Dockerfile
docker-compose.yml
```

---

## 3. แก้ไขโค้ด app.py

```python
# app.py
import streamlit as st

st.title("Hello, Streamlit!")
st.write("Welcome to your first Streamlit app running in Docker! 🚀")
```

---

## 4. แก้ไข requirements.txt

```text
streamlit
```

---

## 5. แก้ไข Dockerfile

```dockerfile
FROM python:3.10-slim

WORKDIR /app

COPY requirements.txt ./
RUN pip install --no-cache-dir -r requirements.txt

COPY app.py ./

EXPOSE 8501

CMD ["streamlit", "run", "app.py", "--server.port=8501", "--server.address=0.0.0.0"]
```

---

> **หมายเหตุ:** เนื่องจากเราแมปโฟลเดอร์โปรเจกต์เข้า `/app` ด้วย volumes ใน docker-compose, ขั้นตอน `COPY app.py ./` ใน Dockerfile จะไม่จำเป็นสำหรับการพัฒนา (dev) เพราะโค้ดจะถูกโหลดจากโฟลเดอร์แมปโดยตรง แต่ยังคงแนะนำให้ใส่ไว้ใน Dockerfile เพื่อให้ image ทำงานได้แบบ standalone (เช่น ใน production หรือ CI/CD)

## 6. แก้ไข docker-compose.yml

```yaml
version: '3.8'

services:
  streamlit-app:
    build: .
    ports:
      - "8501:8501"
    volumes:
      - ./:/app
    environment:
      - STREAMLIT_SERVER_ENABLECORS=false
```

---

## 7. Build & Run

```bash
docker-compose up --build -d
```

รอจนเห็น:

```
Local URL: http://localhost:8501
```

---

## 8. เปิดเว็บ & ทดสอบ

- เปิดเบราว์เซอร์ไปที่ `http://localhost:8501`
- คุณจะเห็นข้อความ **Hello, Streamlit!** และข้อความต้อนรับ

---

## 9. แก้ไขโค้ด แล้วดูผลทันที

1. แก้ไข `app.py` เช่น:

```python
# เปลี่ยนบรรทัดนี้
st.write("Welcome to your first Streamlit app running in Docker! 🚀")
# เป็น
st.write("Updated: สวัสดีจาก Brew-Right! ☕")
```

2. บันทึกไฟล์ → Docker Compose จะ reload อัตโนมัติ (เพราะแมปโฟลเดอร์)
3. รีเฟรชเว็บ → เห็นข้อความใหม่ทันที

---

## 10. ปิดและ cleanup

```bash
docker-compose down
# ถ้าต้องการลบ image ด้วย
docker-compose down --rmi all
```
## 11. Stage & Commit โค้ดทั้งหมด

```bash
git add .
git commit -m "Add Hello World Docker setup"
```

## 12. Push branch ขึ้น remot
```bash
git push origin lab/week2
```

## 13. ไปที่หน้า GitHub ของ repo → จะเห็นปุ่ม **Compare & pull request**
คลิก **Compare & pull request** → ใส่หัวเรื่อง เช่น "Add Streamlit Docker Hello World lab"
กด **Create pull request** → ส่งให้ทีม review

## 14. เมื่อทีม Review แล้ว บน GitHub ให้กดปุ่ม **Merge pull request** แล้วกด **Confirm merge** แล้วลบ Branch lab/week2

## 15. Pull การเปลี่ยนแปลงกลับมาที่เครื่อง
```bash
git checkout main
git pull origin main
```
## 16 ลบ Branch lab/week2 ที่เครื่อง
```bash
git branch -d lab/week2
```
