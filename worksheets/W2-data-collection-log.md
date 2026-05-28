<!-- workshop-header -->
<img width="1347" height="127" alt="Coding Thailand 2026 header" src="https://github.com/user-attachments/assets/ba5cf267-f460-4fb0-b69b-c461ae061a3b" />

# 📝 Worksheet W2 — Data Collection Log

> **ทำในช่วง 10:30-12:00**
> บันทึก process ของการเก็บข้อมูล

---

## ข้อมูลทีม + Edge Impulse

- **ชื่อทีม:** Darasamutr
- **Edge Impulse Project URL:**
  ```
  https://studio.edgeimpulse.com/studio/XXXXX
  ```

---

## 1. Setup Log

ก่อนเริ่มเก็บข้อมูล ทีมทำอะไรบ้าง?

| เวลา | ทำอะไร | ผู้รับผิดชอบ |
|---|---|---|
| 10:30 | จัดมุมกล้องติดตั้ง Webcam เหนือชั้นวางให้อยู่ในระดับสายตา | ภาณุ |
| 10:35 | จัดแสงสว่างบริเวณชั้นวาง (Test แสง 2 ระดับ) | ชินพัฒน์ |
| 10:45 | ล้างข้อมูลเก่าและตั้งชื่อโปรเจกต์ใน Edge Impulse | นภัทร |

---

## 2. Data Collection Sessions

บันทึกแต่ละ session การเก็บข้อมูล:

### Session 1

- **เวลา:** 10:50 ถึง 11:10
- **Class:** Empty_Shelf
- **จำนวน samples ที่เก็บ:** 110
- **สภาพแวดล้อม:** แสงปกติในห้องเรียน
- **ใครเป็น subject?:** _________________
- **Variation ที่ลอง:** มุมกล้องซ้าย-ขวา เล็กน้อย
- **ปัญหาที่เจอ:** แสงสะท้อนจากพื้นชั้นวาง

### Session 2

- **เวลา:** 11:15 ถึง 11:40
- **Class:** Tool_Present
- **จำนวน samples ที่เก็บ:** 110
- **สภาพแวดล้อม:** แสงปกติและแสงมืดลงเล็กน้อย
- **ใครเป็น subject?:** สมาชิกทีม
- **Variation ที่ลอง:** เปลี่ยนประเภทของอุปกรณ์ (กรรไกร, คีม)
- **ปัญหาที่เจอ:** อุปกรณ์บังกันเองในบางมุม

### Session 3

- **เวลา:** 11:45 ถึง 12:00
- **Class:** Hand_Reaching
- **จำนวน samples ที่เก็บ:** 110
- **สภาพแวดล้อม:** แสงปกติ
- **ใครเป็น subject?:** สลับกัน 3 คน
- **Variation ที่ลอง:** ความเร็วในการเอื้อมมือ (เร็ว/ช้า)
- **ปัญหาที่เจอ:** ภาพเบลอเมื่อเอื้อมมือเร็วเกินไป

> หาก session มากกว่า 3 ให้ copy template เพิ่ม

---

## 3. Dataset Summary

| Class | จำนวน Train | จำนวน Test | สัดส่วน Train:Test |
|---|---|---|---|
| Empty_Shelf | 88 | 22 | 80:20 |
| Tool_Present | 88 | 22 | 80:20 |
| Hand_Reaching | 88 | 22 | 80:20 |
| **รวม** | 264 | 66 | 80:20 |

**เป้าหมายตาม W1:** 100 samples × class
**ทำได้จริง:** 100 samples × class
**ห่างจากเป้า:** +10% (บรรลุเป้าหมาย)

---

## 4. Quality Check

ตอบทุกข้อก่อนเริ่ม train:

- [ x ] ทุก class มี samples ใกล้เคียงกัน (ไม่ต่างกันเกิน 20%)
- [ x ] เก็บใน ≥2 สภาพแวดล้อม
- [ x ] เก็บจาก ≥2 subjects (Vision/Audio/Motion ที่มีคน)
- [ x ] มี variation ใน angle/distance/lighting
- [ x ] ไม่มี mislabeled data (เช็คตัวอย่างแล้ว)
- [ x ] Train:Test split = 80:20

---

## 5. Reflection — สิ่งที่เรียนรู้

### a) สิ่งที่ยากที่สุด:
```
การควบคุม "ความเร็วของมือ" ให้ AI จับภาพได้ชัดเจนโดยไม่เบลอ (Motion Blur)
```

### b) ถ้าทำใหม่จะปรับอะไร:
```
จะใช้ขาตั้งกล้องที่มั่นคงกว่านี้ และเพิ่มความสว่างของไฟหน้าชั้นวางให้มากขึ้นเพื่อลด Noise ในภาพ
```

### c) คาดการณ์: model จะ confuse class ไหนกับอะไรมากที่สุด?
```
อาจจะสับสนระหว่าง Tool_Present กับ Hand_Reaching ในจังหวะที่มือเริ่มแตะอุปกรณ์ เพราะขอบของวัตถุกับมืออาจซ้อนทับกัน
```

---

## 📤 วิธี submit

```bash
git add worksheets/W2-data-collection-log.md
git commit -m "docs: data collection log เก็บได้ครบ X samples ใน Y session"
git push
```

---

## 💡 Best Practices

1. **อย่าเก็บข้อมูลที่ "สมบูรณ์แบบ" หมด** — โลกจริงไม่สมบูรณ์แบบ
2. **เก็บข้อมูล "เหมือนไม่ใช่ class ใดเลย" เป็นอีก class** = noise/background class
3. **สลับคนเก็บ** — กัน bias ของ subject เดียว
4. **เช็คตัวอย่างทุก 20 samples** — กัน mislabel
