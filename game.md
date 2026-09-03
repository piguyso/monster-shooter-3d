# MONSTER SHOOTER 3D - MULTIPLAYER BOT COMPETITION & COSTUMES (FPS)
**เอกสารสรุปข้อกำหนด โครงสร้างเกม และแผนการพัฒนา (Game Design Document & Roadmap - 3D FPS Edition)**

> เอกสารฉบับนี้ถูกปรับปรุงสำหรับการอัปเกรดเป็นเกม **3D First-Person Shooter (FPS)** โดยใช้ WebGL (Three.js)
> 
> 🌐 **เล่นเกมออนไลน์สด (Live Game URL):** [https://piguyso.github.io/monster-shooter-3d/](https://piguyso.github.io/monster-shooter-3d/)
> 📦 **GitHub Repository:** [https://github.com/piguyso/monster-shooter-3d](https://github.com/piguyso/monster-shooter-3d)

---

## 1. ภาพรวมของเกม (Game Overview)
* **ชื่อเกม:** Monster Shooter 3D - Multiplayer Bot Competition & Costumes
* **รูปแบบเกม:** 3D First-Person Shooter (FPS) Action Arcade บน WebGL / Three.js
* **แพลตฟอร์ม:** Web Browser (รองรับทั้ง Desktop ด้วย Pointer Lock Mouse Look และ Mobile Touch FPS Controls)
* **จุดเด่นหลัก:**
  * มุมมองบุคคลที่หนึ่ง (First-Person Perspective) พร้อมโมเดลปืน 3 มิติ (Cyber Blaster) ถืออยู่ในมือ ขยับส่ายตามจังหวะเดิน (Weapon Bobbing) และมีแรงดีด (Recoil)
  * ระบบคอสตูม 5 สี พร้อมหน้าพรีวิว **3D Canvas Model Preview** หมุนโชว์อาวุธ/ตัวละครในหน้าเมนูหลัก
  * ระบบแข่งขันคะแนน Real-time แข่งกับบอท AI แบบ 3 มิติ (Bot-Alpha และ Bot-Blaze) บน Live Leaderboard
  * ระบบต่อสู้ 2 Wave ในสนามประลอง 3D Sci-Fi Arena (Wave 1: ฝูงมอนสเตอร์เอเลี่ยน 3D | Wave 2: มหาบอส Lord Demon 3 มิติตัวมหึมามีปีกขยับได้)
  * ระบบเสียงสังเคราะห์เอฟเฟกต์ (Web Audio API Synthesizer) โดยไม่ต้องดาวน์โหลดไฟล์เสียงภายนอก
  * ระบบโหมดทดสอบสำหรับนักพัฒนา (Developer Testing Panel) เพื่อตรวจสอบฟีเจอร์ต่างๆ ได้ทันใจ

---

## 2. การควบคุมและปุ่มกด (Controls & Inputs - 3D FPS)

| คำสั่ง / ฟังก์ชัน | Desktop (คีย์บอร์ด & เมาส์ FPS) | Mobile (Touch FPS Controls) |
| :--- | :--- | :--- |
| **มุมกล้อง 3D (Aim & Look)** | ขยับเมาส์อย่างอิสระ (Pointer Lock 360 องศา) | ลากนิ้วบนครึ่งขวาของหน้าจอ (Touch Look Area) |
| **เคลื่อนที่ (3D Movement)** | ปุ่ม `W`, `A`, `S`, `D` หรือลูกศร (เดินหน้า, ถอยหลัง, สไลด์ซ้าย-ขวา) | Virtual Joystick บนครึ่งซ้ายของหน้าจอ |
| **ยิงกระสุนปืน (Shoot)** | คลิกเมาส์ซ้าย (Left Click) ยิงกระสุนพลาสมา 3D | ปุ่ม Fire หรือแตะบนหน้าจอเพื่อยิง |
| **แดชหลบหลีก (Dash Skill)** | ปุ่ม `SPACEBAR` (พุ่งตัวไปข้างหน้าพร้อมเอฟเฟกต์ FOV Warp, Cooldown 1.2 วินาที) | ปุ่ม Dash บนหน้าจอ |
| **ท่าไม้ตาย (Ultimate Nuke)**| ปุ่ม `Q` (ระเบิดคลื่นพลังงาน 3D Shockwave ล้างบาง เมื่อ Boost 100%) | ปุ่ม Ultimate (Q) รูปอะตอมพลังงาน |
| **หยุดเกม / ปลดล็อคเมาส์** | ปุ่ม `ESC` หรือ `P` | ปุ่มฟันเฟือง (Settings) บน HUD |

---

## 3. ระบบตัวละครและการปรับแต่ง (Characters & Costumes)

### 3.1 ตัวเลือกสีคอสตูม (Costume Color Selector)
ผู้เล่นสามารถเลือกสีคอสตูม/สีอาวุธ 5 สี โดยจะสะท้อนบนโมเดลปืน 3 มิติของผู้เล่นในเกม และโมเดล 3D Preview ในหน้า Lobby:
1. **Classic Azure (ฟ้ามาตรฐาน):** `#0284c7`
2. **Crimson Fury (แดงคริมสัน):** `#dc2626`
3. **Emerald Hunter (เขียวมรกต):** `#16a34a`
4. **Neon Violet (ม่วงนีออน):** `#9333ea`
5. **Solar Gold (ทองสว่าง):** `#d97706`

### 3.2 ค่าพลังตัวละคร (Player Attributes)
* **พลังชีวิต (HP):** สูงสุด 100 หน่วย (หากหมดจะ Game Over)
* **เกราะป้องกัน (Shield):** สูงสุด 50 หน่วย (รับความเสียหายแทน HP ก่อนเสมอ)
* **เกจไม้ตาย (Boost):** สูงสุด 100% (สะสมจากการยิงโดน สังหารศัตรู หรือเก็บไอเทม Boost)
* **ระบบคริติคอล (Critical Hit System):**
  * โอกาสติดคริติคอล (Crit Chance): **59%**
  * ตัวคูณความเสียหายคริติคอล (Crit Multiplier): **2.45 เท่า** (แสดงตัวเลขลอยสีทอง 3D ชัดเจน)

### 3.3 บอทผู้ร่วมรบ 3D (AI Companions & Competitors)
* **Bot-Alpha (สีม่วง `#9333ea`) & Bot-Blaze (สีส้ม `#f97316`):**
  * โมเดลหุ่นยนต์ไซเบอร์ 3 มิติพร้อมปืน เดินลาดตระเวนและเล็งยิงมอนสเตอร์ในพื้นที่ 3 มิติ
  * เก็บคะแนนและขึ้นแข่งขันบน Live Leaderboard แบบเรียลไทม์

---

## 4. แผนที่ 3D และสิ่งแวดล้อม (3D Environment & Obstacles)
* **Sci-Fi Battle Arena:** แผนที่กว้างสไตล์ไซไฟ พร้อมพื้นเรืองแสง Cyber Grid และกำแพงนีออนกั้นขอบเขต
* **สิ่งกีดขวาง 3 มิติ (5 Pillars & Barricades):** เสาและแท่นหินไซไฟ 5 จุด บล็อกการเดินและบล็อกกระสุนทั้งของผู้เล่นและศัตรู
* **Dynamic 3D Lighting:** แสงเงาสมจริงรอบสนามประลอง แสงแฟลชจากปากกระบอกปืน และแสงสะท้อนจากกระสุนพลาสมา

---

## 5. ศัตรูและระบบ WAVE แบบ 3 มิติ (3D Enemies & Wave System)

### 5.1 Wave 1: ฝูงมอนสเตอร์เอเลี่ยน 3D (Monster Horde)
* **จำนวนมอนสเตอร์รวม:** 20 ตัว (ทยอยเกิดจากรอบขอบสนาม 3 มิติ)
* **โมเดลศัตรู:** สัตว์ประหลาดไซเบอร์ 3D ดวงตาสีแดงเรืองแสง วิ่งพุ่งเข้าหาผู้เล่นและบอท
* **ค่าสถานะ:** HP 35 | พุ่งเข้าโจมตีระยะประชิด
* **รางวัล:** +100 คะแนนต่อการกำจัด 1 ตัว พร้อมโอกาส 40% ดรอปไอเทม 3D ลอยหมุนได้ (Heal, Shield, Boost)

### 5.2 Wave 2: การต่อสู้กับบอส 3 มิติ (Boss Fight - Lord Demon 3D)
* **ชื่อบอส:** Lord Demon
* **ลักษณะ 3 มิติ:** มหาบอสปีศาจขนาดยักษ์ลอยเด่นกลางอากาศ พร้อมปีกปีศาจ 3D ที่ขยับกระพือได้ เขาคู่สีแดงสด และแกนกลางเรืองแสง
* **ค่าสถานะ:** HP 1,200 | มีหลอดเลือดบอสขนาดใหญ่บนหน้าจอ
* **รูปแบบการโจมตี 3 มิติ (3 Attack Patterns):**
  1. **Radial Ring:** กระสุนพลังงาน 14 ทิศทางกระจายเป็นวงแหวน 3 มิติรอบตัวบอส
  2. **Focused Spread:** กระสุนความเร็วสูง 3 นัดยิงพุ่งตรงเล็งหาผู้เล่นแบบมุมกระจาย
  3. **Spiral Barrage:** พายุกระสุน 8 นัดหมุนวนเกลียวพุ่งใส่เป้าหมาย
* **รางวัล:** +1,500 คะแนนเมื่อปราบบอสสำเร็จ

---

## 6. ระบบเสียงเอฟเฟกต์ (Web Audio API Synthesizer)
เสียงสังเคราะห์ผ่าน Web Audio API 10 รูปแบบ:
* `shoot`, `hit`, `crit`, `dash`, `pickup`, `nuke`, `playerHurt`, `bossAttack`, `victory`, `defeat`
* ตัวเลื่อนปรับ Master SFX Volume และปุ่มเปิด/ปิดเสียง Mute

---

## 7. ส่วนต่อประสานผู้ใช้ (HUD, Crosshair & Modals)
* **First-Person Crosshair:** เป้าเล็งตรงกึ่งกลางหน้าจอ ปรับเปลี่ยนอนิเมชันเมื่อยิงโดน (Hitmarker)
* **Top HUD:** แถบ HP, Shield, Boost Meter (กะพริบเรืองแสงเมื่อ 100%), Dash Cooldown, จำนวนศัตรูคงเหลือ, Wave Badge, Real-time Leaderboard
* **Modals:** Start Lobby (พร้อม 3D Model Preview), How to Play, Pause & Settings, Victory & Game Over พร้อม Combat Analytics สถิติละเอียด
* **Developer Testing Panel:** แถบสูตรโกง (God Mode, Max Boost, เลือดเต็ม, เสกมอนสเตอร์, เสกบอสทันที, ฆ่าศัตรูทั้งหมด)

---

## 8. บันทึกความคืบหน้าและการวางแผนพัฒนา (Roadmap & Changelog)

| รายการระบบ / ฟังก์ชัน | ความสำคัญ | สถานะปัจจุบัน | หมายเหตุ |
| :--- | :---: | :---: | :--- |
| **จัดทำเอกสารข้อกำหนด `game.md` (3D FPS Edition)** | สูง | ✅ เสร็จสิ้น | กำหนดสเปกและข้อกำหนด 3D FPS ครบถ้วน |
| **จัดทำแผนการพัฒนา (`implementation_plan.md`)** | สูง | ✅ เสร็จสิ้น | วางแผนสถาปัตยกรรม Three.js และระบบ Pointer Lock |
| **ติดตั้ง Three.js & Setup 3D Scene / Renderer** | สูง | ✅ เสร็จสิ้น | สร้าง Scene, Perspective Camera, Lighting, Shadows |
| **ระบบควบคุม FPS (Pointer Lock, WASD, Dash FOV Warp)** | สูง | ✅ เสร็จสิ้น | หันกล้องอิสระ 360 องศา และการเคลื่อนที่ตามมุมกล้อง |
| **โมเดลปืน 3D มุมมองบุคคลที่หนึ่ง & 3D Lobby Preview** | สูง | ✅ เสร็จสิ้น | ปืน 3D เปลี่ยนสีตามคอสตูม มี Recoil & Muzzle Flash |
| **ระบบกระสุน 3D, Hit Detection & Crit 59% (2.45x)** | สูง | ✅ เสร็จสิ้น | กระสุนพลาสมา 3D พุ่งออกจากปืน พร้อมตัวเลขดาเมจ 3D |
| **ระบบ AI Companions 3D (Bot-Alpha, Bot-Blaze)** | สูง | ✅ เสร็จสิ้น | หุ่นยนต์ 3D เดินยิงศัตรูและแข่งขันคะแนนสด |
| **ระบบ Wave 1 (มอนสเตอร์ 3D 20 ตัว + ไอเทมดรอป 3D)** | สูง | ✅ เสร็จสิ้น | มอนสเตอร์ 3D วิ่งไล่กวด พร้อมไอเทม 3D หมุนเคว้ง |
| **ระบบ Wave 2 (บอส Lord Demon 3D - ปีกขยับได้ 3 ท่าโจมตี)** | สูง | ✅ เสร็จสิ้น | บอส 3 มิติขนาดยักษ์ ปล่อยกระสุน 3D สลับรูปแบบ |
| **ระบบแผนที่ Sci-Fi Arena 3D & สิ่งกีดขวาง 5 จุด** | ปานกลาง | ✅ เสร็จสิ้น | พื้น Grid Sci-Fi พร้อมเสาหินและกำแพง 3D |
| **ระบบเสียงสังเคราะห์ Web Audio API & UI Glassmorphism** | ปานกลาง | ✅ เสร็จสิ้น | HUD ครบถ้วนพร้อมเป้าเล็ง Crosshair และ Leaderboard |
| **แถบเครื่องมือทดสอบสำหรับนักพัฒนา (Dev Test Panel)** | ปานกลาง | ✅ เสร็จสิ้น | ปุ่ม God Mode, เสกบอส 3D, เติมเลือด, ล้างศัตรู |

