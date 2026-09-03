# MONSTER SHOOTER 3D - MULTI-STAGE FLOW LINE & BOSS BATTLES (FPS)
**เอกสารสรุปข้อกำหนด โครงสร้างเกม และแผนการพัฒนา (Game Design Document & Roadmap - Multi-Stage Edition)**

> เอกสารฉบับนี้ถูกปรับปรุงสำหรับการเพิ่มระบบ **หลายด่าน (Multi-Stage)**, หน้าเลือกด่านแบบ **Flow Line**, มอนสเตอร์หลากหลายชนิด และมหาบอสประจำแต่ละด่าน
> 
> 🌐 **เล่นเกมออนไลน์สด (Live Game URL):** [https://piguyso.github.io/monster-shooter-3d/](https://piguyso.github.io/monster-shooter-3d/)
> 📦 **GitHub Repository:** [https://github.com/piguyso/monster-shooter-3d](https://github.com/piguyso/monster-shooter-3d)

---

## 1. ภาพรวมของเกม (Game Overview)
* **ชื่อเกม:** Monster Shooter 3D - Multi-Stage Flow Line & Boss Battles
* **รูปแบบเกม:** 3D First-Person Shooter (FPS) Action Arcade บน WebGL / Three.js
* **แพลตฟอร์ม:** Web Browser (Desktop Pointer Lock Mouse Look & Mobile Touch FPS Controls)
* **จุดเด่นหลักที่เพิ่มเข้ามา:**
  * **ระบบเลือกด่านแบบ Flow Line (Interactive Mission Roadmap):** หน้าเลือกด่านมีเส้นทาง Flow Line เรืองแสง เชื่อมโยง Stage 1 -> 2 -> 3 -> 4 ปลดล็อคด่านใหม่เมื่อกำจัดบอสด่านก่อนหน้าสำเร็จ (บันทึกลงใน `localStorage`)
  * **ระบบสปอว์นบอสตามจำนวนการกำจัดมอนสเตอร์ (Boss Quota Spawn):** ในแต่ละด่าน ผู้เล่นต้องสังหารมอนสเตอร์ตามโควตาที่กำหนด (เช่น 15, 20, 25, 30 ตัว) จึงจะปลุกมหาบอสประจำด่านออกมา
  * **ความหลากหลายของศัตรู 3 มิติ (Enemy Variety):**
    1. **Cyber Creeper:** สัตว์ประหลาดสีแดง วิ่งไว พุ่งกัดระยะประชิด
    2. **Acid Spitter:** เอเลี่ยนสีเขียว ลอยกลางอากาศ ยิงกระสุนกรดพลาสมาใส่ผู้เล่นจากระยะไกล
    3. **Void Brute:** อสูรยักษ์สีม่วง เกราะหนา HP สูง โจมตีหนักหน่วง
  * **มหาบอสประจำแต่ละด่าน 3 มิติ (Unique Stage Bosses):**
    * **Stage 1 Boss:** *Cyber Golem 3D* (HP 800) หุ่นจักรกลไซเบอร์ ปืนใหญ่คู่
    * **Stage 2 Boss:** *Infernal Behemoth 3D* (HP 1,200) อสูรเขาเพลิง ปล่อยพายุลูกไฟ
    * **Stage 3 Boss:** *Lord Demon 3D* (HP 1,600) ปีกปีศาจขยับได้ พร้อม 3 ท่ากระสุนสุดโหด
    * **Stage 4 Boss:** *Omega Colossus 3D* (HP 2,400) มหาเทพจักรวาล ความยากระดับ Extreme

---

## 2. รายละเอียดระดับด่าน (Stage Progression & Flow Line)

| ด่าน (Stage) | ชื่อสมรภูมิ (Arena) | โควตามอนสเตอร์ | ชนิดมอนสเตอร์ | มหาบอสประจำด่าน (Boss) | เลือดบอส (HP) |
| :---: | :--- | :---: | :--- | :--- | :---: |
| **Stage 1** | **Neon Outpost (ค่ายฝึกนีออน)** | 15 ตัว | Cyber Creeper | Cyber Golem 3D | 800 |
| **Stage 2** | **Crimson Core (เหมืองลาวาเดือด)** | 20 ตัว | Creeper + Acid Spitter | Infernal Behemoth 3D | 1,200 |
| **Stage 3** | **Void Sanctum (วิหารมิติแห่งความมืด)** | 25 ตัว | Spitter + Void Brute | Lord Demon 3D | 1,600 |
| **Stage 4** | **Apocalypse Nexus (มิติล้างบาง)** | 30 ตัว | ทุกประเภทรุมโจมตี | Omega Colossus 3D | 2,400 |

---

## 3. การควบคุมและปุ่มกด (Controls & Inputs)

| คำสั่ง / ฟังก์ชัน | Desktop (คีย์บอร์ด & เมาส์ FPS) | Mobile (Touch FPS Controls) |
| :--- | :--- | :--- |
| **มุมกล้อง 3D (Aim & Look)** | ขยับเมาส์อย่างอิสระ (Pointer Lock 360 องศา) | ลากนิ้วบนครึ่งขวาของหน้าจอ |
| **เคลื่อนที่ (3D Movement)** | ปุ่ม `W`, `A`, `S`, `D` หรือลูกศร | Virtual Joystick บนครึ่งซ้ายของหน้าจอ |
| **ยิงกระสุนปืน (Shoot)** | คลิกเมาส์ซ้าย (Left Click) | ปุ่ม Fire บนหน้าจอ |
| **แดชหลบหลีก (Dash Skill)** | ปุ่ม `SPACEBAR` (Cooldown 1.2 วินาที, FOV Warp) | ปุ่ม Dash บนหน้าจอ |
| **ท่าไม้ตาย (Ultimate Nuke)**| ปุ่ม `Q` (ระเบิด 3D Shockwave ล้างบาง เมื่อ Boost 100%) | ปุ่ม Ultimate (Q) |
| **หยุดเกม / หน้าต่างตั้งค่า** | ปุ่ม `ESC` หรือ `P` | ปุ่มฟันเฟือง (Settings) บน HUD |

---

## 4. ระบบคอสตูม & อาวุธ 3D (Costumes & 3D Blaster)
* **5 สีคอสตูม:** Classic Azure (`#0284c7`), Crimson Fury (`#dc2626`), Emerald Hunter (`#16a34a`), Neon Violet (`#9333ea`), Solar Gold (`#d97706`)
* หน้าต่างปรับแต่งสีปืนพร้อม **3D Real-time Weapon Preview** หมุนโชว์ในโมดอล
* ปืน First-person Cyber Blaster ในมุมมองผู้เล่น เปลี่ยนสีตามคอสตูม พร้อมแอนิเมชัน Recoil และ Weapon Bobbing

---

## 5. ระบบเสียงสังเคราะห์ (Web Audio API Synthesizer)
สร้างเสียงเอฟเฟกต์ 10 เสียงผ่านโค้ด JavaScript ไม่ต้องโหลดไฟล์ MP3:
* `shoot`, `hit`, `crit`, `dash`, `pickup`, `nuke`, `playerHurt`, `bossAttack`, `victory`, `defeat`
* ตัวเลื่อนปรับ Master SFX Volume และปุ่มเปิด/ปิดเสียง Mute

---

## 6. บันทึกความคืบหน้าและการวางแผนพัฒนา (Roadmap & Changelog)

| รายการระบบ / ฟังก์ชัน | ความสำคัญ | สถานะปัจจุบัน | หมายเหตุ |
| :--- | :---: | :---: | :--- |
| **จัดทำเอกสารข้อกำหนด `game.md` (Multi-Stage Edition)** | สูง | ✅ เสร็จสิ้น | บันทึกรายละเอียดด่าน 1-4 และชนิดมอนสเตอร์/บอส |
| **ระบบหน้าเลือกด่านแบบ Flow Line (Animated SVG Path)** | สูง | ✅ เสร็จสิ้น | เส้นทาง Flow Line สวยงาม เชื่อมด่าน 1 -> 2 -> 3 -> 4 |
| **ระบบบันทึกการปลดล็อคด่าน (Progression LocalStorage)** | สูง | ✅ เสร็จสิ้น | บันทึกด่านที่ผ่านและปลดล็อคด่านถัดไปอัตโนมัติ |
| **ระบบสปอว์นบอสตามโควตากำจัดมอนสเตอร์ (Boss Quota)** | สูง | ✅ เสร็จสิ้น | กำจัดมอนสเตอร์ครบ 15, 20, 25, 30 ตัวจึงจะเสกบอส |
| **ระบบศัตรู 3D หลากหลายชนิด (Creeper, Spitter, Brute)** | สูง | ✅ เสร็จสิ้น | วิ่งไว, ยิงกระสุนกรดระยะไกล, และตัวใหญ่เกราะหนา |
| **ระบบมหาบอส 3D ประจำแต่ละด่าน (4 Boss Types)** | สูง | ✅ เสร็จสิ้น | Golem, Behemoth, Lord Demon, Omega Colossus |
| **ปุ่ม "ด่านถัดไป (Next Stage)" เมื่อผ่านด่านสำเร็จ** | ปานกลาง | ✅ เสร็จสิ้น | กดข้ามไปลุยด่านถัดไปได้ทันทีจากหน้า Victory Modal |
| **โมดอลปรับแต่งสีคอสตูมปืน 3D จากหน้า Flow Line** | ปานกลาง | ✅ เสร็จสิ้น | มี 3D Live Preview และปุ่มเลือกสี 5 สี |
| **Deploy เวอร์ชันล่าสุดขึ้น GitHub Pages อัตโนมัติ** | สูง | ✅ เสร็จสิ้น | ซิงค์โค้ดสดขึ้น https://piguyso.github.io/monster-shooter-3d/ |
