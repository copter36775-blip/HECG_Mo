# HECG01 Console — GitHub Pages

โฟลเดอร์นี้คือของที่จะขึ้น GitHub Pages เท่านั้น (ไฟล์เว็บล้วน ๆ)
**เฟิร์มแวร์ `src/main.cpp` ไม่ได้อยู่ในนี้** — ถ้า push โฟลเดอร์นี้อย่างเดียว
โค้ดเฟิร์มแวร์จะไม่ถูกเปิดเผย

| ไฟล์ | คืออะไร |
|---|---|
| `index.html` | หน้าแรก — เลือกเข้า mobile หรือ desktop + ตรวจว่าเบราว์เซอร์รองรับ Web Bluetooth ไหม |
| `hecg_mobile_v1.html` | คอนโซลตัวใหม่ — มือถือ + เดสก์ท็อปในไฟล์เดียว |
| `hecg_console.html` | คอนโซลเดสก์ท็อปเดิม (ไม่ถูกแก้) |
| `.nojekyll` | บอก GitHub Pages ว่าอย่าเอา Jekyll มายุ่ง |

---

## ขั้นตอน push ขึ้น GitHub Pages

### 0. ตั้งชื่อ-อีเมลให้ git ก่อน (ทำครั้งเดียวในชีวิต)

```bash
git config --global user.name  "ชื่อของพี่"
git config --global user.email "copter36775@gmail.com"
```

### 1. สร้าง repo เปล่าบน GitHub

ไปที่ <https://github.com/new>

- **Repository name**: `hecg01-console` (หรือชื่ออื่นที่ชอบ)
- **Public** ← ต้องเป็น public ถ้าใช้ GitHub ฟรี เพราะ Pages ของ repo ส่วนตัว
  ต้องมี GitHub Pro
- **อย่า** ติ๊ก "Add a README" / .gitignore / license (ให้มันว่างเปล่า)

กด **Create repository**

### 2. push จากเครื่อง

เปิด terminal ที่โฟลเดอร์ `publish` นี้ แล้วรัน (แทน `<USERNAME>` กับ `<REPO>`):

```bash
git add -A
git commit -m "HECG01 console: mobile v1 + desktop v3"
git branch -M main
git remote add origin https://github.com/<USERNAME>/<REPO>.git
git push -u origin main
```

ตอน push ครั้งแรก Windows จะเด้งหน้าต่างให้ login GitHub — login ตามปกติ

### 3. เปิด GitHub Pages

ใน repo บนเว็บ → **Settings** → **Pages** (เมนูซ้าย)

- **Source**: `Deploy from a branch`
- **Branch**: `main` / `/ (root)` → **Save**

รอประมาณ 1–2 นาที

### 4. ลิงก์ที่จะได้

```
https://<USERNAME>.github.io/<REPO>/                      ← หน้าแรก
https://<USERNAME>.github.io/<REPO>/hecg_mobile_v1.html   ← เข้ามือถือตรง ๆ
```

เอาลิงก์แรกเปิดบนมือถือได้เลย

---

## อัปเดตทีหลัง

ถ้าแก้ไฟล์ในโปรเจกต์แล้วอยากอัปขึ้นใหม่:

```bash
# จาก root ของโปรเจกต์ HECG01
cp web/hecg_mobile_v1.html web/hecg_console.html publish/

cd publish
git add -A
git commit -m "update console"
git push
```

---

## ข้อควรรู้

**HTTPS จำเป็น** — Web Bluetooth ทำงานเฉพาะบน secure context
GitHub Pages ให้ HTTPS มาอยู่แล้ว เลยใช้ได้เลย
(เปิดไฟล์จากมือถือตรง ๆ แบบ `file://` จะใช้ไม่ได้ นี่คือเหตุผลที่ต้อง host)

**Android** — เปิดด้วย Chrome หรือ Edge กด CONNECT ได้เลย
ครั้งแรกอาจขอสิทธิ์ตำแหน่ง/อุปกรณ์ใกล้เคียง (Android ผูก BLE scan ไว้กับสิทธิ์นั้น)

**iPhone / iPad** — **กด CONNECT ไม่ได้** Apple บังคับให้ทุกเบราว์เซอร์บน iOS
ใช้เอนจิน WebKit ซึ่งไม่มี Web Bluetooth แม้แต่ Chrome บน iOS ก็ต่อไม่ได้
หน้าเว็บจะเปิดได้ปกติ UI ใช้ได้หมด แต่ต่อบลูทูธไม่ได้
ถ้าจำเป็นต้องใช้ iPhone จริง ๆ มีทางเดียวคือเบราว์เซอร์อย่าง **Bluefy**
(แอปเสียเงินใน App Store ที่ทำ Web Bluetooth เองผ่าน CoreBluetooth)

**เพิ่มไอคอนลงโฮมสกรีน** — เปิดหน้าเว็บ → Share / เมนู → "Add to Home Screen"
จะได้ไอคอนเปิดแบบเต็มจอไม่มีแถบเบราว์เซอร์ (ใส่ meta ไว้ให้แล้ว)
