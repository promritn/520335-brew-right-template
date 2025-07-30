# Lab Week 4: Data Transformation with dbt
## จากข้อมูลดิบสู่ข้อมูลที่พร้อมใช้งาน

## 0. สร้าง Branch ใหม่ 
```bash
git checkout -b lab/week4
```

## 1. เตรียมความพร้อม

### 1.1 ตรวจสอบโครงสร้างโปรเจกต์
```bash
ls -la notebooks/
ls -la dbt_project/
```

ควรแสดง:
```
notebooks/
├── week04_data_transformation.ipynb  # ไฟล์ใหม่ที่เราจะใช้

dbt_project/
├── .gitkeep
```

### 1.2 เริ่ม Docker Services
```bash
docker-compose up -d
```

ตรวจสอบว่า services ทำงานแล้ว:
```bash
docker-compose ps
```

---

## 2. ทำงานกับ Notebook: Data Transformation

ใช้ VS Code เปิดไฟล์ `notebooks/week04_data_transformation.ipynb`

### 2.1 เรียนรู้แนวคิด Medallion Architecture
- ทำความเข้าใจ Bronze, Silver, Gold layers
- ดูตัวอย่างปัญหาของข้อมูลดิบ
- เรียนรู้วิธีการแก้ไขด้วย Data Transformation

### 2.2 ติดตั้งและตั้งค่า dbt
- ติดตั้ง dbt-duckdb
- สร้าง dbt project structure
- ตั้งค่า profiles.yml

### 2.3 สร้างข้อมูลตัวอย่าง
- สร้างข้อมูลใน DuckDB
- เตรียม Bronze layer data
- ทดสอบการเชื่อมต่อ

### 2.4 สร้าง dbt Models
- **Sources**: กำหนดแหล่งข้อมูล Bronze layer
- **Staging Models**: สร้าง Silver layer (stg_orders.sql)
- **Marts Models**: สร้าง Gold layer (daily_sales_summary.sql, customer_summary.sql)

### 2.5 รัน dbt และตรวจสอบผลลัพธ์
- รัน `dbt run` เพื่อสร้าง models
- รัน `dbt test` เพื่อตรวจสอบคุณภาพข้อมูล
- ดูผลลัพธ์ใน DuckDB

---

## 3. เรียนรู้ 5 ขั้นตอนการ Transform ข้อมูล

### 3.1 Data Profiling
- วิเคราะห์ข้อมูลดิบ
- หาปัญหาและ patterns
- นับ NULL values และ data types

### 3.2 Data Cleaning
- แก้ไขข้อผิดพลาด
- จัดการ invalid data
- ทำความสะอาด strings

### 3.3 Data Standardization
- ทำให้รูปแบบเป็นมาตรฐานเดียวกัน
- แปลงวันที่และสกุลเงิน
- Normalize naming conventions

### 3.4 Data Deduplication
- กำจัดข้อมูลซ้ำ
- Exact vs Fuzzy matching
- Business rule based deduplication

### 3.5 Data Enrichment
- เพิ่มคุณค่าให้ข้อมูล
- Derived fields และ calculations
- External data joins

---

## 4. Data Quality Testing

### 4.1 Built-in Tests
- unique, not_null, accepted_values
- relationships tests
- Schema validation

### 4.2 Custom Tests
- สร้าง custom SQL tests
- Business rule validation
- Cross-table consistency checks

### 4.3 Data Quality Dashboard
- สร้าง metrics dashboard
- Monitor data completeness
- Track data freshness

---

## 5. Best Practices และเทคนิคขั้นสูง

### 5.1 Incremental Models
- เรียนรู้การประมวลผลแบบ incremental
- จัดการข้อมูลขนาดใหญ่
- Optimize performance

### 5.2 Macros และ Reusability
- สร้าง reusable SQL logic
- Currency conversion macros
- Data quality check macros

### 5.3 Documentation
- เขียน comprehensive documentation
- Column descriptions
- Model lineage

---

## 6. การบ้านและแบบฝึกหัด

### 6.1 Lab Exercise
- เพิ่ม Product Analysis Model
- สร้าง Custom Tests
- เพิ่ม Documentation

### 6.2 Challenge (ขั้นสูง)
- Time Series Analysis
- Customer Segmentation
- Data Quality Monitoring

---

## 7. Stage & Commit โค้ดทั้งหมด

```bash
git add .
git commit -m "Add Week 4 Data Transformation with dbt implementation"
```

---

## 8. Push branch ขึ้น remote

```bash
git push origin lab/week4
```

---

## 9. สร้าง Pull Request

1. ไปที่หน้า GitHub ของ repo
2. จะเห็นปุ่ม **Compare & pull request**
3. คลิก **Compare & pull request**
4. ใส่หัวเรื่อง: `Week 4: Data Transformation with dbt Implementation`
5. ใส่รายละเอียด:
   ```
   ## สิ่งที่เพิ่มใน Week 4
   
   ### 🔄 Data Transformation Pipeline
   - dbt project setup พร้อม DuckDB integration
   - Medallion Architecture implementation (Bronze → Silver → Gold)
   - Comprehensive data cleaning และ standardization
   
   ### 🏗️ dbt Models Implementation  
   - Sources configuration สำหรับ Bronze layer
   - Staging models (Silver layer) พร้อม data quality rules
   - Marts models (Gold layer) สำหรับ business analytics
   
   ### 🧪 Data Quality Testing
   - Built-in tests (unique, not_null, accepted_values)
   - Custom SQL tests สำหรับ business rules
   - Data quality metrics dashboard
   
   ### 📚 Learning Materials
   - Jupyter notebook พร้อม hands-on examples
   - 5 ขั้นตอนการ transform ข้อมูล
   - Best practices และเทคนิคขั้นสูง
   
   ### ✅ ผลลัพธ์ที่ได้
   - [x] dbt models รันได้สำเร็จ
   - [x] Data quality tests ผ่านทั้งหมด
   - [x] Bronze → Silver → Gold transformation สมบูรณ์
   - [x] Documentation และ schema tests ครบถ้วน
   ```
6. กด **Create pull request**

---

## 10. หลังจาก Review และ Merge

เมื่อทีม review แล้ว:

1. กดปุ่ม **Merge pull request** บน GitHub
2. กด **Confirm merge**  
3. ลบ branch `lab/week4` บน GitHub

---

## 11. Pull การเปลี่ยนแปลงกลับมาที่เครื่อง

```bash
git checkout main
git pull origin main
```

---

## 12. ลบ Branch lab/week4 ที่เครื่อง

```bash
git branch -d lab/week4
```

---

## 🎯 สิ่งที่ได้เรียนรู้ใน Week 4

### แนวคิดหลัก
- **Medallion Architecture**: Bronze → Silver → Gold
- **Data Transformation**: 5 ขั้นตอนสำคัญ
- **dbt**: Modern data transformation tool
- **Data Quality**: Testing และ monitoring

### ทักษะปฏิบัติ
- สร้างและจัดการ dbt project
- เขียน SQL models แบบมืออาชีพ
- ทดสอบคุณภาพข้อมูลอย่างเป็นระบบ
- สร้าง documentation ที่มีคุณภาพ

### เครื่องมือที่ใช้
- **dbt**: Data transformation framework
- **DuckDB**: In-memory analytical database
- **SQL**: ภาษาสำหรับ data transformation
- **Git**: Version control สำหรับ data code

---

**ขั้นตอนต่อไป**: Week 5 จะเรียนรู้การสร้าง CI/CD Pipeline เพื่อ automate การ deploy และ test dbt models! 🚀