# hobi-web — Hobi Partner Portal

เว็บฝั่งลูกค้า (public-facing) สำหรับ **สมัครเป็นพาร์ตเนอร์** ของแพลตฟอร์มเช่าเครื่องจักร Hobi
เป็นคู่หูของ `hobi-dashboard` (ระบบหลังบ้านที่ทีมงานใช้จัดการพาร์ตเนอร์)

## หน้าเว็บมีอะไรบ้าง
- Landing page แนะนำ Hobi + สิทธิประโยชน์ของการเป็นพาร์ตเนอร์
- ขั้นตอนการสมัคร (How it works) + FAQ
- **ฟอร์มสมัครพาร์ตเนอร์** พร้อมตัวเลือกเครื่องจักรและแผนที่ปักหมุดตำแหน่ง
- รองรับธีมสว่าง/มืด (ใช้ดีไซน์เดียวกับแดชบอร์ด Hobi)

## เชื่อมกับแดชบอร์ดยังไง
ฟอร์มเขียนพาร์ตเนอร์ใหม่เข้า **Firebase Firestore ตัวเดียวกัน** กับแดชบอร์ด
(`hobi-partner-dashboard` → collection `hobi` → doc `data` → array `partners`)
โดยตั้งสถานะเป็น `pending` เมื่อมีคนสมัคร ข้อมูลจะเด้งขึ้นแดชบอร์ดแบบเรียลไทม์ทันที
(ใช้ Firestore transaction เพื่อ append อย่างปลอดภัย ไม่ทับข้อมูลเดิม และซิงก์ `partnerIdCounter`)

ฟิลด์ที่ส่งตรงกับ schema ของแดชบอร์ด:
`id, name, contact, phone, email, area, status, tags, price, lat, lng, address, notes`
(เพิ่ม `source:"partner-portal"` และ `appliedAt` ไว้ให้ทีมงานอ้างอิง)

## รันแบบ local
เป็นไฟล์ HTML ไฟล์เดียว เปิด `index.html` ในเบราว์เซอร์ได้เลย
หรือเสิร์ฟด้วย:

```bash
python3 -m http.server 8080
# เปิด http://localhost:8080
```

## Deploy
วางเป็น static site ได้ทุกที่ (GitHub Pages, Netlify, Vercel, Cloudflare Pages)
ตั้ง `index.html` เป็นหน้าแรกได้เลย ไม่ต้อง build

---
เทคโนโลยี: HTML/CSS/JS ล้วน · Tabler Icons · Leaflet (แผนที่) · Firebase Firestore (แชร์กับแดชบอร์ด)
