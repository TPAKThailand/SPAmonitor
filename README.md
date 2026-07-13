# SPA14 Monitor

ระบบติดตามคุณภาพข้อมูลภาคสนาม — โครงการสำรวจกิจกรรมทางกายระดับประเทศ ครั้งที่ 14 (SPA14)
Thailand Physical Activity Knowledge (TPAK), มหาวิทยาลัยมหิดล

## การใช้งาน

1. เปิดเว็บไซต์ (GitHub Pages) หรือเปิดไฟล์ `index.html` ในเครื่องโดยตรง
2. เลือกไฟล์ข้อมูลดิบจาก LimeSurvey (.xlsx) — ต้องมีชีตที่มีคอลัมน์รหัส เช่น `C1. ...`
3. ระบบจะประมวลผลและแสดงผล 7 หน้า: ภาพรวม, ความก้าวหน้า, ตรวจ GPAQ, ตรวจ 24 ชม., เวลาสัมภาษณ์, ทีมงานสนาม, สรุปรวม

## ความปลอดภัยของข้อมูล (PDPA)

- **ข้อมูลไม่ถูกส่งออกจากเครื่องผู้ใช้** — การประมวลผลทั้งหมดเกิดขึ้นในเบราว์เซอร์ (client-side) เท่านั้น
- GitHub Pages ทำหน้าที่เพียงเสิร์ฟไฟล์ HTML แบบ static — ไม่มี server รับข้อมูล ไม่มีฐานข้อมูล ไม่มีการเก็บ log ข้อมูลผู้ตอบ
- ปิดหน้าเว็บ = ข้อมูลหายจากหน่วยความจำทันที
- แนะนำ: ตั้งค่า repository เป็น **Private** ไม่ได้ผลกับ GitHub Pages ฟรี (Pages ของ repo private ต้องใช้แผน Pro/Team) — ตัวไฟล์ `index.html` ไม่มีข้อมูลผู้ตอบฝังอยู่ จึงเผยแพร่เป็น public ได้อย่างปลอดภัย

## การ Deploy ขึ้น GitHub Pages

### วิธีที่ 1: ผ่านหน้าเว็บ GitHub (ง่ายสุด)

1. สร้าง repository ใหม่ เช่น `spa14-monitor`
2. อัปโหลดไฟล์ทั้งหมดในโฟลเดอร์นี้ (ลากวางได้)
3. ไปที่ **Settings → Pages**
4. Source: เลือก **Deploy from a branch** → Branch: `main` → โฟลเดอร์ `/ (root)` → Save
5. รอ 1–2 นาที เว็บไซต์จะอยู่ที่ `https://<username>.github.io/spa14-monitor/`

### วิธีที่ 2: ผ่าน Git command line

```bash
git init
git add .
git commit -m "Deploy SPA14 Monitor v2"
git branch -M main
git remote add origin https://github.com/<username>/spa14-monitor.git
git push -u origin main
```

จากนั้นตั้งค่า Pages ตามข้อ 3–5 ของวิธีที่ 1

### วิธีที่ 3: GitHub Actions (มี workflow ให้แล้ว)

ไฟล์ `.github/workflows/deploy.yml` ถูกเตรียมไว้แล้ว — ถ้าตั้งค่า **Settings → Pages → Source: GitHub Actions** ระบบจะ deploy อัตโนมัติทุกครั้งที่ push ขึ้น branch `main`

## การอัปเดตเวอร์ชัน

แทนที่ไฟล์ `index.html` ด้วยเวอร์ชันใหม่ แล้ว commit + push — Pages จะอัปเดตเองภายใน 1–2 นาที (ถ้าเปิดแล้วยังเห็นเวอร์ชันเก่า ให้กด hard refresh: `Ctrl+Shift+R`)

## โครงสร้างไฟล์

```
├── index.html                     # แอปทั้งหมดในไฟล์เดียว (ฝังไลบรารีครบ ใช้งานออฟไลน์ได้)
├── README.md
└── .github/workflows/deploy.yml   # workflow สำหรับ deploy อัตโนมัติ (ทางเลือก)
```
