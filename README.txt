UsedBooks Market (PHP + MySQL) — เว็บซื้อขายหนังสือมือสอง
===========================================================

ติดตั้ง:
1) XAMPP / WAMP / Laragon
2) Import ฐานข้อมูล:
   - เข้า phpMyAdmin
   - Import ไฟล์ sql/schema.sql
   - จะสร้าง DB ชื่อ used_books_db + ตาราง + ข้อมูลตัวอย่าง

3) เอาโฟลเดอร์ used-books-web ไปไว้ใน htdocs:
   C:\xampp\htdocs\used-books-web

4) เปิดเว็บ:
   - หน้าเว็บ: http://localhost/used-books-web/public/index.php
   - หลังบ้าน: http://localhost/used-books-web/admin/index.php

แอดมินเริ่มต้น:
- admin@books.local / Admin@1234

ถ้าแอดมินเข้าไม่ได้:
- เปิด http://localhost/used-books-web/public/reset_admin.php
- เห็น OK แล้ว “ลบไฟล์ reset_admin.php ทิ้งทันที”


อัปเดต v2:
- หน้า Shop/หน้าแรก แสดงรูปปกสินค้า
- หลังบ้านมีหน้า Admin Login แยก: /admin/login.php


อัปเดต v3 (MEB-like):
- ธีมโทนสว่าง + โทนส้ม
- คลิกซูมรูปปก (Lightbox)
- ทดลองอ่าน (Preview) เปิดใน Popup + เปิดแท็บใหม่ได้
- หลังบ้านอัปโหลดไฟล์ทดลองอ่าน: Admin > หนังสือ > ทดลองอ่าน
- ถ้าอัปเดตจาก v2 ให้รัน sql/migrations_add_preview.sql


อัปเดต v4 (Dark fix):
- กลับธีมสีเดิมแบบ Dark Neon
- ซ่อม Overlay ให้ซูมปก + ทดลองอ่านทำงาน
- ตรวจว่า footer โหลด public/assets/js/ui.js แล้ว


อัปเดต v5 (ชำระเงิน):
- ระบบชำระเงินจริงแบบโอนเงิน + แนบสลิป
- ลูกค้าแจ้งสลิป: public/pay.php?order_id=...
- แอดมินตรวจสลิป: admin/payments.php
- ถ้าอัปเดตจากเวอร์ชันเก่าให้รัน sql/migrations_add_payments.sql


อัปเดต v7 (Google Login + Remember Me):
- Google Login: public/login_google.php และ callback: public/google_callback.php
- ตั้งค่าใน config/google.php (Client ID/Secret/Redirect URI)
- Remember me 30 วัน: checkbox ในหน้า login และ admin login
- Migration: sql/migrations_add_auth_tokens.sql + sql/migrations_add_google_columns.sql


=== v8 COMPLETE RESET (แนะนำ) ===
1) ลบ DB เก่า: DROP DATABASE used_books_db; แล้วสร้างใหม่
2) Import: sql/schema_full.sql (ไฟล์เดียวจบ)
3) ตั้งค่า Google OAuth: config/google.php (Client ID/Secret/Redirect URI)
Admin demo: admin@demo.com / admin1234


=== v10 (แก้ให้ใช้ได้ทั้งหมด) ===
- แก้ปัญหา is_published / categories ไม่ตรง schema
- config/db.php สร้าง DB + import schema_full + auto-fix ให้เอง
เปิดเว็บได้เลย: http://localhost/used-books-web/public/index.php
หลังบ้าน: http://localhost/used-books-web/admin/index.php (admin@demo.com / admin1234)


=== v11 AUTH MODAL (MEB-like) ===
- หน้าเข้าสู่ระบบ/สมัครสมาชิกแบบป๊อปอัป: public/auth.php
- Google login ใช้งานได้จริง (ตั้งค่าใน config/google.php)
- Facebook/LINE/Apple เป็นปุ่ม UI (ต้องตั้งค่า OAuth เพิ่ม)


=== v12 DARK FOOTER + COOKIE BAR ===
- เพิ่ม Footer สีดำ 4 คอลัมน์ + แถบ Cookie ด้านล่าง (คล้ายตัวอย่าง)


=== v13 ACCOUNT DRAWER ===
- เพิ่มเมนูบัญชีแบบ Drawer (คล้ายตัวอย่าง) เมื่อล็อกอินแล้ว
- หน้าใหม่: profile.php, address.php, privacy.php, settings.php


=== v14 COMPLETE (Admin login fixed + Healthcheck) ===
- แก้ปัญหาแอดมินเข้าไม่ได้: config/db.php จะ seed/reset แอดมินอัตโนมัติทุกครั้ง (dev)
- ตรวจระบบ: /public/health.php
- รีเซ็ตแอดมิน: /public/reset_admin.php?key=APP_SETUP_KEY (ดูค่าใน config/app.php)


=== v15 ADMIN AUTH FIX ===
- แก้ลิงก์ /admin/auth.php ให้ redirect ไป /admin/login.php


=== v16 BOOKWALKER-LIKE FILTERS ===
- หน้า shop.php เพิ่ม Search bar + Sidebar Filter (หมวดหมู่/สภาพ/ราคา) + Sort + Chips
- หลังบ้านเพิ่มฟิลด์ author/category/condition/description/publish (ถ้าไฟล์เดิมรองรับ)


=== v17 SHIPPING COLUMNS FIX ===
- แก้ Error: Unknown column shipping_name โดยเพิ่มคอลัมน์ shipping_* ในตาราง orders (auto-migrate ใน config/db.php)


=== v18 PRO BOOK DETAIL PAGE ===
- ปรับหน้า book.php ให้เหมือนเว็บมือโปร (คล้าย BookWalker): หน้าปกซ้าย, รายละเอียดขวา, ปุ่มทดลองอ่าน/ซื้อ, ตารางสเปก, แท็ก


=== v19 ADD TO CART FIX ===
- เพิ่มไฟล์ public/add_to_cart.php ให้ลิงก์ใส่ตะกร้าทำงาน ไม่ขึ้น Not Found


=== v20 ADMIN FULL CRUD + SOFT DELETE ===
- หลังบ้านแก้ไขหนังสือได้ครบ: author/publisher/series/file_type/list_price/tags/description/publish
- ป้องกันลบหนังสือแล้วติด FK: ถ้าลบไม่ได้จะ archive (is_deleted=1) และซ่อนจากหน้าร้าน


=== v21 ORDER_ITEMS SNAPSHOT FIX ===
- แก้ Error: Unknown column title_snapshot โดยเพิ่มคอลัมน์ title_snapshot/price_snapshot ใน order_items (auto-migrate)


=== v22 THEME + ADMIN REMEMBER ===
- ปรับโทนสีให้อ่านง่ายสบายตา
- หลังบ้านมีจดจำการเข้าสู่ระบบแอดมิน 30 วัน (remember token)


=== v23 THEME V1 + ADMIN SLIP PREVIEW ===
- โทนสีกลับเป็นแบบเวอร์ชันแรก (ส้ม/ดำแบบ glass)
- หลังบ้านดูสลิปโอนเงินแบบพรีวิวในหน้า payments.php (รองรับรูป + PDF)


=== v24 CART EMPTY FIX ===
- แก้ตะกร้าว่างเมื่อ stock=0: ถือว่าไม่จำกัดสต็อก


=== v25 COMPLETE + V1 THEME + DB MIGRATION ===
1) ใช้โทนสีแบบเวอร์ชันแรก (ส้ม/ดำ glass)
2) โค้ดรวมแพตช์ทั้งหมด: ตะกร้า/checkout/order_items snapshots/shipping/admin CRUD/soft delete/admin remember
3) ถ้า DB เก่า ให้รันไฟล์ sql/migrate_v25.sql ใน phpMyAdmin


=== v26 ADMIN ORDER DETAIL SLIP + GLOBAL COLOR ===
- หน้า admin/order_detail.php แสดงสลิปโอนเงิน (พรีวิว)
- ปรับสีให้ใช้โทนเดียวกันทั้งเว็บ/หลังบ้าน


=== v28 UX/UI + Social Login ALL (DEV mock) ===
- เพิ่ม Toast แจ้งเตือน, Ripple click, Hover micro-interactions
- ปรับโทนสีให้อ่านง่ายแต่ยังเป็น V1 Orange Glass
- Social Login เข้าได้ครบ: Google/Facebook/LINE/Apple (โหมด mock สำหรับทดสอบ)
  ตั้งค่าได้ที่ config/social.php (mock_enabled)
- add_to_cart รองรับ JSON (?ajax=1) + อัปเดต badge ตะกร้า


=== v29 Social Login fix ===
- แก้ social_lib ให้ตรงกับ schema: users.fullname (แทน name)
