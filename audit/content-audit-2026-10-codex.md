# Content Audit — Codex (gpt-5.6-terra) · 2026-10-02

Run: `~/.hermes/codex-runs/20261002T101154Z_I1zrYm/` (duration 222s, tokens ~100.5k, exit 0)
Scope: 14 sheets + index.html + flashcards.csv · Verdict: **PASS with minor fixes** (0 CRITICAL)

## Findings + triage (ทุกข้อถูกแก้ใน commit ถัดจากไฟล์นี้)

| # | Sev | File | ประเด็น | การแก้ |
|---|-----|------|---------|--------|
| 1 | MOD | 08-cicd | “ทีมระดับ elite” — DORA เลิกใช้กรอบ elite แล้ว | ✅ เปลี่ยนเป็น top performers / ใช้ปรับปรุงไม่ใช่จัดอันดับ |
| 2 | MOD | 08-cicd | “DORA 4 metrics” ขัดกับอัปเดต 5 metrics ในหน้าเดียวกัน | ✅ หัวข้อ/ต้องจำ/self-check → 5 ตัวปัจจุบัน + Four Keys เดิม |
| 3 | MOD | flashcards.csv | การ์ด DORA ล้าสมัย/ขัดกับ sheet | ✅ อัปเดตเป็น 5 ตัว |
| 4 | MOD | 10-docker | “แต่ละคำสั่งสร้าง layer” — CMD/ENV/EXPOSE เป็น metadata | ✅ ระบุ RUN/COPY/ADD สร้าง layer |
| 5 | MOD | 10-docker | “container ตาย → ไฟล์หาย” ไม่แม่น (หายเมื่อ `rm`) | ✅ แก้ + ระบุหยุดรันข้อมูลยังอยู่ |
| 6 | MOD | 06-programming | pass by value/reference เหมารวม (Java/Python) | ✅ pass-by-value ของ reference + mutate vs rebind |
| 7 | MOD | 07-version-control | `reset --hard` “ทิ้งทั้งหมด” — untracked ไม่หาย | ✅ ระบุ staged/tracked + untracked/ignored ยังอยู่ |
| 8 | MOD | 01-database | leftmost prefix “ไม่ใช้” เป็น absolute เกิน | ✅ คงคำตอบมาตรฐาน + โน้ต skip scan (MySQL 8.0.13+) |
| 9 | MOD | 14-ai-llm | attention เห็นทุก token — decoder ใช้ causal mask | ✅ แก้เป็น token ก่อนหน้า/causal mask |
| 10 | MIN | 03-security | Implicit “ถูกยกเลิก” — จริงคือ deprecated (RFC 9700) | ✅ แก้ทั้ง sheet + flashcard |
| 11 | MIN | 02-design | 422 “Validation” — ชื่อมาตรฐานคือ Unprocessable Content | ✅ แก้ตาม RFC 9110 |
| 12 | MIN | 10-docker + csv | ENTRYPOINT “ตายตัว” — override ได้ด้วย `--entrypoint` | ✅ แก้ทั้ง sheet + flashcard |

## Notes จากการ triage (ผู้ตรวจรอบสอง = Hermes)
- รายงานระบุสรุป “7 MOD / 3 MIN” แต่ตารางมีจริง 9 MOD / 3 MIN — ใช้ตัวเลขจากตาราง
- ข้อ 1 (elite): DORA เลิก tiering จริง แต่ถ้อยคำ “เลิกตั้งแต่ 2022” ของ Codex ไม่ได้ยืนยันครบ → ใช้ถ้อยคำกลาง (top performers) ไม่กล่าวอ้างปี
- ข้อ 8: Codex อ้าง PostgreSQL ทำ skip scan ได้ — Hermes ไม่ยืนยัน → ลดข้ออ้างเหลือ MySQL 8.0.13+ เท่านั้น
- Sheets 04, 05, 09, 11, 12, 13, index.html: ไม่พบประเด็น
