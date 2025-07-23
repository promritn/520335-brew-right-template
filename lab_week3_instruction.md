# Lab Week3 : Data Ingestion และ Bronze Layer

## 0. สร้าง Branch ใหม่ 
```bash
git checkout -b lab/week3
```

## 1. ตรวจสอบโครงสร้างโปรเจกต์

ตรวจสอบว่ามีไฟล์และโฟลเดอร์ที่จำเป็นแล้ว

```bash
ls -la notebooks/
```

ควรแสดง
```
notebooks/
├── week03_api_web_scraping.ipynb
└── week03_bronze_ingestion.ipynb
```

---

## 2. เริ่ม Docker Services

เริ่ม MinIO และ services อื่นๆ ที่จำเป็น

```bash
docker-compose up -d
```

ตรวจสอบว่า services ทำงานแล้ว

```bash
docker-compose ps
```

---

## 3. ทำงานกับ Notebook 1: API และ Web Scraping

ใช้ VS Code เปิดไฟล์ `week03_api_web_scraping.ipynb`

### 3.1 ทดสอบ API Client
- ทดสอบการดึงข้อมูลจาก Coffee API
- ทำความเข้าใจ HTTP headers และ error handling
- ลองแก้ไขโค้ดในส่วน template exercises

### 3.2 ทดสอบ Web Scraping
- ทดสอบการ scrape ข้อมูลราคากาแฟจาก ธปท.
- เรียนรู้การใช้ BeautifulSoup
- ตรวจสอบ robots.txt ก่อน scraping

---

## 4. ทำงานกับ Notebook 2: Bronze Layer Ingestion

เปิดไฟล์ `week03_bronze_ingestion.ipynb`

### 4.1 ตั้งค่าการเชื่อมต่อ MinIO
- ตรวจสอบการเชื่อมต่อ MinIO
- ดู buckets ที่มีอยู่ (bronze, silver, gold)

### 4.2 ทดสอบการอัพโหลดข้อมูล
- อัพโหลดข้อมูล JSON จาก API
- อัพโหลดข้อมูล CSV จาก web scraping
- ตรวจสอบ Medallion Architecture structure

### 4.3 ตรวจสอบข้อมูลใน MinIO
เปิด MinIO Console: http://localhost:9011
- Username: `minioadmin`
- Password: `minioadmin`

ตรวจสอบว่าข้อมูลถูกบันทึกใน bronze bucket แล้ว

---

## 5. Stage & Commit โค้ดทั้งหมด

```bash
git add .
git commit -m "Add Week 3 Data Ingestion and Bronze Layer implementation"
```

---

## 6. Push branch ขึ้น remote

```bash
git push origin lab/week3
```

---

## 7. สร้าง Pull Request

1. ไปที่หน้า GitHub ของ repo
2. จะเห็นปุ่ม **Compare & pull request**
3. คลิก **Compare & pull request**
4. ใส่หัวเรื่อง: `Week 3: Data Ingestion และ Bronze Layer Implementation`
5. ใส่รายละเอียด
   ```
   ## สิ่งที่เพิ่มใน Week 3
   
   ### 📊 Data Ingestion Pipeline
   - API Client สำหรับดึงข้อมูลจาก Coffee APIs
   - Web Scraper พร้อม robots.txt compliance
   - MinIO Uploader ตาม Medallion Architecture
   
   ### 🏗️ Bronze Layer Implementation  
   - โครงสร้างข้อมูลแบบ partitioned (year/month/day)
   - รองรับหลายรูปแบบไฟล์ (JSON, CSV, Parquet)
   - Metadata tracking และ error handling
   
   ### 📚 Learning Materials
   - Jupyter notebooks สำหรับ hands-on learning
   
   ### ✅ ผลลัพธ์ที่ได้
   - [x] ดึงข้อมูลจาก APIs ได้สำเร็จ
   - [x] Web scraping ทำงานได้ถูกต้อง
   - [x] อัพโหลดข้อมูลไป MinIO Bronze layer ได้
   - [x] Notebooks รันได้ครบทุก cell
   ```
6. กด **Create pull request**

---

## 8. หลังจาก Review และ Merge

เมื่อทีม review แล้ว

1. กดปุ่ม **Merge pull request** บน GitHub
2. กด **Confirm merge**  
3. ลบ branch `lab/week3` บน GitHub

---

## 9. Pull การเปลี่ยนแปลงกลับมาที่เครื่อง

```bash
git checkout main
git pull origin main
```

---

## 10. ลบ Branch lab/week3 ที่เครื่อง

```bash
git branch -d lab/week3
```

---

**ขั้นตอนต่อไป**: Week 4 จะเรียนรู้การแปลงข้อมูลจาก Bronze ไป Silver layer ด้วย dbt! 🚀